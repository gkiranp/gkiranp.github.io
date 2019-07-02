---
layout: post
excerpt_separator: <!--more-->
title: "Essential software skills you need to master, beyond coding"
date: 2018-03-21
tags: skills software-development 
---

Learning is everyday life. Programming jobs are as hot as ever and there is no end in sight. If you are looking for a secure job with the flexibility to work online from anywhere, programming is the way to go. One of the best things about the field of computer programming is that the most popular programming languages can be learned online for free. Introductory programming courses are available for learning Java, Python, Perl, C++, and pretty much everything else. In addition to free online courses, there are hosts of websites dedicated to teaching you how to code. To add top programming skills to your resume, all you need is a computer, some dedicated time and the desire to learn. Here are few essential things you need to master, if you want to be on top of compitition. <!--more-->

**Git, GitHub and Pull Requests**
Git is a version control system. For example, if you have a file on which you’ve been working on and reworking for a long time, all the versions of it are saved in Git, and you can easily get back to every version.
The `Git` or any version control system has the following benefits:

	- You have access to all versions of all files in Git repository at any time, it’s almost impossible to lose any part of a code.
	- Multiple developers can work on one project at the same time without interfering with each other, and without fear of losing any changes made by a colleague. 
	In Git, the possibilities of collaborative work are unlimited.

You will have to use Git every day, and this is a tool you should have a perfect command of.
Although you can run your own Git server locally, `Github` is both a remote server, a community of developers, and a graphical web interface for managing your Git project. It’s free to use for up to 5 public repositories – that is, when anyone can view or fork your code – with low cost plans for private projects. I strongly suggest you go sign up for a free account so you can start playing around with your own projects or forking someone elses.

Below are the questions you should know how to..:
	- How do I merge or rebase my branch, and what is the difference?
	- How do I resolve conflicts? For example, mine versus theirs versus manual merge
	- What is a feature branch?
	- What is a pull request?
	- What are the different collaboration workflows in Git?

That’s it, and this is pretty straight forward.

[Try Git](https://try.github.io/levels/1/challenges/1) — an interactive introduction course on Git. If you study it closely and thoroughly you’ll know enough to perform usual tasks;
[Version control: best practices](https://www.rainforestqa.com/blog/2014-05-28-version-control-best-practices/) — an article on the best ways of using Git and Github;
[A Git Workflow for Agile Teams](http://reinh.com/blog/2009/03/02/a-git-workflow-for-agile-teams.html) — provides insight into the organization of work with Git repository for a team of three or more developers.

**The Agile Methodology**
The first thing a team needs to do when starting a project or a larger task is to split the job. Over the last 10 years, the “Agile” methodology replaced the traditional waterfall planning. Agile methodology has taken the software development world by storm and rapidly cemented its place as “the gold standard.” Agile methodologies all started based on four core principles as outlined in the Agile Manifesto. These methodologies are rooted in adaptive planning, early delivery and continuous improvement, all with an eye toward being able to respond to change quickly and easily. The Agile manifesto is [here](http://agilemanifesto.org/).
Practically speaking it says “let’s not plan too much ahead, because inputs and assumptions we have today about the project will change”. This is almost always true, and nowadays there is hardly any team under the sun that is not (sometimes self-proclaimed) “Agile”.
In Agile, a software project will be split into tens or hundreds of tasks. You need a tool to manage them. The reference tool is [JIRA](https://www.atlassian.com/software/jira).

**Testing and Continuous Integration**
Git and agile tools allow teams to go fast. With speed inevitably come errors and bugs. Consider a team of five developers working on rather independent pieces of code. Each of them will make a pull request to the repository. Two problems can arise:

	- Once the code of the “first developer” gets to the Git repository, the code of the others is no longer valid or working because some things have changed. 
	This is not a mistake from “the first developer”, it is just life and it will happen.
	- Once all the developers pushed their code to the Git repository, chances that everything work as expected out of the box are rather low. 
	Again, this is not a reflection of poor teamwork. It will just happen.

Therefore, you need to test your software. Even after each developer has pushed their code? Yes, it would be great to do that so!
Automated tests and [Continuous Integration](https://www.martinfowler.com/articles/continuousIntegration.html) are there to the rescue.
Automated testing is a topic one could write many books about. Each language and framework has its own set of tools. Just keep in mind that testing is time consuming and not always planned for. Regardless, you should know how to write unit tests for your code and be proactive about writing them.

Continuous Integration is a process in which every push to your repository triggers a build and runs your tests automatically. A red flag is raised as soon as a faulty commit goes in. Pull requests should also be tested automatically before merging to avoid bugs that impact the whole team. Popular continuous integration server is [Jenkins](https://jenkins.io/).

I will keep post here if I come-up with any other skill-set, easy to learn and master about.