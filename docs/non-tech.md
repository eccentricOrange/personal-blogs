---
layout: default
title: The other side of tech
---

# The other side of tech
{: .no_toc }

## Table of Contents
{: .no_toc }

1. TOC
{:toc}

## Why do friends sometimes manage to teach their peers better than teachers?
I help out a lot of my friends out through their courses in college. This is far from unique to me, but many people turn to their friends for help instead of faculty. This also happens to classes with the best and most compassionate teachers I've met, so the obvious answers that friends are more empathetic probably don't apply.

I cannot fully answer this question today, but we'll try to think about it and tackle similar questions on this part of this blog. For now, let's look at some aspects of how I help my friends learn something, and hope that you're able to apply this whenever it's relevant to your life.

### Finding out where they stand
Yesterday, one of my old roommates and good friends (who we'll call Dhruv) kidnapped me and dragged me to the library to help him learn hypothesis testing for his statistics exam. Yeah.

Well, the first thing we did was review his class notes briefly, just to see if his professor had taught something differently from mine. She hadn't, thankfully. The next thing I tried was asking Dhruv to solve the first sort of problems we'd encounter in the 2-3 chapters he'd asked me to help him digest in two hours. For the most part, he did it correctly, but I noticed that he hadn't drawn the normal curve showing the critical reasons. Upon asking him about it, we figured out that he didn't really know how the system worked.

Notice this - by just testing Dhruv on real-world problems (or "real-world" problems, in this case), we were able to identify both that he knew the bulk of the steps *and* that he didn't know the fundamental underlying concept. This gave me two tools to boost his confidence: the former to let him understand that he had a foothold, and the latter to show him that it's easy to learn by explaining precisely what he didn't know.

### Providing a precise explanation
The next thing we did was to tackle the concept in its rawest form: diving into populations, samples, estimators etc. This sort of a clear-cut explanation is my style of doing it, but it takes someone close to know when to apply it. My best friend, for instance, knows that I strongly prefer a clear understanding but that I also often need mnemonic or other visual aides to recall concepts.

## Technical Documentation
I'm hilariously famous among my friends for both writing verbose code, and documenting in a lucid style. A consequence of this is that there is no shortage of people asking me how I do it. While I'd love to guide you to excellent resources like [Google's article on it](https://developers.google.com/tech-writing/one/documents), [UC Berkley's guidelines](https://guides.lib.berkeley.edu/how-to-write-good-documentation), and several others, here are some of my personal tips:

### The philosophy
I have a few principles guiding how my documentation is written, and with these you should be able to derive the rest of the tips I provide. But we will discuss those tips later on anyway.

1.  **I am the one of the two primary audience:** My docs *must* explain anything I've spent time thinking/deriving/designing, as I'm fairly forgetful. It *must* explain any hacks/workarounds.
2.  **The other audience is a smart but clueless internet stranger:** I should write from the perspective of someone who knows the basics of the language and surrounding technology, but not the specifics of the project. So, I should explain contexts and use cases well. I should also try to give them a high-level foothold before throwing them into the abyss of my codebase.
3.  **Try to not document code:** If my code is so complex that it's difficult to understand without a docstring, it's not good code. I should document the logic and the design decisions, not the code itself. The code should be self-explanatory. However, it is important to recognize that some cases (such as competitive coding and embedded coding) will often be convoluted, and in this case I must not shy away from verbose documentation.
4.  **Cite heavily:** If I've used a resource to understand something, I should cite it. This is not just for academic honesty, but also to help the reader (who could be me in another life!) understand what I understood when I wrote the project.
5.  **High-level first:** The reader should be able to understand the project at a high level before diving into the details. It is especially important for libraries and frameworks, where the user may not need to understand the nitty-gritty of the codebase to use it. This is redundant with point #2, but it bears repeating, as this is one the most common reasons large projects sometimes feel like labyrinths to me.
6.  **Clarity is king:** If anything feels ambiguous or a personal choice, it should be explained and made clear.

### What to write about code itself?
Let's consider the following [snippet from my own project](https://github.com/eccentricOrange/npbc/blob/0a43f37c39840bfa3dfd4bb3bd945370e00c6c40/npbc_core.py#L106C1-L116C137):

```python
def extract_number(string: str, month: int, year: int) -> date:
    """if the date is simply a number, it's a single day. so we just identify that date"""

    day = int(string)

    # if the date is valid for the given month
    if 0 < day <= monthrange(year, month)[1]:
        return date(year, month, day)

    # if we reach here, the check failed and it's not a valid date
    raise npbc_exceptions.InvalidUndeliveredString(f'{string} is not a valid date for {datetime(year=year, month=month, day=1):%B %Y}.')
```

*   First of all, note that the function name tells us its purpose clearly. GIven that, we do not need to explain in dept it's purpose. So, the docstring instead focuses on a **justification for a decision** I made in how the function behaves. This makes it easy to see what the function does elsewhere when it is called, and the docstring mentally prepares the reader on what to expect.

    Consider another function, from a [different file in the same project](https://github.com/eccentricOrange/npbc/blob/0a43f37c39840bfa3dfd4bb3bd945370e00c6c40/npbc_cli.py#L570-L697):

    ```python
    def getpapers(parsed_arguments: ArgNamespace, connection: Connection) -> None:
    """get a list of all papers in the database
    - filter by whichever parameter the user provides. they may use as many as they want (but keys are always printed)
    - available parameters: name, days, costs
    - the output is provided as a formatted table, printed to the standard output"""

    # get the papers from the database
    try:
        raw_data = npbc_core.get_papers(connection)

    # if there is a database error, print an error message
    except DatabaseError as e:

    [...]
    ```

    This function is relatively complex, and here it makes sense to provide more information about what the function does. The docstring here is more verbose, and explains the function's purpose, the parameters it takes, and the output it provides.

*   The comments just aide the reader in following through the code. Additionally, the second comment **explains how the logic was derived** in the code, and saves you from re-engineering it every time you read the code.

### Quickly tell me the most important things
Let's look at examples of my projects' README files.

> # NewsPaper Bill Calculator
> {: .no_toc }
> 
> This app calculates your monthly newspaper bill. Requires SQLite>=3.35 (and Python>=3.9 if you intend to develop anything, instead of just using the executables).
> 
> ## Key concepts
> {: .no_toc }
> 1. Each newspaper has a certain cost per day of the week
> 2. Each newspaper may or may not be delivered on a given day
> 3. Each newspaper has a name, and a number called a key
> 4. You may register any dates when you didn't receive a paper in advance using the `addudl` command
> 5. Once you calculate, the results are displayed and logged.
> 
> From [npbc](https://github.com/eccentricOrange/npbc/blob/0a43f37c39840bfa3dfd4bb3bd945370e00c6c40/README.md)


> # Scholarships scraper
> {: .no_toc }
> 
> This project helps you get through giant lists of scholarships. In particular, this project handles the following for you:
> *   Downloading the HTML source of multiple webpages.
> *   Handling all the files and intermediate conversions.
> *   Providing a framework to handle the different types of webpages.
> 
> However, since each provider/website use their own DOM layout, it is not feasible to provide a standardised interface for all of them. So it is up to you to write code to actually parse the website (and, yes, this is kind of complex).
> 
> 
> ## Expected website structure and pre-requisites:
> {: .no_toc }
> *   There are several pages of **lists** on the website. These are numbered and the number can be written inside a URL.
> *   Each **scholarship** in the list can provide you a name and a link.
> *   Following the link will take you to a **page** with more details about that specific scholarship.
> *   All this data must be directly embedded in the HTML (and not downloaded through JavaScript, for instance). This does appear to be the common case, thankfully.
> *   You'll need to know how to use the [`BeautifulSoup`](https://www.crummy.com/software/BeautifulSoup/doc/) Python module (in addition to knowing Python scripting, of course).
> *   A recent Python 3, and all Python dependencies (listed in [requirements file](./requirements.txt)), must be installed. You can use the `pip` tool to install the dependencies using the following command:
> 
>     ```shell
>     python -m pip install -r requirements.txt
>     ```
>
> From [scholarships-scraping](https://github.com/eccentricOrange/scholarships-scraping)

> # Differential Drive Robot
> {: .no_toc }
> 
> This library provides an interface to easily control a [differential wheeled robot](https://en.wikipedia.org/wiki/Differential_wheeled_robot) using an Arduino-compatible microcontroller.
> 
> The expectation is that you have an even number of motors, with one half on either side of a structure that looks like a rover or a car. You then control the direction the robot moves in by controlling which motors turn on and in which direction. For example, if the left motors spin forward and the right motors spin backwards, the robot will rotate clockwise.
> 
> Check out [line-follower-std](https://github.com/eccentricOrange/line-follower-std) and [line-follower-smooth](https://github.com/eccentricOrange/line-follower-smooth) for two examples where this library is used in a project.
> 
> From [DDBot](https://github.com/eccentricOrange/DDBot)

Notice what's common between these?

1.  **Quick and clear explanation:** The first few paragraphs quickly tell you exactly what the project does, and what context you should use it in.
2.  **Key concepts:** Lay out in the initial stages itself, any information that will help the reader follow through the rest of the codebase or documentation.
3.  **Key dependencies:** If there are any dependencies that are not standard, they are mentioned upfront. This is especially important for projects that are not meant to be used by the author alone.

### Explain how to use the project
Most of the remaining space in these READMEs is dedicated to helping you run or use the project. I'm not going through them here, but you can check them out in the links provided:

*   **[npbc](https://github.com/eccentricOrange/npbc?tab=readme-ov-file#installation)**: Succinctly explains how to install and run the project. Try to accommodate different users. For instance, try to provide ways for different operating systems.
*   **[scholarships-scraping](https://github.com/eccentricOrange/scholarships-scraping?tab=readme-ov-file#usage)**: Unlike NPBC, this one is a development framework, not an end-user tool. So, we provide various examples with code, walk through when to use one method over another, and lay down suggested steps for developing using the project.
*   **[DDBot](https://github.com/eccentricOrange/DDBot?tab=readme-ov-file#overview-of-the-library)**: This one is also a library. In this case, we expect the user to call the library functions rather than modify them on their own. So we give them a high-level classification of the functions and what they do, followed with case-by-case examples of all the different ways you can use the library functions.

### Explain different parts of the project
In each of [npbc](https://github.com/eccentricOrange/npbc?tab=readme-ov-file#detailed-explanations) and [scholarships-scraping](https://github.com/eccentricOrange/scholarships-scraping?tab=readme-ov-file#understanding-the-file-structure), I provide a table explaining the purpose of each file in the project. This is especially useful for larger projects, where it's easy to get lost in the codebase. Moreover, in Scholarships Scraper, I provide a "Yes/No" column that explains the user whether they should modify the file or not, providing clarity as they are expected to muck around with these files.


## [HOW TO TECH \#1] How to come up with project ideas?

{: .note-title }
> This entry is taken my [Reddit post](https://www.reddit.com/r/btech/comments/1eovf99/how_to_tech_1_how_to_come_up_with_project_ideas/).


There are a two basic ways I (and I guess other much smarter innovators throughout history) have come up with their projects.

### 1. Is there something you need?
This seems to be by far the best recipe for a good project. Some examples, and you don't need to dig much online to find tons more:
* [me] I wrote a little application to calculate the monthly newspaper bill for my home. Keep in mind: the prices differ per week day, sometimes a certain newspaper delivery is just missing, and we subscribe to 5-6 different papers. While this basic explanation of what it does is fairly simple, I was able to evolve the project to teach me a lot more.
* [me] I'm currently working on a robot simply because I wanted to learn about robotics algorithms and couldn't find a good, robust robot cheap enough to test my algos on.
* [Linus Torvalds] Bro made Linux (one of the most used kernels if you count Android and servers), simply because the alternative was expensive.
* [Linus Torvalds] Bro also made Git just to help maintain Linux and make sure that he doesn't have to talk to too many people 💀
* [u/Tornole](https://www.reddit.com/user/Tornole) This project is a great example: [https://www.reddit.com/r/EngineeringStudents/comments/1cmpdsw/i_built_a_tool_to_help_me_type_my_engineering/](https://www.reddit.com/r/EngineeringStudents/comments/1cmpdsw/i_built_a_tool_to_help_me_type_my_engineering/)

If you have an itch that nothing existing solves, or at least doesn't do it quite the way you want, start creating your own solution. Keep in mind that many of the software tools you use today were created by people who wanted to solve their own problems. Think about that.

### 2. Rebuild something that exists
If you are quite new to technical fields, you're obviously going to struggle with building something all by yourself. You need to get a foothold. In such a scenario, try to first build something that already exists, and preferably something you're familiar with.

Some suggestions (these are the only  domains I know about):
 
#### Beginner/Intermediate level
- [electronics] drive a single motor with varying speed and direction
- [electronics] make LEDs blink in a certain sequence (whatever sequence you want). can you achieve this without a microcontroller too?
- [electronics] make a simple IoT system. for example, control some LEDs with your phone wirelessly. 
  
  {: .warning }
  > PLEASE **DON'T PLAY WITH MAINS VOLTAGE** WITHOUT EXPERIENCE AND/OR COMPETENT SUPERVISION, stick to simple battery-operated stuff
  
- [programming] write a to-do app. start with something really basic, maybe just a simple array. evolve it into either a full-fledged native app or maybe something that can support multiple users on a server

#### Experienced level
- [robotics] make a line follower robot. can you achieve this without a microcontroller too? or can you leverage the microcontroller to achieve good speed/control?
- [robotics] make a robotic arm with a GUI and a camera. if you point out an object in the POV video feed using the GUI, the arm goes to pick it up
- [programming] write your own kernel
- [programming] write your own compiler/interpreter
- [programming] write your own VM

### 3. Other basic advice
- **Start at your own level:** Common mistake, I made it too. You probably will too despite me telling you, because it's difficult to judge your own level. But keep in mind that there's no shame in trying something simpler and simpler until you're working on something you're comfortable with.
- **Design with intent:** This one will be a little difficult for beginners to follow; even for me it really clicked only once in college despite having like 8-9 years of prior experience. Define the purpose of your project, break it into smaller parts, develop each individual bit to a good standard, and keep testing every little bit as you build it. Then put it together. Don't start with a giant system all at once, humans suck at this and will struggle.
- **Ask around!** No idea why more people don't do this. If you see someone doing something you find interesting, just go and ask them about. Most people will be happy to tell you about their own work. Even if they're not, cool, you've now eliminated one guy out of like 8 billion people in the world.
- **Find high quality resources:** For software stuff, see the wiki of [r/learnprogramming](https://www.reddit.com/r/learnprogramming/wiki/index/) Electronics and mech peeps, you need some theory. For electronics, I cannot over-recommend *The Art of Electronics* (though it's a tough read), but at least learn basic circuital laws, purposes of basic RLC components etc. Even school-level textbooks are fine for this. Mech peeps, idk much, but try do learn some CAD - it helps a lot.
- **See what other people are doing:** Get off of Reddit, and interact with flesh-and-blood people. If you're not in a college or otherwise productive environment, go and find industry people. Even simple electricians and carpenters can show you some basics, some of which I find very useful (but be careful please).
- **Improve your existing projects:** Even simple school/college assignments qualify for this. Take something and add more features to it. You learn a lot along the way. I'll break down [a very simple programming example and involved concepts in another post](https://www.reddit.com/r/btech/comments/1eovsst/how_to_tech_2_i_only_know_the_basics_or_know/).
- **Re-build the same projects:** Once you make something (and assuming you spent at least like 3-4 months on it), you would've likely learnt a lot, but that project will be a mess. But now you have clarity. So make a high-level flowchart (or some other diagram or write it down or whatever) of how that project should be, and make it again. This time, try your best to focus on quality. You learn a lot about pitfalls and how to make good stuff in this way. Many of your projects will also become more reliable.


## [HOW TO TECH \#2] I only know the basics, or know nothing. How do I make anything with that?

{: .note-title }
> This entry is taken my [Reddit post](https://www.reddit.com/r/btech/comments/1eovsst/how_to_tech_2_i_only_know_the_basics_or_know/).

{: .tldr }
> Use what you know to make something, even if it's very simple. Then try to find a way to use whatever new stuff you learn to that project.

___

### Explanation
This is a very common question, and I've seen a lot of people struggle with it. The answer is simple: **start with what you know**. If you're a beginner, you probably know very little. That's fine. Start with that. If you're intermediate, you probably know a bit more. That's fine too. Start with that.

As you go along, keep learning stuff. Ideally, I'd recommend at least some structure when starting out, at least as a YouTube playlist, if not something like a college class. But even if you don't have that, just keep learning random related stuff. Whatever you do, find a way to use that new stuff in your project.

It's okay if you initial projects turn out to be a Frankenstein's monster. That's how you learn. But as you keep building, you'll start to see patterns. You'll start to see how to make things better. You'll start to see how to make things more reliable. You'll start to see how to make things more efficient. Most importantly, **you'll learn how to integrate different types of technical concepts to make something.**

### Example
Keep in mind, this is an example of _how to think_ when developing something. It's **not a laundry list of instructions for you to follow**. You really should try to build something just on the edge of your current capabilities - that's the cheat code to learn.

Let's start with a simple to-do list app, in whatever programming language you like.

1. **Bare bones basics:** If you've just learnt about programming, maybe you've just learnt what variables are. Make one to store the name of one task, and another to store its status. That's it.
2. **Add interactivity:** Maybe your course now moves on to input and output. That's great! Now someone apart from a developer can use your "app." Make it input task name and status, and output the same back.
3. **Loops:** But you need to run it every time. Put the whole thing into a `while` loop.
4. **[no new concept]** You're a busy person, and have a lot of tasks in mind. So, make more variables, two for each task.
5. **Arrays:** That's a pain to maintain. Put it into arrays. You'll also be forced to learn about `for` loops at this point.
6. **Files:** All your tasks reset every time you run the "app." That's not how professional apps work, right? You somehow need to save the data in between. Maybe you decide to use a CSV file.
7. **[celebrate]** At this point, your "app" can really be called an app, i.e., it's actually functional and useful.
8. **GUI:** Why not try to learn some kind of GUI framework? Maybe you try web/app dev, or maybe something is built into the your language of choice.
9. **Multi-user:** By this point, your family/friends has taken note of your work. So you try to implement some basic user management.
10. **OOP:** Now your code is too complex. Break it down, and use OOP (or whatever) to clean it up.
11. **Database:** Someone uttered this word to you. You decide to explore what it means. Do a basic course on it, and then try to relace your CSV file with a proper DB.
12. **Server-side separation:** Why not see if you can make your application accessible to at least everyone on your home Wi-Fi?
13. **Web-dev:** Look beyond your own home. Make it a website!
14. **CI/CD:** Man, it's really tedious to republish the website every time you make a tiny change.
15. **Linux:** You need to know Linux to use CI/CD in most cases.
16. **Git:** OH IT WAS WORKING AND NOT IT ISN'T!! AND I FORGOT WHAT I CHANGED!! Learn to use version control.

If you got here, congratulations you've learnt most of the major tools and concepts of the software world. At least whatever you need to know to very confidently learn something else on your own. And you built something you can be proud of.


## [HOW TO TECH #3] My college/university wants us to (or I want to) install and learn Linux. What are my options?

{: .note-title }
> This entry is taken my [Reddit post](https://www.reddit.com/r/btech/comments/1eoy25f/how_to_tech_3_my_collegeuniversity_wants_us_to_or/).

### 0. Some keywords and concepts you need to know no matter how you choose to install Linux
- **Distro:** Short for distribution. This is the version of Linux you're going to install. The most popular one is Ubuntu, but there are many others. Some are more user-friendly, some are more developer-friendly, some are more server-friendly, some are more security-focused, some are more privacy-focused, some are more bleeding-edge, some are more stable. You get the idea.
- **Kernel:** This is the core of the operating system. All Linux distros use the same kernel, but they may have different versions of it. Similar to the NT Kernel for Windows and the Darwin Kernel for macOS.
- **Partition:** This is a way to divide your hard drive into separate sections. You can have multiple partitions on a single hard drive, and each partition can have a different operating system. This is how you dual-boot.
- **Virtualization:** This is a way to run one operating system on top of another. You can run Linux on Windows, or Windows on Linux, or even Windows on Windows.

### 1. Know your options
#### Dual-boot
Divide your hard-disk (HDD) or solid-state drive (SSD) space into two. You can then have two operating systems installed, but may boot into only one at a time.

#### VM
Run one OS (such as Ubuntu) on top of another OS (such as Windows). Many options like VirtualBox, Oracle, the Windows thing (for Pro or better editions), VMWare etc. You can technically boot two OSes at a time.

#### WSL
For Windows 10 and newer, there's a new choice, officially supported by Microsoft. You can install a WSL distro through Windows. It will behave like a VM but the nitty-gritty of the virtualization is handled by a hypervisor, so it is much faster and more responsive than a VM. The downside is that you only get a CLI, and GUI on a per-app basis. You don't get the whole OS GUI.

#### Docker
Unfortunately, this one is a bit hard if you don't already know about the Linux world, but there's a way to run many many different kind of OSes with a virtualization method that's a lot better than traditional VMs and not as restrictive as WSL. You can also have separate OS instances per project without consuming a ton of storage space.

#### Cloud
This is, again, not so easy if you don't already know about Docker and Linux. There are online services (such as GitHub Codespaces) where you can get a remote Linux system per project. With a student license, you get a good amount of compute time though storage is limited. You don't even have to install anything on your system (except a browser, and maybe VS Code). It depends on a good internet connection though.

### 2. The resource allocation thing

> I don't clearly understand the 'resource allocation' thing. So, what should I go with

\[Question courtesy of [this post](https://www.reddit.com/r/btech/comments/1em4uzm/comment/lgwje1c/)\]

Nothing, they're talking about how you divide your hard drive space if you dual-boot.

In general, I'd recommend the following configuration:
- At least 100-150 GB to `C:` of Windows. This doesn't account for you installing heavy apps or similar, so you'll have to adjust accordingly.
- [optional] Separate partitions for Data and Applications in Windows. Sizes are up to you.
- 50-100 GB for the Linux partition, per distro. You can get away with lesser usually, but in my experience this is a good number.

### 3. Opinion/recommendation
**If you're completely new**, do a WSL install first. Less chances of messing things up, and you can keep switching between Windows and Linux quickly if you get confused.

**If you are required to, or if you have some experience**, do a dual-boot. This lets you really experience Linux, and many tasks (like interacting with USB ports) is a lot more seamless. If you can manage it, I'd recommend this.

Whatever you do, if you choose Ubuntu, try to get a distro who's pattern is like this: `xx.04`, where `xx` is an even number. These are "LTS (long term support)" releases and are likely to be stable for a long period. Current releases are 22.04 LTS and 24.04 LTS; some laptop manufacturers may not have provided drivers for these, so in many cases you may have to use an older one like 20.04 LTS.

### 4. A note on self-learning
For a lot concepts, I (or someone else) can explain it to you. But for dev tooling (as I've come to call it), you really do need to grapple with it yourself to get a foothold. Please do your own research. Watch several different videos on how to dual boot, read articles from at least 2-3 different sources. You'll get to know the usual steps, so you can be aware if one particular resource advises something different.

Also, keep in mind that this has risk of data loss (from Windows especially). So you really should take a full system back up before proceeding.

### Resources/references
- **WSL**: [https://learn.microsoft.com/en-us/windows/wsl/](https://learn.microsoft.com/en-us/windows/wsl/)
- **Official Ubuntu install tutortial**, including dual-boot instructions, but recommend you to search online and at least watch some videos: [https://ubuntu.com/tutorials/install-ubuntu-desktop]()
- **Ubuntu VM:** [https://ubuntu.com/tutorials/how-to-run-ubuntu-desktop-on-a-virtual-machine-using-virtualbox](https://ubuntu.com/tutorials/how-to-run-ubuntu-desktop-on-a-virtual-machine-using-virtualbox)
- **[my own list] Docker resources:** [https://eccentricorange.netlify.app/tools#3---docker-for-isolating-your-development-environment](https://eccentricorange.netlify.app/tools#3---docker-for-isolating-your-development-environment)
- **GitHub codespaces:** [https://docs.github.com/en/codespaces/overview, https://code.visualstudio.com/docs/remote/codespaces](https://docs.github.com/en/codespaces/overview, https://code.visualstudio.com/docs/remote/codespaces)
- [r/linux4noobs](https://www.reddit.com/r/linux4noobs/), [r/linuxquestions](https://www.reddit.com/r/linuxquestions/)

In the interest of making sure I'm not aligning to a specific party, popular alternatives:
- **To Ubuntu:** Debian (stable), Fedora (dev-oriented), Arch (bleeding-edge), and many other Ubuntu-offshoots
- **To VS Code:** Basically any IDE
- **To Codespaces:** Gitpod, [offline dev containers](https://code.visualstudio.com/docs/devcontainers/containers)


## [HOW TO TECH #4] Why should you lean Linux, Git, command lines etc? How are they better than things like buttons in an IDE?

{: .note-title }
> This entry is taken my [Reddit post](https://www.reddit.com/r/btech/comments/1fojdtd/how_to_tech_4_why_should_you_lean_linux_git/).

### 1. Why command lines?
*   **Servers and other remote systems usually don't give you another option**

    For the vast majority of languages in the modern world, there is a shortcut to run code. Sometimes you can press a button, other times you need to hit a key combination, and many other times you need to click a menu item. This is called an Integrated Development Environment (IDE). It's a great tool, and I use one all the time.

    Realistically, however, there are many situations where you can't use an IDE. Do you know what a server is? To give you one example: when you request something from the internet (such as reddit.com), your computer asks a computer operated by Reddit called the server. It then processes your request and sends you back the page you wanted. This is a very simplified version of what happens, but the point is that these servers are usually what you'd call a "remote system." This means that they're deployed somewhere else, physically far away from you, and often run OSes that don't have a GUI (Graphical User Interface). Your only option is a command line interface (CLI).

    One of the more popular CS jobs in our country appears to be web development, and you cannot do that without knowing command lines.

    Personally, I am an embedded systems developer. The code I have to write doesn't even run on what you'd typically call a "computer." It runs on devices like ESP32s, STM32s, Arduino boards, Raspberry Pis, etc. Forget a GUI, these devices often don't have an operating system at all!

*   **You simply have more functionality**

    EVen the largest screen in the world has a finite number of pixels; you will not be able to put every single kind of functionality in a GUI. However, when you can simply type the name of what you want, the limit then becomes combinations of keyboard characters.

*   **Batch processing many instructions**

    Let's say you need to do something in a GUI like a word processor that involves 10 steps. You usually have to do these 10 things (in sequence) byt clicking on things. Yes, there are things like VBA which means you can write scripts to do this automatically, but this isn't an option in every software. However.... If all your instructions are text to begin with, nothing is stopping you from writing all of the instructions together in a file and running it all at once :D

    Over the years, computer programmers have taken this into an extreme. Turns out, in many cases, the commands you type into a command line are in fact part of a programming language. This means you can write scripts involving complex (or simple) conditions, loops etc and you can run it all at once. Or on a schedule. Or on a specific event/condition. Or on a different machine (such as a remote server).

*   **Chaining commands**

    Let's say you have software A which gives you a list of student IDs from your college, and you want to extract just the IDs of students who are in the Electrical Engineering department. Usually you have to take the list from software A and paste it into a searching program, or write a script in software A itself to do the search for you. However, modern operating systems ship with command-line programs which can just do the job then and there in a single line. Don't believe me? Here's how you can do it in Linux:

    ```bash
    cat list_of_student_ids.txt | grep "EEE"
    ```

    That's it. `cat` is a program that reads a file and prints it to the screen. `grep` is a program that searches for a string in the input it gets. The `|` character is called a "pipe" and it sends the output of the program on the left to the input of the program on the right. So the above command reads the file `list_of_student_ids.txt`, and sends it to `grep` which searches for the string "EEE" and prints the lines that contain it.

    Or in Windows PowerShell:

    ```pwsh
    cat list_of_student_ids.txt | findstr "EEE"
    ```

    The `findstr` program is similar to `grep` in Linux.

    The interesting part is that there is no limit to how many commands you can chain together. You can have 10, 100, 1000 commands all chained together to do something that would take you hours to do manually.

*   **Dockerfiles, CI/CD pipelines, etc**

    There is a tool in the software called "Docker," which is a way to run many many different kind of OSes with a virtualization method that's a lot better than traditional VMs. The way you create a "Docker image" (don't worry if you don't know what that is) is by writing a file called a "Dockerfile." This file is a series of commands that tell Docker how to build the image. It's sort of analogous to normal coding in any programming language...but the commands you put in are what you'd normally put into a a command line! So if you don't know how to use a command line, you can't use Docker.

    And Docker isn't the only tool that works like this.

### 2. Why Git?

To be perfectly honest with you, I've written about Git before, and I don't really want to repeat the content. So here's a summary:

> * Git is just a tool (an **app**, if you will) that tracks changes to a project.
> * GitHub, GitLab, and Bitbucket are online services that **host Git repositories**.
> * The `.git` folder makes a project folder a **Git repository**, and contains all the history and metadata needed for the Git tool to work.
> * These services provide a way to **share your code** with others, and use cloud storage without grappling with traditional cloud storage services like Google Drive or Dropbox. They "understand" the `.git` folder to provide a web interface to the Git repository.

Feel free to check out the original post over on my website (linked at the end). Honestly, I'm not trying to get you to visit my website; I don't earn anything or get user sign-ups or anything like that if you visit. 

### 3. Why Linux?
This question has been asked and answered several times on the internet, and you really should read the Google search results. DO IT, DON'T JUST READ MY ANSWER.

That said, here are my reasons, especially as an embedded systems developer:
*   A bunch of the hardware I use (like Raspberry Pi) only runs Linux. No choice. This is also true of many servers and other remote systems.
*   It's a lot easier to customize how and where you install software on Linux. This is especially important when you're working with a lot of different software packages that need to work together (or need to be separated from each-other like two really annoying twins).
*   You can change almost any setting in the OS you like; this is both a blessing and a curse though, and is often abused by programmers.
*   Almost everything (settings, configurations, hardware ports, internet ports etc) is treated like a file descriptor (if not an actual text file). This means that you can write really simple code to interact with any part of the OS, and there's not need for fancy APIs/libraries in your code.
*   It's very quick and easy to install and setup. I created a setup script that installs all the software I need, sets up folders the way I like, and even imports most of my passwords and things from my previous install. That way, I can very quickly set up a new system if I need to (and I often need to, on my Raspberry Pi).

___

Link to my article explaining command lines, Git, and Docker along with guides on how to get started with them: [https://eccentricorange.netlify.app/tools](https://eccentricorange.netlify.app/tools)