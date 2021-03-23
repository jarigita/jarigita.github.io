---
title: Create a personal blog with github pages and jekyll.
header:
  overlay_image: assets/images/githubpages.gif
  caption: "debateops"
categories:
  - github
tags:
  - github
  - blog
  - jekyll
---

# We use github pages and jekyll to create static personal and project documentation.

## Should I Start a Blog?

We want to create a personal blog, where we can store all those notes, those things to remember that we never remember later.
<br>
On the internet there are a lot of pages that tell you how things are done, but it is always a good idea, if you have already done something, write it down, because in a few days, when a colleague asks for it, or when you need it again, being able to remember it and that it takes little time to solve it, or simply, not having to search the internet again for what you have already searched for before.
<br>
The first and most important thing to store is code, scripts and in any case we want to handle all things as if it were code, and since we already have projects stored in github, our idea is to take advantage of github and the opportunity it offers us with giyhub pages to have a static web.

### Alternatives

The choice of tools is crucial, because we want to make little effort (fast, easy and simple), reuse and / or use markdown which is what we already use for project documentation.
<br>
The first thing is to know which repository to use. The alternatives:

- Google Cloud Source Repositories is from Google and is convenient if you want to integrate with other google tools or if you want to access several different repositories (including bitbucket and github)
- Bitbucket It is from Altassian, and is convenient if you want to integrate with Jira, Trello or other Altassian products.
- GitHub  It is the market leader, I have been having projects on github for several years without problems, so I have no reason to change.

We want the documentation to be together with the code, all in the same place, but to be accessible from the web in an easy way. The most obvious option is to use github pages and use jekyll, but we see alternatives.

- Hugo done in go, it is advertised as the fastest.
- Hexo It is node, growing community, very popular in China.
- jekyll is Ruby created by Github, for large websites it can get slow.

