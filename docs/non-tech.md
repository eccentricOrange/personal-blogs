---
layout: default
title: The other side of tech
---

# The other side of tech

## 1.   Why do friends sometimes manage to teach their peers better than teachers?
I help out a lot of my friends out through their courses in college. This is far from unique to me, but many people turn to their friends for help instead of faculty. This also happens to classes with the best and most compassionate teachers I've met, so the obvious answers that friends are more empathetic probably don't apply.

I cannot fully answer this question today, but we'll try to think about it and tackle similar questions on this part of this blog. For now, let's look at some aspects of how I help my friends learn something, and hope that you're able to apply this whenever it's relevant to your life.

### Finding out where they stand
Yesterday, one of my old roommates and good friends (who we'll call Dhruv) kidnapped me and dragged me to the library to help him learn hypothesis testing for his statistics exam. Yeah.

Well, the first thing we did was review his class notes briefly, just to see if his professor had taught something differently from mine. She hadn't, thankfully. The next thing I tried was asking Dhruv to solve the first sort of problems we'd encounter in the 2-3 chapters he'd asked me to help him digest in two hours. For the most part, he did it correctly, but I noticed that he hadn't drawn the normal curve showing the critical reasons. Upon asking him about it, we figured out that he didn't really know how the system worked.

Notice this - by just testing Dhruv on real-world problems (or "real-world" problems, in this case), we were able to identify both that he knew the bulk of the steps *and* that he didn't know the fundamental underlying concept. This gave me two tools to boost his confidence: the former to let him understand that he had a foothold, and the latter to show him that it's easy to learn by explaining precisely what he didn't know.

### Providing a precise explanation
The next thing we did was to tackle the concept in its rawest form: diving into populations, samples, estimators etc. This sort of a clear-cut explanation is my style of doing it, but it takes someone close to know when to apply it. My best friend, for instance, knows that I strongly prefer a clear understanding but that I also often need mnemonic or other visual aides to recall concepts.

## 2.   Technical Documentation
I'm hilariously famous among my friends for both writing verbose code, and documenting in a lucid style. A consequence of this is that there is no shortage of people asking me how I do it. While I'd love to guide you to excellent resources like [Google's article on it](https://developers.google.com/tech-writing/one/documents), [UC Berkley's guidelines](https://guides.lib.berkeley.edu/how-to-write-good-documentation), and several others, here are some of my personal tips:

### The philosophy
I have a few principles guiding how my documentation is written, and with these you should be able to derive the rest of the tips I provide. But we will discuss those tips later on anyway.

1.  **I am the one of the two primary audience:** My docs *must* explain anything I've spent time thinking/deriving/designing, as I'm fairly forgetful. It *must* explain any hacks/workarounds.
2.  **The other audience is a smart but clueless internet stranger:** I should write from the perspective of someone who knows the basics of the language and surrounding technology, but not the specifics of the project. So, I should explain contexts and use cases well. I should also try to give them a high-level foothold before throwing them into the abyss of my codebase.
3.  **Try to not document code:** If my code is so complex that it's difficult to understand without a docstring, it's not good code. I should document the logic and the design decisions, not the code itself. The code should be self-explanatory. However, it is important to recognize that some cases (such as competitive coding and embedded coding) will often be convoluted, and in this case I must not shy away verbose documentation.
4.  **Cite heavily:** If I've used a resource to understand something, I should cite it. This is not just for academic honesty, but also to help the reader (who could be me in another life!) understand what I understood when I wrote the project.
5.  **High-level first:** The reader should be able to understand the project at a high level before diving into the details. It is especially important for libraries and frameworks, where the user may not need to understand the nitty-gritty of the codebase to use it. This is redundant with point #2, but it bears repeating, as this is one the most common reasons large projects sometimes feel like labyrinths to me.

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
> 
> This app calculates your monthly newspaper bill. Requires SQLite>=3.35 (and Python>=3.9 if you intend to develop anything, instead of just using the executables).
> 
> ## Key concepts
> 1. Each newspaper has a certain cost per day of the week
> 2. Each newspaper may or may not be delivered on a given day
> 3. Each newspaper has a name, and a number called a key
> 4. You may register any dates when you didn't receive a paper in advance using the `addudl` command
> 5. Once you calculate, the results are displayed and logged.
> 
> From [npbc](https://github.com/eccentricOrange/npbc/blob/0a43f37c39840bfa3dfd4bb3bd945370e00c6c40/README.md)


> # Scholarships scraper
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