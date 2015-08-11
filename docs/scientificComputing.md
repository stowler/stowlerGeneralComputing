# Skills for Scientific Computing

_Below I recommend some self-paced training resources, including [Lynda.com][] on-line video courses. New Lynda.com members can sign-up for a free 10-day trail, and won't be charged if they remember to cancel their account before the end of the trail. If a little more time is needed there is a $35 month-to-month rate available._

Contents
=================

  * [Getting started with unix (10 hours)](#getting-started-with-unix-10-hours)
  * [Getting started with git (2 hours)](#getting-started-with-git-2-hours)
  * [Getting started with MATLAB (1.5 hours)](#getting-started-with-matlab-15-hours)
  * [Getting started with R (?? hours)](#getting-started-with-r--hours)
  * [Getting started with Amazon Web Services (?? hours)](#getting-started-with-amazon-web-services--hours)


Users who are going to work directly with neuroimaging data will want a few specific computing skills in addition to understanding their lab's brain imaging software:

1. A working knowledge of **unix** and **git** will allow users navigate the file system, write scripts, and get work done in most neuroimaging environments.  
2. Though there is [plenty](http://www.nitrc.org) of neuroimaging software already written and freely available, learning a little **R** and **MATLAB** will allow users to read, interpret, and install other authors' code.
3. If users need to work in a cloud environment or would like to create their own infrastructure, they may also want to learn how to setup and maintain linux virtual machines on **Amazon Web Services.** 


# Getting started with unix (10 hours)

Working independently with most neuroimaging data requires fluent use of the unix command line, as well as the ability to read and understand shell scripts.  In less than ten hours the initial training for these skills can be completed through three Lynda.com courses **(below)**. 

Once initial training is completed users will want to maintain and extend their new skills. My experience training undergrads, grad students, and young investigators has convinced me that most users have a hard time maintaining fluency if they spend fewer than ten hours per week exercising their new skills. Does that sound like a suspiciously round number? Then pick your own starting point and titrate hours per week up or down until you find the limits of your retention. It's just like learning a new spoken language: give yourself _at least_ the amount of exposure needed to prevent the loss of your newly acquired skills.

## Unix basics

**6 h 35 min:** 

Search Lynda.com for the course titled **"Unix for Mac OS X Users"**. It covers the basics of getting work done on unix, linux, and unix-like systems. The title is a bit of a misnomer: the course is suitable even for users who do not currently use Mac OS X, and is relevant for linux-based servers and workstations.

## Editing text

**57 min or 33 min:** 

Users will want to become comfortable using a text editor that doesn't require a graphical user interface (GUI), because text files and scripts frequently need to be edited within an ssh session or under other circumstances that render GUIs impractical. I recommend that users who touch-type learn the free text editor named [vim][] (nee vi). Search Lynda.com for the course titled **"Up and Running with VI"**, which is 57 minutes. 

For users who don't touch-type, or for whom the vim learning curve too steep, I recommend learning the less powerful but also widely-available free text editor called [nano][]. Search Lynda.com for **"Up and Running with Nano"**, which is 33 minutes.

[vim]: http://www.vim.org/others.php
[nano]: https://en.wikipedia.org/wiki/GNU_nano

## Bash scripting

**1 h 25 min:** 

Bash scripting allows users to take what they learned about using the command line in the first course and extend that knowledge to write, edit, and debug scripts. Search Lynda.com for the course titled **"Up and Running with Bash Scripting"**

[Lynda.com]: http://www.lynda.com

# Getting started with git (3 hours)

[Git][] is an important free software package for managing the code you write: it allows the tracking of changes that have been made to code, and facilitates merging, branching, and other manipulations of code versions. [Github.com][] provides free code hosting services to support the sharing and management of git-tracked code. Most users will first encounter git and github.com when downloading existing code that another author has shared via github.com, but it doesn't take much time to learn to track and share your own code.

**90 min:**

Lynda.com's **"Fundamendals of Software Version Control"** is a great introduction to the concepts important for understanding version control, as well as the mechanics of using git. It's about 90 minutes of video if you skip the sections 4, 5, and 6, which are about git alternatives.

**51 min:**

Github's **[July 2013 webcast][]** provides a reasonable introduction to the mechanics of using git with github. I recommend starting at the 9:10 mark.

Users may want to continue their learning by browsing the Github [Bootcamp][] webpage, which has a written step-by-step guide to  getting started with git and github. It also links to a page with a list of [other resources][] for learning git.

Finally, the free ebook ["Pro Git"][] is a particularly good resource for learning git. 

[Git]: https://git-scm.com
[Github.com]: http://github.com
[Bootcamp]: https://help.github.com/categories/bootcamp/
[other resources]: https://help.github.com/articles/good-resources-for-learning-git-and-github
[July 2013 webcast]: https://www.youtube.com/watch?v=U8GBXvdmHT4
["Pro Git"]: https://git-scm.com/book

# Getting started with MATLAB (1.5 hours)

**90 min:**

[MATLAB][] is a commercial programming language and point-and-click development environment that users can use to write their own neuroimaging analysis code, as well as run community-provided packages like [SPM][] and [GIFT][]. At minimum users will want to be able to read, interpret, and install other authors' code. Search Lynda.com for the course titled **"Up and Running with MATLAB"**.
[MATLAB]: http://www.mathworks.com/products/matlab/ 
[SPM]: http://www.fil.ion.ucl.ac.uk/spm/
[GIFT]: http://mialab.mrn.org/software/



# Getting started with R (?? hours)

TBD


# Getting started with Amazon Web Services (?? hours)

TBD

