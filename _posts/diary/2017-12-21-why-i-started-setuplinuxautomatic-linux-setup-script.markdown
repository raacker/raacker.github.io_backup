---
layout: post
title: "Why I started setup_linux(automatic linux setup script)"
date: "2017-12-21 15:54:29 -0800"
location: "San Diego, CA"
commentIssueId: 30
category: Diary
tags: [study, linux]
---

<h3>WARNING!</h3>

It's not about totally cool, amazing, hipster-like scripts that magically build and setup whole things for your linux. Completely for my own and customized for my develop environment. And I'm writing down this post to inspire(if you get inspired, awesome) other people to do these if they have similar problems :)

It goes back to Feb 19, 2016. I read some article [내맘대로 쓰는 vim 플러그인과 .vimrc 설정](http://luckyyowu.tistory.com/308), [vim 플러그인 매니저, Vundle + NERDTree 플러그인 설치하기](https://ansuchan.com/install-vundle-and-nerdtree/) (Sorry, they are Korean postings. Just they are about how to customize vim with PluginManager and Vundle) and I tried to make mine. But just writing .vimrc on my Evernote was not enough. I had to open gedit and copy and paste... annoying! So I wanted to store .vimrc on online storage and at that time, I'd just learned how to use git and github. That's how [setup_vim](https://github.com/raacker/setup_vim) started.

After I uploaded my .vimrc file, I was easily get annoyed by manual stuffs, like install all the libraries that I need, run :PluginInstalls command.. every time. And I had to write all instructions down on somewhere. I began to find better way to solve this problem and it was 'bash shell' script! with bash shell script, just write bash commands what I have to do manually and give permission to run it.

Maybe because I'm lazy ;p but the reason was same as why I'm doing this blog, **to write down what I learn and use it as my personal memory archive**.

Anyway, I've been maintaining the repository for 2 years. It doesn't have big updates usually but still have been really good tools to setup my vim plugins and other stuffs too. Even for my friends. 'cause they really liked cool vim features.

And Jul 30 2016, I wanted to do similar thing for my blog setup, installing jekyll and atom. Did same stuff as my previous repo, [setup_blog](https://github.com/raacker/setup_blog), and also created for python [setup_python](https://github.com/raacker/setup_python).

Okay, now let's go back to this year. When I was preparing my internship, during the 3 months remote period, I did android stuff. And after June, I had to work on Flask and needed to setup my another virtual linux only for flask. I built another linux mint 17.1 and perfectly setup whole things and after all, made ova file to put on google drive because I had to change my laptop in short time. Can you catch the point where I get bored again? yes I had to setup my linux manually and there were several stuffs to do.

A few days ago, I updated my linux mint ova file and made a repository, [setup_linux](https://github.com/raacker/setup_linux). Yes, this is the long story how setup_linux script started. I made setup_web to setup flask automatically and put all my favorite alias on setup_linux.

These scripts are not only solving my laziness(not actually) but also memos what commands I need for specific stuffs and what I can never forget to setup my development environment.
