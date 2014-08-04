---
layout: blog
title: Must-have tools for a Technology Startup
summary: A list of tools which you should consider start using on day one.
---

When we started in July 2011, we had a lot of disrespect for processes and tools. We just wanted to write code, build products and ship. However, the initial enthusiasm died after an year or so. As the team grew in size, collaboration became difficult. we started investing in tools, which would allow developers to collaborate and build products faster and better.

Here are some of the tools I would recommend for anyone starting up:

+ Bug/Defect Tracking - We started with [Redmine](http://www.redmine.org). Installation was a breeze thanks to packages available in Debian "squeeze" repositories. Redmine aims to be an all-in-one tool, with integrated Wiki, SCM viewer etc. Truth be told, Redmine is not the best defect tracking tool out there. It is a painful tool to use. To change the assignee of a defect, you will have to modify the defect and it will show you a big form with all the fields in it. Then, plugins available are not the best in the world. However, it has one advantage, it comes with the source code, which you can modify to suit your needs. However, you would like your team to code your product and not add code to a Bug Tracker.

    We eventually looked at other tools and stumbled on [Jira](http://www.atlassian.com/software/jira). They have a 30-day trial on their site, which we signed up for. We liked what we saw, changing any field a defect is a one-click affair. Also, at a price of $ 10 for 10 users, Jira is as good as free. Prices increase when you add 11th user, which is fine. As Joel Spolsky asks in his [Joel Test](http://www.joelonsoftware.com/articles/fog0000000043.html) - Do you use the best tools money can buy? I can not agree more.

+ SCM - If you are starting up now, use [Git](http://git-scm.com). Period. We use Atlassian [Stash](http://www.atlassian.com/software/jira) for this, which is a Git repository management software from the makers of Jira. Apart from managing the basics, it add light-weight code reviews to the mix and integrates well with Jira.

+ Continuous Integration - We use [Jenkins](http://www.jenkins.org). Jenkins integrates nicely with Stash as well, so that we can know in Stash, which built was successful in Jenkins and which was not. Jenkins builds and deploys our code to test environments, builds our Windows installers and checks for build fails, if any.

+ Wiki - Well, I needed a Wiki which does not use a database. [MoinMoin](http://moinmo.in) fits the bill. It is very simple to install and easily extensible. We use it for everything, from documenting release notes to writing full installation manuals.

If you have read this till here, please add any tool you think is worth sharing.