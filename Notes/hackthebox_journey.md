# HackTheBox has been PWNED!

**Author**: Michał "miblak" Błaszczak

- [LinkedIn](https://www.linkedin.com/in/michal-blaszczak/)
- [HTB Profile](https://app.hackthebox.com/profile/1246594)

<p align="center">
  <img src="https://raw.githubusercontent.com/notthehiddenwiki/NTHW/nthw/.github/notes/hackthebox/htb_banner.png">
</p>

..**two years later I completed the Hack The Box platform 100%**. I could start the article below with these words. However, before this happened, I had to go through my CTF path. What did she look like? Was anyone helping me? You will find this and other information in the article with, in my opinion, the perfect name: **"HackTheBox has been PWNED!"**

## Beggining

The history of cybersecurity dates back to around 2009. because then I started reading the first books and browsing forums related to cybersecurity. It was also then that I learned my first programming language, C++. From the second half of 2012, I had Backtrack 5 R3 installed on my laptop, which was my first "hacker" operating system - for the uninitiated, Backtrack was the predecessor of today’s Kali Linux. Perhaps the fact that it was my first system adapted for offensive operations is why I use Kali Linux to this day. Of course, I also use other distributions such as Whonix, Debian, and Ubuntu, but as I  mentioned, I use Kali for offensive tests.

So, until around 2021, before I started my adventure with CTFs, I already had some experience in various areas of cybersecurity, especially since as a young person I was interested in multiple areas of cybersecurity, which resulted in at least basic knowledge on many topics ranging from programming, through reverse engineering, cryptography to knowledge from hacking web applications or forensics. Why am I remembering 2021? Because then I joined the discord of the first ever CTF team called **Unicorns of Security**, led by [Lasq](https://www.linkedin.com/in/lukasz-lamparski/) and it was thanks to this team I started my adventure with CTF. This decision also pushed me, a little over a year later, to begin my adventure on the Hack The Box platform.

But what exactly are CTFs and why did I choose the Hack The Box platform and not another one? I  will try to answer these questions later in the article.

And if you don't know where to start, you can watch a video on YouTube titled: [The MOST IMPORTANT advice for young hackers](https://www.youtube.com/watch?v=0Ejj2aBG5c8) which in my opinion is a good starting video.

### What are CTFs?

For the majority of people reading this article, the acronym CTF should not be a problem. However, if you don't know what CTFs are, let me explain. CTF or **C**apture **T**he **F**lag is largely a team tournament during which teams try to solve as many tasks as possible from categories related to security/hacking, such as web (security web applications), pwn (low-level exploitation/security of native applications), RE (crackme / general reverse engineering), crypto (cryptanalysis), forensics (forensics), stegano (steganography), ppc/programming (programming/algorithms). Of course, instead of large tournaments, the entire game can be "wrapped" in a platform that from time to time releases new challenges/machines that we have to face.

Without a doubt, CTFs force the player to constantly develop, learn, look for solutions, learn unknown tools/protocols, etc. Due to the need to have extensive knowledge in various fields, playing alone can cause many problems, which is why many people set up their own teams, thanks to which the entire competition becomes easier on the one hand, and on the other, more fierce.

CTFs can be summarized as a place to verify whether we can use our knowledge to find an often unusual solution.

### Hack The Box Platform

There are many platforms related to CTFs, so why did I choose Hack The Box? You could say that Hack The Box chose me... Before I started my adventure with this platform, I made various hackme / crackme or just CTFs on platforms similar to Hack The Box, such as Try Hack Me. When I did "most" of them, I decided to switch to something new. Back then, Hack The Box was famous for being a platform that had no low entry level and to solve even easy machines you had to already know something. An additional interesting element was that in order to register on the platform, it had to be hacked. This made it a kind of platform that was not available to everyone. I think it was a simple challenge to get an invite code - the registration there can be seen below - it made me want to try my hand at this platform.

<p align="center">
  <img src="https://raw.githubusercontent.com/notthehiddenwiki/NTHW/nthw/.github/notes/hackthebox/htb_invite.png">
</p>

Despite initially various problems with the platform, after the third attempt at the platform I managed to stay on it a little longer and, as it turned out, two years later it led me to personal success.

If someone asked me now: "Miblak, is it worth starting the adventure with Hack The Box?" I would say it's worth it! Even though it is a "terrible time waster", it is a platform worth your time that can teach many things and can also irritate even the best players.

A new person who is just starting their adventure with this platform may be a bit confused by the number of options available in the main panel. Since I initially had problems understanding how it all works, I decided to make a small description below of what can be found on the platform (if you already play on Hack The Box, you can skip this part and go to the next point)

After logging in to [Hack The Box](https://app.hackthebox.com), a panel will appear that will look like this:

<p align="center">
  <img src="https://raw.githubusercontent.com/notthehiddenwiki/NTHW/nthw/.github/notes/hackthebox/htb_panel.png">
</p>

On the left sidebar there are several options that may be too much for a beginner to handle, but below you will find explanations of these options:

- **Starting Point:** Here you will find probably the simplest machines on the entire platform, which are intended to introduce you to the world of Hack The Box and help you understand what you need to do with machines, as well as show you a certain way of thinking.

- **Season 5:** Beginning of 2023 "Seasons" have been added to Hack The Box. This is a set of 13 machines of various levels of difficulty that we need to complete in a maximum of a week to receive points that will count toward the ranking. Importantly, the solution time is also important to be higher in the ranking. At the time of writing this article, Season 5 is slowly coming to an end on Hack The Box. 

- **Machines:** This is one of the main places on Hack The Box. Here you will find various machines with various vulnerabilities that are based on systems such as Windows, Linux, OpenBSD, FreeBSD, Android, and Solaris. Your only task is to capture 2 flags. The first is the **user.txt** flag, which is usually located in the directory of one of the users with "normal" permissions. The second flag, **root.txt**, is available only after gaining administrator/root privileges. The attack vector could be a web application, Active Directory, or anything else. In fact, the only limitation is the imagination of the creators of these machines, which you can also join!

- **Challanges:** Maybe you're not interested in Active Directory hacking, don't like privilege escalation, and aren't comfortable attacking entire machines/networks. Nothing is lost! On Hack The Box you will find challenges sorted into different categories. So if you only want to look for vulnerabilities in web applications, you can select the appropriate category and enjoy tasks strictly related to, for example, hacking web applications. I have briefly described the available categories below:
  - **Crypto:** Revolving around cryptographic functions, this category will have you decrypting objects that were locked away from the prying eye with up-to-date cryptological processes.
  - **Forensics:** Revolving around data recovery and forensics, this category will require you to nitpick at small details in recovery data batches to try to get to the bottom of what happened. A keen eye and a lot of patience will help you go a long way as a forensic analyst. 
  - **Hardware:** Revolving around penetrating different hardware systems with your software, this category will have you analyzing different attack methodologies for objects we use every single day, even if we know it or not.
  - **Misc:** Miscellaneous Challenges that don't strictly fit into any other given category. Variety is key here but also the source of all the fun solving them.
  - **Mobile:** Revolving around multiple types of handheld devices, this category will have you scrolling on social media to like our posts and analyzing the intrinsics of different mobile applications to find the hidden embedded functionalities and flags.
  - **OSINT:** Revolving around publicly available data farming, this category will teach you how to laterally move between search engines' pesky algorithms to try to find the missing piece of the puzzle.
  - **PWN:** Revolving around binary exploitation and memory corruption, this category will have you creating exploits that'll make anyone lose their bits. 
  - **Reversing:** Revolving around the art of reverse-engineering, this category will have you using reversing tools to find out what a certain script or program does to find the flag.
  - **Web:** Revolving around web-based applications, this category will require you to detect, exploit and search through different vulnerable web applications. The themes of these Challenges are very intriguing.

- **Sherlocks:** For a very long time, the Hack The Box platform was associated only with a platform for people interested in offensive aspects of security. It was... For some time now we can find the Sherlocks tab here, where we will be able to analyze various logs, malware samples, and more. In one word - a paradise for people involved in defense.

- **Tracks:** As the name suggests, these are paths created based on machines and challenges that are available in the Machines / Challenges tabs. This is a nice place because you don't have to search everything to find the right machines related to, for example, deserialization or printer hacking.

- **Fortresses / Endgames / Pro Labs:** If you are bored with single machines/challenges, these tabs are for you. Here you will find networks with at least several different machines with different systems and vulnerabilities. These are real scenarios during which you will be transferred to real environments where finding vulnerabilities is not everything. You will need to use C2, malware writing, and in-depth knowledge of various topics.

I think it is worth adding at this point that practically all of the above tabs and what you will find in them are divided into **Active** and **Retired**. This means that if something is Active, it is available to everyone for free. If, for example, a new challenge is released, one of the previous challenges becomes Retired. To solve issues marked as retired, we must have at least a VIP account.

The exception are Pro Labs. In their case, we purchase separate access to solve them. In my opinion, it is worth spending the extra money to try your hand at these huge networks full of vulnerable machines and various kill-chains.

Now that we know what CTFs are and what the Hack The Box platform looks like. Let's take a look at my adventure or rather my experiences and memories from my adventure on Hack The Box.

## What was the Hack The Box adventure like?

<p align="center">
  <img src="https://raw.githubusercontent.com/notthehiddenwiki/NTHW/nthw/.github/notes/hackthebox/htb_climb.png">
</p>

I think it's worth starting with the fact that my achievement would not have happened (at least not at this pace) if it weren't for the people I met during my adventure and with whom I had the opportunity to play. I must emphasize here that it was thanks to the kindness of many people and the willingness to spend time explaining many things to me that I was able to complete the entire Hack The Box. A large piece of this "pie" is teamwork when solving fortresses, machines, or challenges. For 2 years in total, I was part of 3 teams: my own team which no longer exists. Then I played with 7h3B14ckKn1gh75, and eventually moved to APT44 with whom I played until almost the end of the Hack The Box adventure.

Over two years, I have benefited from the support of many great people, but also from write-ups regarding challenges that were retired (i.e. their points did not count towards the ranking). I think that, especially among Hack The Box players, write-ups are somewhat of a taboo topic. That's why I wanted to present my point of view on writeups below. I believe that we need to be able to use writeups and we should use them differently depending on what stage we are at. I have presented three such situations below:

1. **I'm a beginner:** If we are starting our adventure with CTFs, especially the first machines/challenges may be problematic for us, for example, because of the requirement for specific thinking that we have to get used to. Therefore, if you are a beginner and want to start your adventure with CTFs, you can enable writeup on one screen and perform a given challenge on the other. It is important to do it step by step without copying the command etc (you need to rewrite all commands). If we only copy, we will not learn much. Scrolling the writeup directly to the solution will not bring us any closer to development. Thanks to this use of writeups, we will learn how they work, the methodology, and many different tools. Remember that if a concept is new to you, it is worth reading about it a little deeper, for example using Google.

<br>

2. **I'm intermediate:** After some time, we should gain enough experience to pwn at least half of the machine ourselves. In such a case, we only look at the writeup when we are stuck in a given place for a long time and do not know which direction to go. If we pass a problematic moment, we continue without writeup until we get stuck again. If you can't do anything without writeup, go back to point 1. 

<br>

3. **I'm advanced:** I have the impression that for people who consider themselves very experienced, using writeup is like a crime. Fortunately, I do not consider myself such a person, so I will present my point of view on the use of writeups by experienced people. I think the key thing here is to say why exactly should such a person use a writeup. Certainly not to do a challenge/machine! In my opinion, writeups for advanced people are a very interesting read that shows different approaches depending on the person who created the writeup. Additionally, such materials often contain information about paths that were not planned by the creators of the given challenges. Very often it may turn out that instead of escalating privileges by 2 users, we could get to root directly from www-data (on the one hand it is very irritating, but on the other hand it is fascinating that someone found such a possibility). If we think about it, I think that every person, regardless of their level of advancement, should also use writeups in this way. In addition to learning about different paths, we will also see a lot of custom scripts and more. That's why such write-ups are a treasure trove of knowledge.

If you have a different opinion about writeups, let me know! I will be happy to read about it and update the article with your observations!

During my adventure, I encountered machines/challenges that gave me particular problems or were very irritating to me. I think that each of us can replace such machines. I remember how we spent a few hours working on one challenge and it turned out that someone forgot to give the appropriate permissions to the directory, so we were able to simply download the file with the database in which the flag was located without any exploits. In another challenge from the web category (in which the source code was not included), we had to perform a parameter pollution attack, but the trick was that one of the parameters had to have an appropriate numerical value, which led many people to say that this was not the path they needed to follow to get flag because the numerical value was not appropriate. Among the machines that definitely caused me difficulties, I could mention RopeTwo, in which we had to write complicated exploits from the very beginning.

Hack The Box itself or any other platform related to CTFs forces us to constantly learn (I believe that this is a certain condition that we agree to when entering cybersecurity). For many people, this may be a problem if we have to learn quite exotic problems and solutions for various areas of knowledge. Here I will come back to the fact that CTFs are teamwork and I don't know anyone who would be an expert in all areas. This is because we need to constantly develop in our favorite areas and additionally learn how to work as a team. Thanks to this, you can work wonders at CTF events. And if we manage to get through all these tasks, we will certainly gain quite valuable and extensive knowledge and we will learn to look at problems from a broader perspective (especially unusual ones).
 
Anyway, the adventure with Hack The Box was very bumpy, it made me very angry more than once. However, with each new machine, I became more and more addicted to gaining more points on my way to completing everything. I think it was definitely worth it.

After two long years, I completed the Hack The Box platform 100%, which resulted in:

* 391/391 Machines
* 613/613 Challenges
* 40/40 Sherlocks
* 6/6 Fortress
* 8/8 Endgames
* 6/6 ProLabs

<p align="center">
  <img src="https://raw.githubusercontent.com/notthehiddenwiki/NTHW/nthw/.github/notes/hackthebox/htb_stats.png">
</p>

Which resulting in **~2100 flags** (including single anwsers in Sherlock as a flag)


> It [HTB] boosts your knowledge and career to evolve and play amongst people who have the same passion and drive for cybersecurity and hacking in general. When you are in a team or community like that it generates the "flow experience". 
>
> \- **Django88**


## LinkedIn Questions

After I published information on LinkedIn that I was the only person who had managed to complete Hack The Box in its entirety at the time of writing this article, many people, both in private messages and comments, asked many questions about my adventure. So I collected them below and added the answers.

**Q:** `miblak how do i exit vim?`<br>
**A:** Mamy tu tak naprawdę kilka możliwości:
1. Save and exit: If you want to save your changes and exit Vim, you can use the **:wq** command. This writes (saves) your changes to the file and then quits Vim.
2. Exit without saving: If you don’t want to save your changes and just want to exit Vim, you can use the **:q!** command. This will exit Vim without saving your changes, discarding any changes you made since the last time you saved.
3. Save and exit multiple files: If you have multiple files open in Vim and want to save and exit all of them at once, you can use the **:wqa** command. This will write and quit all open files. This is very unlikely to happen if you ended up in Vim unintentionally.

<br>

**Q:**`why such a challenge, and why were you so persistent in pursuing it? I guess the "learned things" part has a steep diminishing return curve, probably initially you learned a lot with each new challenge, but in the end, when solving some annoying esoteric challenges just to finish everything, have you learned so much?  Was the drive to finish just competitiveness and desire to be the first one to do it, or was it something else?`<br>
**A:** I don't think I had this challenge planned until halfway through my adventure. I started doing Hack The Box to try my hand at CTF because when I started playing on the platform, a lot of my friends were doing CTF and saying how cool it was. However, real events have never been my thing, so HTB was the perfect solution for me. Additionally, I think it is one of the best platforms to test your knowledge. Additionally, the variety of challenges forces us to look deeper for solutions to many problems. My first challenge on this platform (as for most players) was to achieve the Omniscient level, i.e. the level you get for completing all active challenges, machines, etc. By achieving this achievement, I was looking for a new "stimulus" and the challenge of completing the entire platform was something huge. Especially since no one has achieved this at the moment. Why did I do it? I can't explain, maybe I wanted to prove something to myself or it was simply an addiction to gaining experience (like in games). The end of this challenge was definitely very annoying. Especially when I reached the point where I had one task left and I couldn't solve it, and after some time Hack The Box published new challenges that had to be completed. At one point it was a Sisyphean job. However, I believe that despite numerous moments of irritation, the most important lesson on this platform was learning to look for a solution, learning humility, and learning to take a broader look at unusual problems (thoughts that are often unheard of in real life).

<br>

**Q:** `I am interested in learning about your routine and how you manage it alongside your day job. Have you encountered any situations that disrupted your routine? If so, how did you deal with them and get back on track?`<br>
**A:** I think that a very important factor in my success is the fact that I work in security every day. Thanks to this, I can improve my education and expand my knowledge and skills through pentests. I also have the convenience of working almost entirely remotely, which saves me time commuting to and from work (although it wasn't always like that). Practically the whole day I have a certain repetitive schedule which I stick to - my wife plays a very important role in this whole story, thanks to which I can pursue my cyber interests. She relieves me of many tasks and, as I wrote a moment ago, without her, it would not have been possible. I think that for sure something has disturbed my routine more than once, or I have disturbed it myself. I used to think that you could sit at the computer all day and it would be the best solution to develop as much as possible. However, the multitude of different things and even irritation with some challenges/machines led me to a high level of irritation. Leaving it all for a while and changing that routine helps a lot. However, I am one of those stubborn people and if I plan something, I will do it. So I think this personality trait of mine allowed me to come back to Hack The Box every time.

<br>

**Q:** `I'm curious about being burned out while getting through this journey and how did u deal with it.`<br>
**A:** A walk, a barbecue, time with the family. Any other activity than just hacking and learning is a very good solution in my opinion. I have been interested in cybersecurity for a good 10 years now and I haven't had a situation yet in which I've had enough of it (I hope it won't happen). Keep in mind the balance between normal life/health and cyber-related topics.   

<br>

**Q:** `What is a good path to learn (overall path to knowledge of security)`<br>
**A:** I believe that there is no one good path when it comes to learning cybersecurity. One of the main reasons is that there are many possible development paths and each one usually needs to be approached separately. Of course, many topics may overlap. At this point, if you asked me for advice, especially for a person starting their adventure with cybersecurity, I would say not to "speed up" your learning by skipping boring or "too simple" topics. I know well that we prefer to jump straight into interesting attacks and complicated issues, but without solid foundations, at some point, we will reach a place where we will have to go back anyway. So don't skip the "boring" knowledge! Additionally, learn to look for information, cybersecurity is one of those areas in which without our investigation we will never reach a higher level. If you stick to it, regardless of the path you choose, you will gain skills, experience, and knowledge.

<br>

**Q:** `How much money does it take to study?`<br>
**A:** When it comes to Hack The Box (as the main application - not the academy), you don't have to spend a penny because all the active content is available for free. As for my adventure that lasted two years and assuming that 3/4 of that time were retired machines/challenges, I spent +/- $400 on Hack The Box

<br>

**Q:** `What is the key to learning all of this, and how do you tackle a box or challenge when you're unfamiliar with the technology or field involved?`<br>
**A:** I believe that there is no universal key or golden advice. You just have to sit through each topic to understand it to some extent. I think it is crucial to be aware that we will not be experts in each of these areas, and very often your team, which has different experiences and which will sometimes push you forward so that you can later pull the rest with you, turns out to be beneficial. However, if you do not have such a team, it is important to be able to search for information and be persistent in it, because very often the answers to our problems are not on the first pages of the search engine and we have to spend some time to first understand our problem/issue/technology/field and then use the information found to get what we need. I think that at the beginning of your adventure with CTFs, it is worth using writeups, which I already wrote about in the article.

<br>

**Q:** `How to maintain willingness and motivation? What topics were the most interesting for you (and which ones you didn't like much)?`<br>
**A:** Regarding motivation, I don't know what it's like for others, but in my case, the desire to learn cybersecurity came to me at some point. Perhaps my motivation is other people who are much smarter than me and have greater skills. Whenever I think I know a topic very well, there will be someone who knows it better. I greatly respect the knowledge of the people I had the opportunity to meet and I strive for such knowledge myself. So I think this is the driving force behind my motivation and constant desire to learn. When it comes to the topics that interested me and which ones I didn't, I think each topic was interesting in its own way. However, if I had to choose my least favorite category in which I don't want to develop, it would be GamePWN. The more popular categories are PWN, RE, and Crypto. I have always had and still have a lot of problems with them - but these are categories in which I want to develop, so I do not cross them out. I think my favorite category is Web. When it comes to challenges, in the case of machines, the most interesting one is always the privilege escalation stage.

<br>

**Q:** `How can you master different topics such as reverse engineering, crypto, binary exploitation, and hardware attacks to solve the challenges besides the regular machines which require expert knowledge in case of insane machines about pentesting Domains such as web exploitation and different network attacks?`<br>
**A:** I once dreamed of gaining in-depth knowledge of various security areas. Now I know that it is simply unattainable. Of course, we may have some knowledge in various areas, but we will not be experts in many areas. When it comes to Hack The Box, as I wrote at the beginning of this article, my success is really the success of many people with whom I played and whom I pestered many times for help in finding an error in the code or explaining many, many issues. I don't consider myself an expert and I know about my shortcomings. I think there is no shame in not knowing something, the most important thing is to be aware of it. Then we can also select a team to cover as many areas as possible. I think this is also part of the "trick" in CTFs that allow you to build strong teams.

<br>

**Q:** `What did you do when you got stuck with the box? `<br>
**A:** The situation in which I didn't know what to do happened often due to the large variety of tasks and, consequently, the need to have extensive knowledge in various areas - which one person is not able to have (at least in my opinion). In the case of active machines, the help of a team that, due to the experience of different people, can analyze the problem from different points of view is invaluable. Additionally, the ability to search for information on Google and connect facts, especially those that are not related at first glance, is very useful. In the case of challenges/machines that are not active and I have as much time as I want to complete them, e.g. a walk or anything else unrelated to Hack The Box helped. I think this is a very good solution to all kinds of problems. A different environment and a moment to breathe can do wonders and give you very good ideas. Another way was to look at writeup.

<br>

**Q:** `How did your perception/ way of thinking change, if you compare it before starting HTB and after finishing all boxes on HTB?`<br>
**A:** As I mentioned earlier, Hack The Box and other CTF platforms teach you to take a broader look at various problems, combine seemingly unrelated things, and create often exotic payloads. I believe that thanks to this adventure I can look at the applications I test during pentests differently. I could compare it to the visions Dr. had. Shaun Murphy from "The Good Doctor". Certainly, experience from such platforms has a positive impact on one's career, especially in offensive positions.

<br>

**Q:** `How did you learn and what websites and resources you use?`<br>
**A:** I learn all the time. In this profession, you can't stop learning. I think it is crucial to acquire certain basics so that I can then move on to practice and solve as many different problems as possible. It is practice and repetition of certain things that allow you to learn. I don't think I said anything new here. When it comes to resources, I used many websites and tools, just like other people who played with me. Putting it together here would make a huge list. For this reason, the [Not The Hidden Wiki](https://github.com/notthehiddenwiki/NTHW) project was created, which collected all these links in one place and divided them into different categories. So please visit the main page of our project!

<br>

If you have any further questions after reading this article, please let me know and I will add your questions to the article!

## What next?

Despite the end of a certain stage of my life related to CTF, I think that I will still visit Hack The Box from time to time to complete the latest machines/challenges, even to de-stress after a whole day of hacking. Currently, I am planning to delve into the topic of Malware Development and related topics - I think I can say now that the topic of malware development will be a series on Not The Hidden Wiki. I will certainly devote some of my "free" time to the development of the Not The Hidden Wiki project, which, as it turns out, has grown from a small, unknown project to an increasingly well-known resource used by many people, regardless of the area of ​​cybersecurity they are interested in.

## THANK YOU GUYS! - Hall of Fame

As I mentioned, in addition to developing my skills on the platform, I met many people who have extensive knowledge on various topics and it is thanks to these people that I was able to get to the point where I am today! It is thanks to people who pull you up and who are around us that we can develop! Thank you for everything!

* [Michał Kucharski - M. Kucharskov](https://kucharskov.pl/)
* [Riccardo M.](https://www.linkedin.com/in/ricc-m/)
* [Tamás Péter](https://www.linkedin.com/in/tam%C3%A1s-p%C3%A9ter-705136285/)
* [Bryan McNulty](https://www.linkedin.com/in/bryanmcnulty/)
* [Roberto Gesteira Miñarro](https://www.linkedin.com/in/roberto-gesteira-minarro/)
* [Markus Mayer](https://www.linkedin.com/in/markus-mayer-57b2971b7/)
* [Yaniv Buta](https://www.linkedin.com/in/yanivbuta/)
* [Dimitar Ganev](https://www.linkedin.com/in/dimitar-ganev-syl-/)
* [Vince Lendvai](https://www.linkedin.com/in/vince-lendvai-a6a32826b/)
* [Jonathan Kachlon](https://www.linkedin.com/in/jonathan-kachlon-595a5a20a/)
* [Eson (Esonhugh) Qian](https://www.linkedin.com/in/anti-osint-prefix-esonhugh-skyworship/)
* [Marcin Motwicki](https://www.linkedin.com/in/marcinmotwicki/)
* [Lukasz Lamparski](https://www.linkedin.com/in/lukasz-lamparski/)
* [Karol Królak](https://www.linkedin.com/in/karol-krolak/)
* [Dawid Ćwikła](https://www.linkedin.com/in/dcwikla/)
* [Ricardo Silva](https://www.linkedin.com/in/ricardo-silva-9b51021a3/)
* [Rafał Wójcicki](https://pl.linkedin.com/in/lu7x00)


Remember to also follow the **Not The Hidden Wiki** project on social media!

* [Linkedin](https://www.linkedin.com/company/not-the-hidden-wiki/)
* [X](https://x.com/NotHiddenWiki)
* [Discord](https://discord.com/invite/HZFcczkva9)

<p align="center">
  <img src="https://raw.githubusercontent.com/notthehiddenwiki/NTHW/nthw/.github/notes/hackthebox/htb_KoTH.png">
</p>


#### Sources of some elements of the article

1. Gynvael Coldwind: Rok CTFów z Dragon Sector - [link](https://gynvael.coldwind.pl/?id=525)
2. Hack The Box: How to Play Challanges - [link](https://help.hackthebox.com/en/articles/5185436-how-to-play-challenges)
3. How to Exit VIM - [link](https://builtin.com/articles/how-to-exit-vim)