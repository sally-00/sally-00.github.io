---
layout: post
title: Setup this website from zero using template with Jekyll and github pages
date: 2022-02-07 17:39:00
description: website memo
tags: website, Jekyll, GithubPages
---

## Fork the theme and create repo
first [fork](https://guides.github.com/activities/forking/) the theme from `github.com:alshedivat/al-folio` to `github.com:<your-username>/<your-repo-name>`
Change repo name to `<your-username>.github.io` 

## Install ruby using rbenv

install ruby(using rbenv for managing ruby gems) and bundler
basic information and installation of rbenv: [https://github.com/rbenv/rbenv](https://github.com/rbenv/rbenv)

I installed using brew:
```bash
$ brew install rbenv
$ brew upgrade rbenv ruby-build
```
Set up rbenv in the shell and verify the setup of rbenv using the following commands.
```bash
$ rbenv init
$ curl -fsSL https://github.com/rbenv/rbenv-installer/raw/main/bin/rbenv-doctor | bash
```
But got error saying: Checking for rbenv shims in PATH: not found

Tried adding 'eval "$(rbenv init -)"' to ~/.bash_profile:
```bash
$ source ~/.bash_profile
$ echo 'eval "$(rbenv init -)"' >> ~/.bash_profile
```
Did not work… Realized that I'm using zsh, not bash!!!
Add the following lines to /Users/<username>/.zshrc
```
eval "$(rbenv init -)"
export RUBY_CONFIGURE_OPTS="--with-openssl-dir=$(brew --prefix openssl@1.1)"
```
checked again with:
```bash
$ curl -fsSL https://github.com/rbenv/rbenv-installer/raw/main/bin/rbenv-doctor | bash` 
```
All working fine now! 

Install the latest stable version of Ruby using rbenv:
(参考：[Qitta: rbenvでrubyのバージョンを管理する](https://qiita.com/hujuu/items/3d600f2b2384c145ad12))

```bash
$ rbenv install 3.1.0
```
Got error… error including the following:
BUILD FAILED (macOS 12.1 using ruby-build 20220125) In file included from compile.c:40: ./vm_callinfo.h:216:16: error: use of undeclared identifier 'RUBY_FUNCTION_NAME_STRING'     if (debug) rp(ci);  

Tried the following:
```bash
$ RUBY_CFLAGS=-DUSE_FFI_CLOSURE_ALLOC rbenv install 3.1.0
```
Did not work for me…
Some are saying about updating the command line tools. So:
（わからんけど，一応コマンドラインツールを再インストールしてみる．[Qiita: rbenvでrubyをインストールできなかったのでメモ](https://qiita.com/marusho_summers/items/1022d5bbfd2f7856d2f8)）
```bash
$ sudo rm -rf /Library/Developer/CommandLineTools
$ xcode-select --install
```

Did `$ rbenv install 3.1.0` again and it worked!!
Check the version:
```bash
$ which ruby
```
If it shows the system's ruby version, we need to switch the version.
```bash
$ rbenv global 3.1.0
```
Now install ruby bundler.
```bash
$ gem install bundler
```

Couldn't do that because not permitted. When checking the version again, the path is still on the system side. The switch of the version was not successful!?

To set ruby path to rbenv, add the following to shell setting file(.bashrc or .zshrc)．
([Qiita: gem installでpermissionエラーになった時の対応方法](https://qiita.com/nishina555/items/63ebd4a508a09c481150))

```bash
[[ -d ~/.rbenv  ]] && \
  export PATH=${HOME}/.rbenv/bin:${PATH} && \
  eval "$(rbenv init -)"
```

check version using `which ruby` and `which gem` to make sure the path is on the rbenv side. Do installation again:

```bash
$ gem install bundler
```
Working now!!

## Back to setting up the theme

Use the following to clone repo to local and execute to see the website
```bash
$ git clone git@github.com:<username>/<username.github.io>.git
$ cd <username.github.io>
$ bundle install
$ bundle exec jekyll serve
```
After `$ bundle exec jekyll serve`, we can access the website through `http://127.0.0.1:4000`. Edits you made to the contents will be applied to it in real-time.

Edit the contents of the website and push to git. Then deployment will be triggered automatically. You should be able to access the website through `https://<username>.github.io` in a few minutes after the whole process is done.

Make sure you did the following to ensure proper deployment:
- In git repo setting, pages, set source branch to gh-pages (not master).
- In the file `_config.yml`, set `url` to `https://<your-github-username>.github.io` and `baseurl` to `/<your-repository-name>/`

↑ If you don't do this properly, the website will display well in the local but wired on the online website.
これちゃんとできなかったら，ローカルではちゃんと表示されるけど，ウェブサイトでは変になる．

I had the problem of pictures not being displayed in `http://127.0.0.1:4000`, but no problem on the `https://<username>.github.io`. It turned out that imagemagick was not installed. Used brew to install and then the pictures were generated with no problem:
```bash
$ brew install imagemagick
```


## Folder structure
Read: [https://jekyllrb.com/docs/structure/](https://jekyllrb.com/docs/structure/)

`_posts` : naming of the file must follow `Year-Month-Day-title.md`

`_pages` : manage what pages are appearing (about, blog, projects, publications, teaching)

`_news` : put news/announcements here

`_posts` : put posts for blog here

`_projects` : put projects here

## Finding website through Google search
I could not reach my website through searching my name and some keywords…
Turned out the reason was that Google has not indexed my website yet which is common with brand new websites.
You can check by searching `site:<your_site_address>`

