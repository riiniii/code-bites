---
title: "Creating a CLI Tool"
date: "2021-11-08T07:26:03.284Z"
description: "Notes on general guidelines for when you create a CLI tool."
categories: [CLI]
comments: true
---

I've recently come across the need to create a script to generate seed data for a project. I wanted developers to be able to run this script by providing the tables they wanted to populate and a json file that had the details for each row of the table(s).

While writing the script, I realized that I had no clue on best practices on how to write this CLI! I felt at the very basic level I could implement encapsulation - providing an easy to use CLI but not letting developers worry about the implementation details. I also wanted developers to be able to control certain settings through flags, but is there a well known interface (like [RESTful API](https://www.redhat.com/en/topics/api/what-is-a-rest-api) interfaces?) that I could use?

The following writing contains my findings on best practices for designing a CLI.

### The Basics

1. Use a command line parsing library when you can
2. Return zero exit code on success, non-zero on failures.
3. Send output to stdout (or your equivalent in your environment)
   1. what's the equivalent in javascript?
4. Send messaging to stderr (so that log messaging, errors will all go to one place and not be fed to the next command)
   1. what's the equivalent in javascript?
5. when passed no options, -h, or the—help flag, return a description of what your program does, one or two examples of invocation, description of flags, and where to go for more information.
   1. don't overload -h
   2. show most common flags
   3. use formatting in your help text

### General Tips

1. Show progress visually & in an easily readable way
2. Create a reaction for every action
3. Create human readable output (errors, action results, progress info, etc.), have a good signal-to-noise ratio
4. Support your skim-readers - keep things succinct!
5. Suggest next best step
6. Consider your options and how you may suggest them for users who are missing some essential information
7. Provide an easy way out
8. Flags over args
   1. have a full length version of all flags (ex. -h and —help do the same things)
   2. see if you can use standard name for flags first
   3. make flag order independent if possible
   4. don't put private data (like token) in flags
9. consider offering documentation, whether it be via the web, terminal-based, or [man-pages](https://en.wikipedia.org/wiki/Man_page)
10. never require a prompt - allow for everything to be done in one line via flags
11. confirm with user before making a "big" change (ex. deleting a file, folder, or even an entire application)
12. on robustness,
    1. validate user input
    2. responsive is more important than fast
    3. show progress if something is taking a long time
    4. do stuff in parallel when you can, but be thoughtful about it
    5. make things time out
    6. make it idempotent
    7. make it crash only
    8. people will misuse your program 😢
13. future proofing your CLI
    1. make changes additive where you can (& ensure for backwards compatibility)
    2. warn before you make a non-additive change
    3. don't allow arbitrary abbreviations of subcommands, it'll take up future wording that you might actually want to mean something
    4. don't create a time bomb (aka don't rely on external dependency where possible)

Great articles from where I got my information:

1. [Command Line Interface Guidelines](https://clig.dev/) - a must read
2. [10 Design Principles for delightful CLIs](https://blog.developer.atlassian.com/10-design-principles-for-delightful-clis/)
3. [Heroku's CLI Style Guide Specifics](https://devcenter.heroku.com/articles/cli-style-guide)
4. [12 Factors for CLI Apps](https://medium.com/@jdxcode/12-factor-cli-apps-dd3c227a0e46)
5. [POSIX Utility Conventions](https://pubs.opengroup.org/onlinepubs/9699919799/basedefs/V1_chap12.html)
