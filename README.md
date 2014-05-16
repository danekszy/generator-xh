XH Generator [![Build Status](https://travis-ci.org/xhtmlized/generator-xh.svg?branch=master)](https://travis-ci.org/xhtmlized/generator-xh) [![NPM version](https://badge.fury.io/js/generator-xh.svg)](http://badge.fury.io/js/generator-xh)
============

XH Generator is a [Yeoman](http://yeoman.io) generator for scaffolding front-end projects. XH is suitable for client work when you deliver a completed project to your client for further review and development.

XH Generator creates a project structure, files and Grunt tasks which support modern workflows like CSS preprocessors. Built HTML, CSS and JS files are prettified and fully editable so clients can work directly with them if they wish.

![Project index](docs/img/project-index.png)

## Table of contents

- [Features](#features)
- [Prerequisites](#prerequisites)
 - [Node.js](#1-nodejs)
 - [Sass](#2-sass)
 - [Grunt](#3-grunt)
 - [Bower](#4-bower)
 - [Yeoman](#5-yeoman)
 - [XH Generator](#6-xh-generator)
- [Usage](#usage)
 - [Project scaffolding](#1-project-scaffolding)
 - [Project structure](#2-project-structure)
 - [Adding pages to the project](#3-adding-pages-to-the-project)
 - [Development](#4-development)
- [Tips & Tricks](#tips--tricks)
 - [Working with files in the dist folder](#working-with-files-in-the-dist-folder)
 - [Writing styles](#writing-styles)
 - [Adding 3rd party dependency via Bower](#adding-3rd-party-dependency-via-bower)
- [License](#license)

## Features
- Custom project name
- Responsive project index with a list of pages / templates
- HTML includes to avoid code duplication
- A sub generator for adding pages to the project
- Industry standard [normalize.css](http://necolas.github.io/normalize.css/) as a base stylesheet
- CSS Preprocessing with [SCSS](http://http://sass-lang.com/) or [Less](http://lesscss.org/)
- Optional [WordPress styles](http://codex.wordpress.org/CSS) for images and captions
- Optional libraries like [Bootstrap](http://getbootstrap.com/), [Modernizr](http://modernizr.com/) & [CSS3 Pie](http://css3pie.com/)
- Grunt tasks for prettifying built HTML / CSS / JS
- Auto generated table of contents in main.css
- Functionality for merging JS libraries to reduce number of HTTP requests
- Consistent coding style supported by [.editorconfig](http://editorconfig.org/)
- JavaScript code linting with [JSHint](http://www.jshint.com/)

## Prerequisites

The following software needs to be installed if you want to use XH Generator. These installations need to be done just once so you can skip this section if you have the software already installed.

(Note: As a command line replacement at Windows we recommend [ConEmu](https://code.google.com/p/conemu-maximus5/).)

### 1) Node.js

Install [Node.js](http://nodejs.org/) so you can work with `npm`, Node package manager.

### 2) Sass
If you want to use SCSS for CSS preprocessing (SCSS is a default option), you will need to install [Ruby](https://www.ruby-lang.org/en/installation/) and [Sass](http://sass-lang.com/install). Once Ruby is installed (on Mac it comes preinstalled), install the Sass preprocessor from the command line.

```
gem install sass
```

### 3) Grunt
Then install [Grunt](http://gruntjs.com/), JavaScript task runner, from the command line:

```
npm install -g grunt-cli
```

### 4) Bower
For managing certain dependencies like Bootstrap, you will need [Bower](http://bower.io/), another package manager. Install it from the command line too:

```
npm install -g bower
```

### 5) Yeoman
XH Generator is a [Yeoman](http://yeoman.io/) generator, so obviously it depends on it. You can easily install Yeoman with the following command:

```
npm install -g yo
```

### 6) XH Generator
Finally install the XH Generator:

```
npm install -g generator-xh
```

Congratulations, you are now ready to use XH Generator!

## Usage

### 1) Project scaffolding

To create a project with XH Generator, create a new folder, open a command line in it and type:

```
yo xh
```

You will be presented with a welcome screen and project scaffolding options. Answer the generator questions according your project needs.

![Project scaffolding](docs/img/scaffolding.png)

Once done, the generator will create the required files and folders and install all npm and Bower dependencies for you:

![NPM & Bower installation](docs/img/installation.png)

### 2) Project structure

The generated project structure will look like this:

![Project structure](docs/img/project-structure.png)

The meaning of files and folders are as follows:

- **dist** - production / preview files are automatically generated here, this is where you check your work in a browser. 
- **node_modules** - Node.js modules for various Grunt tasks, usually you don’t have to do anything about this folder
- **src** - source files, development is done here
 - **bower_components** - 3rd party libraries managed via [Bower](http://bower.io/)
 - **includes** - HTML partials like `head.html`, `scripts.html`, etc.
 - **scss / less** - SCSS or Less files
    - `main.scss` / `main.less` - main file where other stylesheets are imported
    - `_variables.scss` / `variables.less` - variables file
    - `_mixins.scss` / `mixins.less` - mixins file
    - `_common.scss` / `common.less` - common styles with some minimal default styling
    - `_wp.scss` / `wp.less` -  [WordPress styles](http://codex.wordpress.org/CSS) for images and captions (in WP projects)
 - **js** 
    - `main.js` is a main JS file in project
 - `home.html`, etc. - HTML files composed from HTML partials
- `index.html` - project index with project pages listed
- `Gruntfile.js` - [Grunt](http://gruntjs.com/) file with various automation tasks defined in it
- `bower.json` - Bower dependencies in the project
- `package.json` - npm packages dependencies
- `.yo-rc.json` - Yeoman generator configuration file
- `.bowerrc` - configuration file for Bower
- `.editorconfig` - [EditorConfig](http://editorconfig.org/) configuration file to achieve consistent coding style
- `.gitattributes` - [Git](http://git-scm.com/) configuration file to force Unix line ending in all text files
- `.gitignore` - default Git ignore files and folders
- `.jshitrc` - [JSHint](http://www.jshint.com/) configuration


On a typical project, you will work in `src` folder and check your work in `dist` folder so you don’t have to touch other files.

### 3) Adding pages to the project

Once you have basic project structure generated, you should add pages you will be working on. XH Generator comes with a subgenerator for adding new pages to the project. 

From the command line type:

```
yo xh:page “Page Name”
```

for example

```
yo xh:page “Home”
```

The command will do the following:

1. creates a HTML file for your page in `src` folder
2. adds a page name and link to the project index
3. creates a source SCSS or Less file for the page and adds an `@import` statement to `main.scss` or `main.less`
4. creates images subfolder for the page in `dist/img` folder

![Page added](docs/img/page-added.png)

When running the command, you will asked if `index.html` and `main.scss` (or `main.less`) should be overridden:

![Project index overwrite](docs/img/index-overwrite.png)

If you wonder what Yanxdh means in the above screenshot, it is:
- **Y:** Yes (Default)
- **n:** No
- **a:** Yes to this question and all others.
- **x:** Abort
- **d:** Show the differences between the old and the new file
- **h:** Help, list all options

Confirm overwriting the both files with `Y` or with `a` at once.

### 4) Development

When you have the basic setup done and your first page added, you can start development. Run the grunt command to generate preview files in the dist folder:

```
grunt
```

![grunt command](docs/img/grunt.png)

If everything went ok, the preview files will be generated and you will be able to check your work in the `dist` folder. XH Generator doesn't create a server, so you need to preview files on your existing local web server.

To re-compile HTML / SCSS file in real time you can use watch task. Type

```
grunt watch
```

and this will start a task that will watch for changes in files and recompile them as needed. Now you can also connect with a [LiveReload browser extension](http://feedback.livereload.com/knowledgebase/articles/86242-how-do-i-install-and-use-the-browser-extensions) to enable live reloads in your browser.

![grunt watch command](docs/img/grunt-watch.png)

To rebuild the whole project and validate HTML files, use the grunt task again

```
grunt
```

(Please note that HTML validation in `grunt` task can be time consuming so we recommend using `grunt watch` for regular development.)

## Tips & Tricks

### Working with files in the dist folder

In general, it’s not recommended that you work directly with files in the `dist` folder except images in `dist/img` folder. The files in `dist` folder are automatically generated from the source files in `src` folder. However, once you hand over the project to your client, they can work directly with plain HTML and CSS files if they wish.

HTML and CSS files are prettified for consistent formatting and a table of contents from imported SCSS or Less stylesheets is generated at the beginning of `main.css` for better overview.

## Writing styles

XH Generator supports SCSS or Less. The following source files are generated in `src/scss` or `src/less` folders:

- `main.scss` / `main.less` - main file where other stylesheets are imported
- `_variables.scss` / `variables.less` - variables file
- `_mixins.scss` / `mixins.less` - mixins file
- `_common.scss` / `common.less` - minimal common styling
- `_wp.scss` / `wp.less` -  [WordPress styles](http://codex.wordpress.org/CSS) for images and captions (in WP projects)
- `_home.scss` / `home.less`, `_about.scss` / `about.less`, etc. - individual pages

The following approach is recommended when creating styles:

1. Use `main.scss` or `main.less` only for importing other stylesheets. Do not write styles directly to these files!
2. Use variables and mixins files to store your variables and mixins.
3. Use `common.scss` or `common.less` for element's styling which is shared across 2 or more pages. Typically those are main layout, headers, footers, sidebars, pagers, buttons, etc.
4. If you want, you can separate common elements to more stylesheets like `buttons.scss`, `forms.scss`, etc. and import them in `main.scss` (or `main.less`)
5. Use individual pages stylesheets for storing styles which are unique for certain page. This will ease collaboration among more developers.

### Adding 3rd party dependency via Bower

Let’s say you want to add [Colorbox](http://www.jacklmoore.com/colorbox/) to your project. The following example shows how you can add it as a Bower package and merge its JS file into common `plugins.js` file.

1. First, install it via Bower

    ```
    bower install jquery-colorbox --save-dev
    ```

2. Then link it in `src/includes/scripts.html`. This will ensure that the library will be added to `plugins.js` file

    ```html
    <script src="//code.jquery.com/jquery-1.11.1.min.js"></script>
    <script>window.jQuery || document.write('<script src="js/jquery.min.js">\x3C/script>')</script>
    <!-- build:js js/plugins.js -->
    <script src="bower_components/jquery-colorbox/jquery.colorbox-min.js"></script>
    <!-- endbuild -->
    <script src="js/main.js"></script>
```

3. Download [Colorbox archive](https://github.com/jackmoore/colorbox/archive/master.zip) and copy images from `example1/images` folder to `dist/img/colorbox` folder.

4. Get `colorbox.css` from the archive, rename it to `colorbox.scss` and store it in `src/scss` folder

5. Import `colorbox.scss` in `main.scss`

    ```css
    @import "colorbox";
    ```

6. Replace all instances of `images/` in `colorbox.scss` with `../img/colorbox/`

7. Run the `grunt` task or `grunt watch`

8. Now you can use Colorbox in your HTML files and initiate it from `src/js/main.js`

## License

XH Generator is licensed under [MIT License](LICENSE)