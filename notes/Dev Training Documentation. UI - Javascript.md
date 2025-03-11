---
tags: [Dev Training]
title: Dev Training Documentation. UI - Javascript
created: '2022-11-24T06:21:04.431Z'
modified: '2024-11-05T08:51:34.578Z'
---

# Dev Training Documentation. UI - Javascript
https://docs.google.com/document/d/17uYWvSsUQhU_2RFauMY8zuDX34yf0OyvIHsL0FQAVKM/edit#heading=h.s422etnzug7j


## Interesting links
RFE uses:
- Gulp (https://gulpjs.com) => It is a task runner built on Node.js and npm, used for automation of time-consuming and repetitive tasks involved in web development like minification, concatenation, cache busting, unit testing, linting, optimization, etc.

- TypeScript (https://www.typescriptlang.org) => TypeScript is a strongly typed programming language that builds on JavaScript, giving you better tooling at any scale.

- SCSS (https://sass-lang.com/) => Sass is the most mature, stable, and powerful professional grade CSS extension language in the world.

## All Tasks are configured by \vl\vlib\gulpfile.js

**default** This task runs build-styles and build-scripts tasks, so when making changes to the UI by html or js, you may need to run this task.
- **build-** (are used to build specific files)
    - build-script is a useful task to build all scripts (it uses linter and ts compiler)
    - build-styles is a useful task to build all styles. It uses sub-tasks:
    - build-css to bundle all global css files
    - build-scss to compile scss files
- **clean/clean-** (are used to clean destination folder)
    - clean-scripts to clean all javascript and compiled typescript
    - clean-styles to clean global css bundle (with compiled scss)
    - clean to clean all destination stuff
- **compile-/lint-** (are used for typescript and usually called by build-scripts)
    - compile-ts-entry-points to process all index.ts files related to specific pages
    - compile-ts-global to compile all global ts files
    - lint-ts to run static typescript analyzer
- **watch/watch-** (are used for watching)
    - watch-scripts to watch for typescript files and rebuild them if they are changing
    - watch-styles to watch for scss/global css files to rebuild them if they are changing
