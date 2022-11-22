---
title: Getting Started with Jekyll
date: 2019-04-03 17:51:42
tags:
  - static site generator
  - ruby
  - markdown
category: tech
keywords:
  - jekyll
  - ruby
  - github pages
  - static site generator
  - markdown
---

## What is Jekyll?

Jekyll is a [static site generator](/tags/static-site-generator). It takes your content, renders Markdown and Liquid templates, and spits out a complete, static website ready to be served by Apache, Nginx or another web server. You can even host your site for free on GitHub Pages.

### what _language_ is jekyll written in?

**Jekyll** is written in **Ruby**.

## Installing ruby

### Windows

1. Download and install [Ruby+Devkit](https://rubyinstaller.org/downloads/).
2. Run `ridk install` to install the Devkit and install all components.
3. To check if ruby is installed, run `ruby -v` and `gem -v` in the command prompt.

**Note**: If `ruby` is not recognized as a command, you may need to add the ruby bin directory to your PATH environment variable.

- Go to `ruby/bin` directory, by default it is `C:\Ruby27-x64\bin` if you installed it in the default directory. Copy the path.
- Open the Control Panel, click System and Security, then click System.
- Click Advanced system settings on the left and then click Environment Variables.
- Under System variables, click Path, then click Edit.
- Click New and paste the path you copied earlier.
- Click OK to save the change.

## Installing Jekyll

1. Run `gem install jekyll bundler` to install Jekyll and Bundler.
2. Run `jekyll -v` to check if Jekyll is installed.

### Jekyll Structure

<!-- Create a jekyll structure -->

```bash
./
├── _config.yml
├── _drafts/
│ ├── begin-with-the-crazy-ideas.textile
│ └── on-simplicity-in-technology.markdown
├── _includes/
│ ├── footer.html
│ └── header.html
├── _layouts/
│ ├── default.html
│ └── post.html
├── _posts/
│ ├── 2007-10-29-why-every-programmer-should-play-nethack.textile
│ └── 2009-04-26-barcamp-boston-4-roundup.textile
├── _data/
│ └── members.yml
├── _site/
└── index.html
```

### How to create a new post in jekyll?

1. Create a new file in `_posts` directory.
2. The file name must be in the format `YYYY-MM-DD-title.md`.
3. Add the following front matter to the top of the file:

```yaml
---
title: "Title of the post"
date: YYYY-MM-DD HH:MM:SS +/-TTTT
tags:
  - tag1
  - tag2
category: category
keywords:
  - keyword1
  - keyword2
---
```

4. Write the post in **markdown**.

### what is `markdown`?

`Markdown` is a lightweight `markup language` with plain text formatting syntax. It is designed so that it can be converted to HTML and many other formats using a tool by the same name.

- [My Markdown Cheatsheet](https://github.com/adam-p/markdown-here/wiki/Markdown-Cheatsheet)

## Creating a new Jekyll site

1. Run `jekyll new my-awesome-site` to create a new Jekyll site.
2. Run `cd my-awesome-site` to go to the site directory.
3. Run `bundle exec jekyll serve` to start the Jekyll server.
4. Open `http://localhost:4000` in your browser to see the site.

## Creating a new post

1. Run `bundle exec jekyll post "My New Post"` to create a new post.
2. Open the post file in your text editor.
3. Add the following front matter to the top of the file:

   ```yaml
   ---
   title: My New Post
   date: 2019-04-03 17:51:42
   tags:
     - tag1
     - tag2
   category: category
   keywords:
     - keyword1
     - keyword2
   ---
   ```

4. Write your post in Markdown.
5. Save the file.
6. Run `bundle exec jekyll serve` to start the Jekyll server.
7. Open `http://localhost:4000` in your browser to see the site.

   **Notes**:

   - If you want to use a different date for the post, you can use the `--date` option when creating the post. For example, `bundle exec jekyll post "My New Post" --date 2019-04-03`.
   - If you want to use a different port, you can use the `--port` option when starting the server. For example, `bundle exec jekyll serve --port 3000`.

## Creating a new page

1. Run `bundle exec jekyll page "My New Page"` to create a new page.
2. Open the page file in your text editor.
3. Add the following front matter to the top of the file:

```yaml
---
title: My New Page
date: 2019-04-03 17:51:42
tags:
  - tag1
  - tag2
category: category
keywords:
  - keyword1
  - keyword2
---
```

4. Write your page in Markdown.

   **Note**: If you want to create a page that is not in the navigation menu, add `nav_exclude: true` to the front matter.

5. Save the file.
6. Run `bundle exec jekyll serve` to start the Jekyll server.
7. Open `http://localhost:4000` in your browser to see the site.

## Questions

- [ ] Is it possible to serve multiple Jekyll sites locally?

<!-- Qoute an answer from stackoverflow -->

> Yes, you can use the `--port` option to serve multiple sites on different ports. For example, `bundle exec jekyll serve --port 3000` will serve the site on port 3000. You can then serve another site on port 4000 by running `bundle exec jekyll serve --port 4000`.

**reference**: [stackoverflow](https://stackoverflow.com/questions/20155944/is-it-possible-to-serve-multiple-jekyll-sites-locally) question by [Brian Zelip](https://stackoverflow.com/users/2145103/brian-zelip)

## Jekyll cheatsheet and documentation

- [Jekyll Cheatsheet](https://devhints.io/jekyll)
- [Jekyll Documentation](https://jekyllrb.com/docs/)

**reference**:

- [Jekyll on Windows](https://jekyllrb.com/docs/installation/windows/)
- [Step by Step Tutorial](https://jekyllrb.com/docs/step-by-step/01-setup/)
- [Jekyll Cheat Sheet](https://devhints.io/jekyll)
- [Jekyll Configuration Options](https://jekyllrb.com/docs/configuration/options/#serve-command-options)
