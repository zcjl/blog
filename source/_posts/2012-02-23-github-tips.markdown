---
layout: post
title: "关于Github使用的一些技巧"
date: 2012-02-23 21:55
comments: true
categories: git github
---

* test1
 * test2
  * test3 
     * test4
		* test5

#### Global setup:
[Set up git](http://help.github.com/set-up-git-redirect)
	git config --global user.name "zcjl"
	git config --global user.email zcjl516@gmail.com
      
#### Next steps:
	mkdir zcjl
 	cd zcjl
	git init
	touch README
	git add README
	git commit -m 'first commit'
	git remote add origin git@github.com:zcjl/zcjl.git
	git push -u origin master
      
#### Existing Git Repo?
	cd existing_git_repo
	git remote add origin git@github.com:zcjl/zcjl.git
	git push -u origin master
      
#### Importing a Subversion Repo?
[Click here](https://github.com/zcjl/zcjl/imports/new)
      
#### When you're done:
[Continue](https://github.com/zcjl/zcjl)

<br><br>
#### Instructions for setting up [username.github.com]() *  
  Create a repo named [username.github.com]() <br>
  Push a `master` branch to GitHub and enjoy!

#### Instructions for setting up [username.github.com/repo-name]() *
```
  Caution: make your working directory clean before you do this (either stash or commit),
  otherwise this will lose any changes you've made to your project since the last commit.
```

	cd /path/to/repo-name
	git symbolic-ref HEAD refs/heads/gh-pages
	rm .git/index
	git clean -fdx
	echo "My GitHub Page" > index.html
	git add .
	git commit -a -m "First pages commit"
	git push origin gh-pages


WARNING: All pages (even those created on private repos) will be publicly viewable

* It may take up to 10 minutes to activate GitHub Pages for your account