As we have opted for github, the web is not going to be very big and we want simplicity, easy to use, we will stick with jekyll and github pages, if we grow a lot and see problems , [we would go to Hugo and Netlify](https://pawelgrzybek.com/from-jekyll-to-hugo-from-github-pages-to-netlify/).

## We start with github
LThe first thing is to create a personal account to host the blog.
<br>
You must have a github account or create one.

It is necessary to create a repository with the name <user> .github.io that will show the documents under the link  http://usuario.github.io
That is where the pages will be hosted, as we want several languages, we create another repository called es, to contain the documents in Spanish and its link will be http://usuario.github.io/es
<br>
This part can be configured in github /settings
![settings github](/assets/images/github_settings.png)


## We start with jekyll

### how to install jekyll

I use ubuntu and to install ruby
```script
sudo apt-get install ruby-full build-essential zlib1g-dev
```
then you can install jekyll
```script
gem install jekyll bundler

```
we check the installed version
```bash
$ jekyll -v
jekyll 4.2.0

```
[Information for windows](https://www.kiltandcode.com/2020/04/30/how-to-create-a-blog-using-jekyll-and-github-pages-on-windows/)

### Start with the first basic blog

Create an empty directory and execute:
```bash
jekyll new jekyll-site
```
It creates a directory called jekyll-site with the following files with a structure 
```
jekyll-site/
  _posts/
  index.markdown
  about.markdown
  _config.yml
  Gemfile
  404.html
```
- _posts It is the place where the post / markdown will be left)
- index.markdown is the initial page, it can be modified, but better later.
- about.markdown is the documentation about the blog, or if it is a personal blog details of the creator.
- _config.yml configuration file, in which we indicate blog title, email, twitter github account, the fixed data that will be displayed on the basic web
<br>
we modify the _config.yml data and raise the server

```bash
cd jekyll-site/
$ bundle exec jekyll serve
Generating... 
       Jekyll Feed: Generating feed for posts
   Server address: http://127.0.0.1:4000/
  Server running... press ctrl-c to stop.
```
we connect to http://127.0.0.1:4000/
![Initial Start in jekyll](/assets/images/initial_jekyll.png)

Once created, just add new posts, a new markdown in the _post folder 

### We choose the aspect and theme of the web
Now that we know how it works, we are going to create the real blog, for this the first thing is to choose the theme, define what aspect, navigation the web is going to have, define the graphic aspects, and then only dedicate ourselves to creating markdown with post.
<br>
We can see the [default themes that github pages supports] (https://pages.github.com/themes/)
But there is the possibility of adding themes remotely, [possible themes](https://jekyllthemes.io/github-pages-themes)
<br>
We look at themes with photos, compatibility with github, free and we look for examples of blogs created with that theme, which can be seen on github and github pages.
<br>
We like several but looking with real examples in use there are less, in the end, we are left with https://github.com/mmistakes/minimal-mistakes
<br>
example web pages
- https://zenglix.github.io en [github](https://github.com/zengliX/zengliX.github.io)
- https://yxtay.github.io en [github](https://github.com/yxtay/yxtay.github.io)

as information to add more attractive things to the [posts](https://github.com/mmistakes/minimal-mistakes/tree/gh-pages-3.1.6/_posts)
<br>
As navigation we want to create a link and special page for a project (add a link in the menu and a fixed page with the general index), and add photos to the posts (not just text), each post must have a photo in the head and that same photo will be used in the post listing. To facilitate this and not have to be taking photos continuously, there will be at least one photo per category, and we will define the basic categories that we are going to have, so by default the photo of the category will be placed.

### Modifications on the web
We create two fixed pages apart from the posts
in the _pages folder
- about.md  we incorporate the Curriculum Vitae and some more information.
- [debateops.md](https://github.com/jarigita/jarigita.github.io/blob/main/_pages/debateops.md) explanation of the project and index
<br>
We also want to have an external link to redirect to the personal web but in another language, just add an external link in the navigation.
<br>
To add them in each post, the link ** permalink: / DebateOps / ** is indicated and they are added to the navigation index
in ** _ data / navigation.yml ** you have to put

```html
main:
  - title: "About"
    url: /about/
  - title: "DebateOps"
    url: /DebateOps/
  - title: "english"
    url: https://jarigita.github.io/

```
81 / 5000
Resultados de traducción
We test locally, we see that the links come out and it redirects us to the static page
<br>
Now we want to get the list of posts together with a photo.
<br>
To do this you have to create another page with the post list
in _pages we create another page ** blog_page.md **
```html
---
title:  "Blogs"
layout: archive
permalink: /Blogs/
author_profile: true
comments: true
---

  % for post in site.posts %
    <figure>
      <a href="{{post.url}}"><img src="/{{post.header.overlay_image}}" alt="{{post.title}}"></a>
    </figure>
    % include archive-single.html %
  % endfor %
```
In permalink we indicate the link that you will have
<br>
We make a loop through all the posts on the web putting a figure (image) and the basic simple file of each post (the same one created by default)
<br>
It only remains to link the navigation
in ** _ data / navigation.yml ** you have to put
```
main:
  - title: "Blogs"
    url: /Blogs/
```

For the image to be displayed, each post must have in its header a title (title) and a header image that we are going to lengthen the entire width of the page.
<br>
That is, it is mandatory that each post has a header
```
---
title: Debateops. Why a blog.
header:
  overlay_image: assets/images/debateops.gif
  caption: "debateops"
categories:
  - debateops
tags:
  - debateops
  - agile
  - devops
---

```
- **title** It is the title of the post (it will be overwritten in the image)
- **header** with an elongated image and a caption (in each post it will appear in the header and in the list of posts as well) 
- **categories** at least indicate a category the post, and if it does not have an image put the category
- **tags** specify at least a tag (the category) to facilitate the search of the post

### Multiple languages
The option chosen to have several languages has been to create two totally similar static websites.
<br>
Esto nos permite tener la web de cada idioma independiente, no es obligatorio subir a la vez los post en ambas ni que sean los mismos exactamente. Nos permite no mezclar busquedas en varios idiomas, personalmente si busco en español prefiero que me salgan las cosas en español a duplicarse la misma información en varios idiomas.
<br>
This allows us to have the website of each language independent, it is not mandatory to upload the posts in both at the same time or that they are exactly the same. It allows us not to mix searches in several languages, personally if I search in Spanish I prefer that things come out in Spanish to duplicate the same information in several languages.
<br>
Nor is it necessary to indicate translations and have lists of multiple languages.

## conclusion
To see the result of all these posts is my personal website [jarigita](https://jarigita.github.io/) and the code [github](https://github.com/jarigita/jarigita.github.io)
<br>
I have found it very useful and convenient to show the same documents that were already created in markdown in a more web-friendly way, it is like having a technical view (code) and a tutorial view (web).
As an ease to upload post and maintain it, being the same as the code, markdown and using git and its versions, it is very easy.
<br>
Graphic aspect, for me it is enough, it is not a professional blog, only a set of technical notes, so I prefer simplicity and to the point, it looks good and it is quick to handle.
<br>
Regarding the uploads of changes, the time between deployments and that it is seen effectively on the web varies from one time to another, so it is better to deploy, start doing something else and then check, it is a but, as it is not free either we are going to complain.
<br>
It does not seem so easy to modify the appearance, the basic operation is very good, but if you start to change the aspect or go into more low detail, it is no longer so simple or so easy. If you make a mistake, github pages sends an email in which it only indicates the line

```
The page build failed for the `main` branch with the following error:

You have an error on line 16 of your `_config.yml` file. For more information, see https://docs.github.com/github/working-with-github-pages/troubleshooting-jekyll-build-errors-for-github-pages-sites#config-file-error.

For information on troubleshooting Jekyll see:

  https://docs.github.com/articles/troubleshooting-jekyll-builds
```
For me, I want something quick and simple, better to adapt to the basics, if you want something more striking perhaps explore other alternatives.
<br>
I recommend and find my very useful github page with jekyll. 

## For more information

[Jekyll on Ubuntu](https://jekyllrb.com/docs/installation/ubuntu/) como instalar jekyll en ubuntu

[jekyll-docs](http://jekyllrb.com/docs/home) documentos oficiales de jekyll
[jekyll-gh](https://github.com/jekyll/jekyll) proyecto github de jekyll
[jekyll-talk](https://talk.jekyllrb.com/) 

[minimal-mistakes jekyll theme](https://jekyllthemes.io/theme/minimal-mistakes)

[examples of posts ](https://github.com/mmistakes/minimal-mistakes/tree/gh-pages-3.1.6/_posts)

[Best Git Repositories: Google vs. Bitbucket vs. GitHub](https://www.upwork.com/resources/best-git-repository-google-github-bitbucket)

[From Jekyll to Hugo! From GitHub Pages to Netlify!](https://pawelgrzybek.com/from-jekyll-to-hugo-from-github-pages-to-netlify/)

[Jekyll vs. Hugo vs. Hexo](https://www.techiediaries.com/jekyll-hugo-hexo/)
