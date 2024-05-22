# Windows Portable Executable Overview

## Overview

Before reading further, I want you to know that this post is about research I did on static analysis. There is nothing new here - no new tools or features are being discovered. Everything that I talk about already exists in other tools. A big part of this research uses the OpenAI Chat GPT. I made sure to fact-check the information provided here, as the GPT can sometimes produce misleading output.

My research focuses on [Windows Portable Executable (PE)](https://learn.microsoft.com/en-us/windows-hardware/manufacture/desktop/winpe-intro?view=windows-11) files because they are the most common type. Therefore, we'll start by exploring how these files operate.

## Keywords 

- **RVA** (Relative Virtual Address) - the virtual address of an object from the file once it is loaded into memory, minus the base address of the file image.
- **IDT** (Import Directory Table) - is a data structure in a Portable Executable (PE) file that stores information about dynamic-link libraries (DLLs) that the file depends on and the functions that the file imports from those DLLs. 
- **ILT** - is a data structure in a Portable Executable (PE) file that stores the addresses of imported functions in the executable or library.
- **IAT** (Import Address Table) - can be the same with **ILT**, however when a file is being loaded into memory the loader will overwrite the addresses of the **IAT** with their new memory address locations.
- **DEP** (Data Execution Prevention) - is a security feature that is designed to prevent code from being executed in certain areas of memory where it is not supposed to be executed. [doc](https://learn.microsoft.com/en-us/windows/win32/memory/data-execution-prevention)
- **ASLR** (Address Space Layout Randomization) - is a security feature that randomizes the memory locations of certain parts of a program or operating system, making it more difficult for attackers to predict or control where certain code or data is located in memory. [wiki](https://en.wikipedia.org/wiki/Address_space_layout_randomization)

# Windows Portable Executable (PE)

An executable is a set of binary data that contains instructions for the operating system to execute when the program is loaded into memory. Let's examine how we can manually parse a Portable Executable (PE) file by reading and interpreting the bytes it contains. To do this, we must carefully review the binary data in the PE file and try to make sense of it.

> The term **image** refers to the contents of a file when it is loaded into memory. You will encounter this term frequently in the explanations below.

## DOS Header

The first 64 bytes of a binary file represent the DOS header, which is included for backwards compatibility and does not directly affect the functioning of the Portable Executable (PE). These 64 bytes contain information such as the number of pages in the file, the number of relocations, the checksum, OEM identifiers, and reserved words. The last 4 bytes of the DOS header, `e_lfanew`, contain the offset or address of the new PE header in modern Windows applications.

The first two bytes of an executable file, `4D 5A` which translates to `MZ` in ASCII, serve as an indicator that the file is an executable intended for use on a Windows operating system.

- [Why `4D 5A`?](http://4d5asecurity.com/why-4d5a)

## DOS Stub / Rich Header

Following the first 64 bytes is the DOS Stub, a small program that displays an error message on systems that are not compatible with MS-DOS. This is a legacy feature dating back to the early days of Windows, when the operating system was built on top of MS-DOS.

The Rich Header, on the other hand, is not a required or standard part of the Portable Executable (PE) file format. It contains metadata about the compiler or packer that was used to create the executable and may provide additional information about the file. The magic number for the Rich Header is `52 69 63 68`, which translates to `Rich` in ASCII.

The Rich Header information is encrypted using the XOR cipher, which can be easily decrypted using the 4 bytes immediately following the Rich ASCII which is the key. 

To decrypt the rest of the header, we must run the XOR decipher on the file and unmask the value `44 61 6E 53`, which translates to "DanS" in ASCII. This marks the beginning of the Rich Header, which is then followed by 3 `0s` after deciphering. 

With this information, we can determine the start and end of the Rich Header and parse it accordingly.

The header can contain data about:
- Compiler and build environment information
- Timestamps
- Checksums
- Other metadata

The Rich Header is a very interesting topic that I would like to write more about, until then you can read the following articles.

- [VB2019 paper: Rich Headers: leveraging this mysterious artifact of the PE format](https://www.virusbulletin.com/virusbulletin/2020/01/vb2019-paper-rich-headers-leveraging-mysterious-artifact-pe-format/)
- [The devil’s in the Rich header](https://securelist.com/the-devils-in-the-rich-header/84348/)


## NT Headers (New Technology)

If we follow the offset indicated in the last two bytes of the DOS header, we will reach the new PE headers (also known as NT headers). These headers are identified by the 4-byte magic number `50 45 00 00`, which translates to `PE..` in ASCII. This magic number is used to distinguish the PE headers from other types of headers.

The structure of the `_IMAGE_NT_HEADERS64`:

```cpp
typedef struct _IMAGE_NT_HEADERS64 {
    DWORD Signature;
    IMAGE_FILE_HEADER FileHeader;
    IMAGE_OPTIONAL_HEADER64 OptionalHeader;
} IMAGE_NT_HEADERS64, *PIMAGE_NT_HEADERS64;
```

The structure of `_IMAGE_FILE_HEADER`:

```cpp
typedef struct _IMAGE_FILE_HEADER {
    WORD  Machine; // Predefined value [IMAGE_FILE_MACHINE_I386 or IMAGE_FILE_MACHINE_AMD64]
    WORD  NumberOfSections; 
    DWORD TimeDateStamp; // Timestamp of which the executable was compiled or linked
    DWORD PointerToSymbolTable; // The offset to the COFF Symbol Table
    DWORD NumberOfSymbols; // The number of symbols in the COFF Header
    WORD  SizeOfOptionalHeader;
    WORD  Characteristics; // https://learn.microsoft.com/en-us/windows/win32/debug/pe-format#characteristics
} IMAGE_FILE_HEADER, *PIMAGE_FILE_HEADER;
```

- [What is COFF?](https://en.wikipedia.org/wiki/COFF)

The structure of `_IMAGE_OPTIONAL_HEADER`, this structure is "optional" but in fact most of the PE files contains this header.

```cpp
typedef struct _IMAGE_OPTIONAL_HEADER {
  WORD                 Magic; 
  BYTE                 MajorLinkerVersion;
  BYTE                 MinorLinkerVersion;
  DWORD                SizeOfCode; // .text section size
  DWORD                SizeOfInitializedData; // .data section size
  DWORD                SizeOfUninitializedData; // .bss section size 
  DWORD                AddressOfEntryPoint; // 0 if a DLL because its optional otherwise it indicates the RVA (Relative Virtual Address) it is used to determine the address of elements within the file (strings, icons etc.)
  DWORD                BaseOfCode; // The RVA is the base address of the code section loaded in memory
  DWORD                BaseOfData; // The RVA for the base address of the data section
  DWORD                ImageBase; // This indicates the prefered address at which the file is intended to be loaded in memory, almost never used address instead the PE Loader looks for unused memory space to load the image.
  DWORD                SectionAlignment; // Sections are aligned in memory boundaries that are multiples of this value
  DWORD                FileAlignment; // Raw data alignment on disk
  WORD                 MajorOperatingSystemVersion; 
  WORD                 MinorOperatingSystemVersion; 
  WORD                 MajorImageVersion; 
  WORD                 MinorImageVersion; 
  WORD                 MajorSubsystemVersion; 
  WORD                 MinorSubsystemVersion; 
  DWORD                Win32VersionValue; // Reserved (for future use) must be 0, ensures that the file is compatible with the current system
  DWORD                SizeOfImage; // It gets rounded to a multiple of `SectionAlignment`
  DWORD                SizeOfHeaders; // Sum(DOS Stub, NT Headers, Section Headers)
  DWORD                CheckSum; // Checksum of the Image
  WORD                 Subsystem; // Refer to documentation for this one
  WORD                 DllCharacteristics; // Refer to documentation for this one
  DWORD                SizeOfStackReserve;
  DWORD                SizeOfStackCommit;
  DWORD                SizeOfHeapReserve;
  DWORD                SizeOfHeapCommit;
  DWORD                LoaderFlags; // Obsolete refering to documentation, 0
  DWORD                NumberOfRvaAndSizes; // Size of DataDirectory below
  IMAGE_DATA_DIRECTORY DataDirectory[IMAGE_NUMBEROF_DIRECTORY_ENTRIES]; // This contains the addresses of the Export/Import Directories, the Base Relocation table and so on. It is a constant of `16`.
} IMAGE_OPTIONAL_HEADER32, *PIMAGE_OPTIONAL_HEADER32;
```

I've written some quick comments on each of the fields however since that struct is lengthy and well documented you can check the [fields here](https://learn.microsoft.com/en-us/windows/win32/api/winnt/ns-winnt-image_optional_header32) as well.

Here is the the list of Data Directories entries:

```cpp
#define IMAGE_DIRECTORY_ENTRY_EXPORT          0   // Export Directory
#define IMAGE_DIRECTORY_ENTRY_IMPORT          1   // Import Directory
#define IMAGE_DIRECTORY_ENTRY_RESOURCE        2   // Resource Directory
#define IMAGE_DIRECTORY_ENTRY_EXCEPTION       3   // Exception Directory
#define IMAGE_DIRECTORY_ENTRY_SECURITY        4   // Security Directory
#define IMAGE_DIRECTORY_ENTRY_BASERELOC       5   // Base Relocation Table
#define IMAGE_DIRECTORY_ENTRY_DEBUG           6   // Debug Directory
//      IMAGE_DIRECTORY_ENTRY_COPYRIGHT       7   // (X86 usage)
#define IMAGE_DIRECTORY_ENTRY_ARCHITECTURE    7   // Architecture Specific Data
#define IMAGE_DIRECTORY_ENTRY_GLOBALPTR       8   // RVA of GP
#define IMAGE_DIRECTORY_ENTRY_TLS             9   // TLS Directory
#define IMAGE_DIRECTORY_ENTRY_LOAD_CONFIG    10   // Load Configuration Directory
#define IMAGE_DIRECTORY_ENTRY_BOUND_IMPORT   11   // Bound Import Directory in headers
#define IMAGE_DIRECTORY_ENTRY_IAT            12   // Import Address Table
#define IMAGE_DIRECTORY_ENTRY_DELAY_IMPORT   13   // Delay Load Import Descriptors
#define IMAGE_DIRECTORY_ENTRY_COM_DESCRIPTOR 14   // COM Runtime descriptor
```

## Sections Headers

The section headers are stored in the NT Headers. And the structure of the `IMAGE_SECTION_HEADER` looks like this:

```cpp
typedef struct _IMAGE_SECTION_HEADER {
  BYTE  Name[IMAGE_SIZEOF_SHORT_NAME];
  union {
    DWORD PhysicalAddress;
    DWORD VirtualSize;
  } Misc;
  DWORD VirtualAddress;
  DWORD SizeOfRawData;
  DWORD PointerToRawData;
  DWORD PointerToRelocations;
  DWORD PointerToLinenumbers;
  WORD  NumberOfRelocations;
  WORD  NumberOfLinenumbers;
  DWORD Characteristics;
} IMAGE_SECTION_HEADER, *PIMAGE_SECTION_HEADER;
```

- [Source and Documentation](https://learn.microsoft.com/en-us/windows/win32/api/winnt/ns-winnt-image_section_header)
- [PE Format](https://learn.microsoft.com/en-us/windows/win32/debug/pe-format#section-table-section-headers)

The sections of a Portable Executable (PE) file contain various types of data, such as code, data, resources, and other information. The headers of the file are used to specify the characteristics of these sections, such as whether they contain executable code, initialized data, uninitialized data, or other types of information.


> **Tip**: You can detect if a PE file has been packed by comparing the values of the `VirtualSize` and `SizeOfRawData` fields in the headers. If the `VirtualSize` is significantly larger than the `SizeOfRawData`, it is a strong indication that the file has been packed. However, it is worth noting that there may be some discrepancy between the two values due to section padding and alignment.

## Sections

Sections are where the actual data of the file is. There are [Special Sections](https://learn.microsoft.com/en-us/windows/win32/debug/pe-format#special-sections) as well but we will focus only on the reserved sections such as:
- .bss - Uninitialized data (free format)
- .data - Initialized data (free format)
- .cormeta - CLR metadata that indicates that the object file contains managed code
- .debug (following with)
	- $F - Generated FPO [Frame Poiner Omission](http://www.nynaeve.net/?p=91) debug information (obsolete)
	- $P - Precompiled debug types (object only)
	- $S - Debug symbols (object only)
	- $T - Debug types (object only)
- .drective - Linker Options
- .edata/.idata - Export/Import Tables
- .idlsym - Includes registered SEH (image only) to support IDL attributes. Often used in conjuction with FPO [ref](https://learn.microsoft.com/en-us/windows/win32/debug/pe-format#references)
- .pdata - Exception information
- .rdata - Read-only initialized data
- .reloc - Relocations of the Image 
- .rsrc - Resource Directory
- .s(following with) - Global Pointer-relative
	- .sbss - uninitialized data
	- .sdata -  initialized data 
	- .srdata - read-only data
	- .sxdata - Registered exception handler data (free format and x86/object only)
	- .vsdata - initialized data (free format and for ARM, SH4, and Thumb architectures only)
- .text - Executable code (free format)
- .tls/.tls$ - Thread-local storage (object only)
- .xdata - Exception information (free format)

Refer to the [documentation](https://learn.microsoft.com/en-us/windows/win32/debug/pe-format#special-sections) for further explanation. Each section is explained very well there.

## Import Directory Table (IDT)

The Import Directory Table (**IDT**) stores information about dynamic-link libraries (DLLs) that a Portable Executable (PE) file depends on and the functions that the file imports from those DLLs. In most cases, this information is stored in the `.idata` section of the PE file, which is dedicated to this purpose. However, in some cases, the **IDT** may be stored elsewhere.

The address of the IDT can be found in the `IMAGE_DATA_DIRECTORY` array of the `_IMAGE_OPTIONAL_HEADER` structure. It is the second entry in the array. Each entry in the IDT is 8 bytes in size, with the first 4 bytes representing the address of the entry and the second 4 bytes representing the size. This information is used by the operating system's dynamic linker to resolve the addresses of the imported functions and link them to the actual functions in the imported DLLs.

Let's take a look at an example:

```text
CC280000 
	The IDT is located at 0xCC28
A0000000
	The size is 160 (A0)
```

Following the address of the Import Directory we reach the first import located at `0xCC28`, let's see what is located at that address. 

Each Import is defined by 24 bytes, given these 24 bytes values:

```text
F8290000
	OriginalFirstThunk
00000000
	Timestamp
00000000
	Forwarder Chain (Address)
C02A0000
	Name of the Import (RVA)
D8210000
	FirstThunk
```

- [OriginalFirstThunk/FirstThunk](https://stackoverflow.com/questions/42413937/why-pe-need-original-first-thunkoft)

To find out which functions are imported by a particular import in a Portable Executable (PE) file, we can follow the `OriginalFirstThunk` address at `0xF829`, which leads us to the Import Lookup Table (ILT). The ILT is a sequence of bytes that represents the addresses of the imported functions, similar to an array or table.

> **Note**: It's important to note that the Import Address Table (IAT) may be the same as the ILT. However, when a file is loaded, the loader will overwrite the addresses in the IAT with the new memory addresses of the imported functions.

Each function address in the ILT is 8 bytes in length, so the resulting data should look something like this:

```text
FC2A0000
    This is the address of the imported function
00000000

at 0xFC2A ->

B001
	Ordinal/Name Import Flag
5368656C6C4578656375746557
	ASCII -> 'ShellExecuteW'
00
	Null char terminating the string
```

With this we can denote and 'parse' all the imports and respectively their imported functions. 

## Resources

To locate the resources in a Portable Executable (PE) file, you can use the third entry in the `IMAGE_DATA_DIRECTORY` array of the `IMAGE_OPTIONAL_HEADER` structure. This entry contains the address and size of the resources section in the file.

```text
00000000 
	Characteristics
00000000
	TimeDateStamp
0000
	Major Version
0000
	Minor Version
0000
	Number of Named entities
0400
	Number of ID entities
```

And the corresponding struct

```cpp
typedef struct _IMAGE_RESOURCE_DIRECTORY {
     DWORD   Characteristics;
     DWORD   TimeDateStamp;
     WORD    MajorVersion;
     WORD    MinorVersion;
     WORD    NumberOfNamedEntries;
     WORD    NumberOfIdEntries;
    IMAGE_RESOURCE_DIRECTORY_ENTRY DirectoryEntries[];
 }
```

Now let's take a look at the entries `IMAGE_RESOURCE_DIRECTORY_ENTRY`

```cpp
typedef struct _IMAGE_RESOURCE_DIRECTORY_ENTRY {
  union {
    struct {
      DWORD NameOffset:31;
      DWORD NameIsString:1;
    } DUMMYSTRUCTNAME;
    DWORD   Name;
    WORD    Id;
  } DUMMYUNIONNAME;
  union {
    DWORD   OffsetToData; // Leads us to the resource directory 
    struct {
      DWORD   OffsetToDirectory:31;
      DWORD   DataIsDirectory:1;
    } DUMMYSTRUCTNAME2;
  } DUMMYUNIONNAME2;
} IMAGE_RESOURCE_DIRECTORY_ENTRY, *PIMAGE_RESOURCE_DIRECTORY_ENTRY;
```

The user `mmn3mm` has written a pretty good explanation of how to parse this section [here](https://github.com/mmn3mm/peresources).

## Exception Directory

The Exception Directory is a section in a Portable Executable (PE) file that contains information about the exception handling functions in the code. It includes the addresses of the exception handling functions, the types of exceptions they handle, and other relevant details.

When an exception occurs, the operating system's exception handling mechanism uses the Exception Directory to find the appropriate exception handling function. This section is optional and may not be present in every PE file, depending on whether the code in the file uses exception handling.

It is typically located at `.pdata` section, and the offset to the Exception section is the 4th entry in the `IMAGE_DATA_DIRECTORY` array.

> **Personal Note**: As far as I understood that section (I could be wrong here) it contains exception handlers that are being used throughout the execution and they execute only if the execution is within the specified `BeginAddress` and `EndAddress`.

The entries there are 12 bytes, first 4 bytes contains the `BeginAddress` the next 4 bytes contain the `EndAddress` and the last 4 bytes contains the address (`UnwindInfoAddress`) for the **Unwind Information Block** which contains information of how to unwind the stack whenever an exception occurs.

## Base Relocations

When a program is compiled, the compiler saves a value into the `IMAGE_OPTIONAL_HEADER.ImageBase` field, which specifies the desired memory location where the program is intended to be executed. However, this memory location is often already occupied by other programs, so the actual memory location used by the program may be different. In this case, the loader will recalculate the `ImageBase` value and write the new value into the program's image. This will cause all addresses in the program that are offset by the `ImageBase` value (essentially, all addresses in the program) to be recalculated with the new ImageBase value and stored in the `.reloc` section of the image. This process is necessary to ensure that the program can run correctly at its actual memory location.

The user `0xRick` has written a [very good article](https://0xrick.github.io/win-internals/pe7/) of how to calcuate the entries within the Relocation Block and more.

## Debug

[Microsoft Documentation](https://learn.microsoft.com/en-us/windows/win32/debug/pe-format#debug-directory-image-only)

The Debug section is the 7th entry of the `IMAGE_DATA_DIRECTORY` array, its structure looks like this:

```cpp
typedef struct _IMAGE_DEBUG_DIRECTORY {
    DWORD   Characteristics; // Describing the debug info
    DWORD   TimeDateStamp;
    WORD    MajorVersion; // Version of the debugging tool
    WORD    MinorVersion; // Version of the debugging tool
    DWORD   Type; // Type of Debugging (this will denote the format that you need to parse)
    DWORD   SizeOfData; // The size of the debug data (not including the debug directory itself)
    DWORD   AddressOfRawData; // The address of the debug data when loaded, relative to the image base
    DWORD   PointerToRawData; // The file pointer to the debug data.
} IMAGE_DEBUG_DIRECTORY, *PIMAGE_DEBUG_DIRECTORY;
```

Refer to the [Microsoft's Documentation](https://learn.microsoft.com/en-us/windows/win32/debug/pe-format#debug-type) about how to parse further debug information.

## Load Config

This section contains information about the dynamic linking and loading of the executable or library and it is the 11th entry of the `IMAGE_DATA_DIRECTORY` array. The Load Config section typically includes information such as the address of the entry point of the program, the size of the stack and heap, and the addresses of any imported functions or data. 

It can also include security and integrity-related information, such as Data Execution Prevention (**DEP**) and Address Space Layout Randomization (**ASLR**) settings.

It is typically located at `.rdata` section and it is an optional section for a PE file.

The structure follows:

```cpp
typedef struct _IMAGE_LOAD_CONFIG_DIRECTORY {
    DWORD   Size;
    DWORD   TimeDateStamp;
    WORD    MajorVersion;
    WORD    MinorVersion;
    DWORD   GlobalFlagsClear;
    DWORD   GlobalFlagsSet;
    DWORD   CriticalSectionDefaultTimeout;
    DWORD   DeCommitFreeBlockThreshold;
    DWORD   DeCommitTotalFreeThreshold;
    PVOID   LockPrefixTable;
    DWORD   MaximumAllocationSize;
    DWORD   VirtualMemoryThreshold;
    DWORD   ProcessAffinityMask;
    DWORD   ProcessHeapFlags;
    WORD    CSDVersion;
    WORD    DependentLoadFlags;
    PVOID   EditList;
    PVOID   SecurityCookie;
    PVOID   SEHandlerTable;
    DWORD   SEHandlerCount;
    PVOID   GuardCFCheckFunctionPointer;
    PVOID   GuardCFDispatchFunctionPointer;
    PVOID   GuardCFFunctionTable;
    DWORD   GuardCFFunctionCount;
    DWORD   GuardFlags;
} IMAGE_LOAD_CONFIG_DIRECTORY, *PIMAGE_LOAD_CONFIG_DIRECTORY;
```

## Access Rights of the Sections

The section rights are presented in the `DWORD Characteristics;` field of the `_IMAGE_SECTION_HEADER `, you can check the valid values in the [microsoft's documentation](https://learn.microsoft.com/en-us/windows/win32/api/winnt/ns-winnt-image_section_header?redirectedfrom=MSDN#members).

Those are the standard access rights of PE.

| Section Name | Access Rights |
|--- |--- |
| `.text` | Read and Execute |
| `.rdata` | Read-Only |
| `.data` | Read and Write |
| `.bss` | Read and Write |
| `.rsrc` | Read Only |
| `.reloc` | Read Only |

> Note: Seungwon Lee has indicated that if an essential element of an executable is the WRITE property of a section, the PE could be packed.

# References
- https://sy1.sh/post/2023/01/06/static-analysis-research-p1.html
- https://chat.openai.com/
- https://github.com/mandiant/flare-floss
- https://www.mandiant.com/resources/blog/automatically-extracting-obfuscated-strings
- https://stackoverflow.com/questions/36550038/in-utf-16-utf-16be-utf-16le-is-the-endian-of-utf-16-the-computers-endianness
- https://0xrick.github.io/
- https://securelist.com/the-devils-in-the-rich-header/84348/
- https://www.virusbulletin.com/virusbulletin/2020/01/vb2019-paper-rich-headers-leveraging-mysterious-artifact-pe-format/
- https://forensicitguy.github.io/rich-header-hashes-with-pefile/
- https://github.com/mmn3mm/peresources
- The Study of Evasion of Packed PE from Static Detection (Mirza Baig, Pavol Zavarsky, Ron Ruhl, Dale Lindskog)
- Han, Seungwon Lee, Keungi Lee, Sangjin, “Packed PE File Detection for Malware Forensics”, Computer Science and its Applications, 2nd International Conference, http://ieeexplore.ieee.org/stamp/stamp.jsp?arn umber=05404211, 12 Dec 2009