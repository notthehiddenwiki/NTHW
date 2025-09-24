#  Metadata for newbies

**Author**: 50sec<br>
*"Get Job at Cybersec or die tryin"*

Github: https://github.com/50sec


# 💾 Metadata - what's that?

Metadata might be a familiar concept to those interested in cybersecurity, but for many, it's still unknown topic. Long story short, metadata refers to hidden information embedded in files such as images, documents, or videos.

When it comes to photos (like JPEGs), your device saves additional data alongside the actual image, known as EXIF tags. These can be read by image viewers, editors, or analysis tools. Importantly, this data often stays in the file even after it's uploaded to the cloud or sent by email — unless the platform removes it (which not all do).

## 🟦 Common types of Metadata:
- EXIF — Mostly found in images: includes timestamp, device model, camera settings, and sometimes GPS coordinates.

- IPTC / XMP — Extended image metadata: titles, captions, author info, tags.

- Document metadata — Word or PDF files often include author name, edit history, comments, file paths, etc.

- Communication/network metadata — Email headers, server logs, GPS data from trackers, etc.

# 🟦 Case Study: Tracking Someone Using EXIF Metadata
**John McAfee & the Photo with GPS Data**

You may have heard of John McAfee, the founder of the McAfee antivirus company. In 2012, while he was on the run, VICE published a photo of him. Unfortunately, that photo included EXIF metadata with GPS coordinates, revealing his exact location. After the issue was exposed, VICE removed the data, but the damage was already done.

Publicly shared photo + GPS data = exposed location

**Facebook’s EXIF Scandal (2012)**

Researchers found that, in the past, Facebook photos retained EXIF metadata, including GPS coordinates. Many users unknowingly exposed their home, workplace, or school locations. After the issue made headlines, Facebook implemented automatic metadata stripping on uploads.


# 🟦  How to Check or Remove Metadata — Example tools
📱 **For Regular Users:**

- Disable geotagging in your camera settings (Android/iOS → camera → location permissions). This is the most important step.

- Before sharing a photo, use the "remove metadata" option if available (some galleries and apps offer this).

- Messaging apps: some apps like WhatsApp remove metadata through compression, but not all do. Don’t rely on this blindly.

🛠️ **For Advanced Users:**

- ExifTool (command line) — A most popular, powerful tool for viewing, editing, and deleting metadata from many file types.

- MAT2 (Metadata Anonymisation Toolkit 2) — A privacy-focused tool (GUI/CLI) to strip metadata from images, documents, torrents, etc.

- Image editors (e.g., GIMP, Photoshop) — often let you export images without metadata.

- On Windows: right-click file → Properties → Details → Remove properties and personal information.


# 🟦 How to view & remove metadata from image via EXIFTOOL

You can download Exiftool from here:  https://exiftool.org/

I'm gonna show this on Kali Linux, but this software works on windows and mac as well

On Kali exiftool is pre-installed, so you don't need to install it.

**🟩 Viewing metadata:**

to view metadata of .jpg file, just type: 

```exiftool filename.jpg```

<img src="https://raw.githubusercontent.com/notthehiddenwiki/NTHW/nthw/.github/notes/HTSW/metadata_for_newbies/exiftool_view.png">

this command views many of metadatas for example gps data:

<img src="https://raw.githubusercontent.com/notthehiddenwiki/NTHW/nthw/.github/notes/HTSW/metadata_for_newbies/exiftool_gps.png">

**🟥 Removing metadata:**

to remove metadata, just type:

```exiftool -all= filename.jpg``` <br>

<img src="https://raw.githubusercontent.com/notthehiddenwiki/NTHW/nthw/.github/notes/HTSW/metadata_for_newbies/exiftool_remove.png">

NOTE: This command leaves a backup of your original file called filename.jpg_original
<br>This is the simplest command but if you wanna make sure that everything will be as you want, or you want exiftool to overwrite file automatically, you can use different commands, all of them you can find on official exiftool website.

# Conclusion

Metadata is invisible to the eye, but it can reveal a surprising amount — location, time, device used, and more. Understanding how it works and taking precautions is crucial if you care about your digital privacy, especially when sharing photos online.

<img src="https://raw.githubusercontent.com/notthehiddenwiki/NTHW/nthw/.github/notes/HTSW/metadata_for_newbies/metadatameme.jpg">
