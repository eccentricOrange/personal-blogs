# Tools that I use in my work

I use most of the tools listed below regularly in my work as an electrical engineering student passionate about robotics. I find all of these fascinating, and would like to share that with you. Some of these are really standard tools that you'll find in any engineer's toolbox, while others are more niche. I hope you find something useful here.

Note that nothing here is sponsored, and I am not affiliated with any of the companies that make these tools. I just like them.

## 1.   Git for source control
How often have you had to deal with this?

![Badly named Word documents](assets/1-bad-naming.png)

I did pretty often. I've often lost track of which version of a document was the latest, and which one was the one I was supposed to be working on; and on occasion, I've even lost weeks of work because I accidentally overwrote a file.

Any of you that have used [Google Docs](https://docs.google.com/) or similar online tools would be [laughing at me right now](https://support.google.com/a/users/answer/13004165?hl=en). But how do you do the same thing for *any* file on your computer, not just the ones that are supported by Google's office suite? This doesn't make sense for a document, but for a technical project, you could very well have multiple versions that are developed in parallel, and you need to keep track of all of them.

Enter [Git](https://git-scm.com/). Git is a source control system that allows you to keep track of all the changes you make to a file, and revert to any version you want. It's also great for collaborating with others, as it allows you to merge changes made by multiple people to the same file. It's by far the most popular [version control system (VCS)](https://about.gitlab.com/topics/version-control/) out there today.

### Resources to understand what Git is
Just pick one of these and read/watch it, these are just an overview.
*   [Atlassian article on version control](https://www.atlassian.com/git/tutorials/what-is-version-control)
*   [Wikipedia article on version control](https://en.wikipedia.org/wiki/Version_control)
*   [Atlassian article on Git](https://www.atlassian.com/git/tutorials/what-is-git)
*   [_Git Explained in 100 Seconds_, YouTube video by Fireship](https://www.youtube.com/watch?v=hwP7WQkmECE)

### Resources to learn how to use Git
*   [_Git & GitHub Tutorial for Beginners_, YouTube playlist by Net Ninja](https://youtube.com/playlist?list=PL4cUxeGkcC9goXbgTDQ0n_4TBzOO0ocPR) (this is what I used when I learnt Git)
*   [_Getting started with Git and GitHub_, article by GitHub](https://docs.github.com/en/github/getting-started-with-github)
*   [_Git It? How to use Git and Github_ by Fireship on YT](https://www.youtube.com/watch?v=HkdAHXoRtos)
*   [Official Git documentation](https://git-scm.com/docs/gittutorial)

### Important concepts you should look into
*   [GitHub](https://github.com/)/[GitLab](https://about.gitlab.com/) or other Git hosting services
*   Git branching
    *   [Official Git documentation on branching](https://git-scm.com/book/en/Git-Branching-Branches-in-a-Nutshell)
    *   [Atlassian article on branching](https://www.atlassian.com/git/tutorials/using-branches)
*   [Issues](https://docs.github.com/en/issues/tracking-your-work-with-issues/about-issues) and [pull requests](https://www.youtube.com/watch?v=HkdAHXoRtos)
*   [The `.gitignore` file](https://git-scm.com/docs/gitignore)
*   [Resolving merge conflicts](https://docs.github.com/en/pull-requests/collaborating-with-pull-requests/addressing-merge-conflicts/resolving-a-merge-conflict-using-the-command-line)

While Git is exceedingly popular, you should know that there are alternatives, such as SVN and Mercurial.

### Interesting tidbit
[_Tech Talk: Linus Torvalds on git_, YT video by Google](https://www.youtube.com/watch?v=4XpnKHJAok8)

Linus Torvalds visits Google to share his thoughts on git, the source control management system he created.