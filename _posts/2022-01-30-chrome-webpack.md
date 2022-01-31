---
toc: true
layout: post
description: Chrome Extension + Webpack
categories: [chrome-extension, webpack]
title: Building Chrome Extension with Webpack Bundler
image: images/chrome-webpack-nob.png
---

# Chrome Extension Manifest Version 3 + Webpack  

## Boilerplate Code 

Find the codebase in the github link [here](https://github.com/RasikaWarade/chrome-extension-mv3-webpack-boilerplate).

The Chrome Extension boilerplate uses Webpack to speed up the process of writing modular Javascript code, loading HTML and CSS easily, and automatically refresh the browser based on changes.

## Why?

As per the [Chrome Extension Timeline](https://developer.chrome.com/docs/extensions/mv3/mv2-sunset/), all extensions supporting Manifest Version v2 will sunset in Jan 2023, and for new extensions, it has now become a requirement to move to Manifest Version V3.

Google Chrome Extension Manifest v3's most significant security change is that [remotely hosted code](https://developer.chrome.com/docs/extensions/mv3/intro/mv3-overview/#remotely-hosted-code), such as Javascript, is now not allowed. If your extension codebase is not bundled and structured in a modular fashion, this can lead to problems. A beginner like me will definitely have a hard time building a setup like that without any guideline. 

When I built my Chrome Extension, I had limited experience with webpack, and I believe that new beginners may have the same issue, which is why I decided to compile this resource.


# Structure

I am assuming you have taken look for introduction at the [Chrome Extension docs](https://developer.chrome.com/docs/extensions/mv3/getstarted/) and [Webpack docs](https://webpack.js.org/).

Also, if you are beginner, I am assuming you probably would have worked on the [Getting Started Guide](https://developer.chrome.com/docs/extensions/mv3/getstarted/) for extension. If not, I would give a quick look at it as well.

**This repo bundles the code explained in the [Getting Started Guide](https://developer.chrome.com/docs/extensions/mv3/getstarted/) with Webpack.**

## Initial Setup

Make sure you have latest [Node.js](https://formulae.brew.sh/formula/node) installed.

My current version:
```
(base) ➜  chrome-extension-mv3-webpack-boilerplate git:(main) ✗ node --version
v16.13.1
(base) ➜  chrome-extension-mv3-webpack-boilerplate git:(main) ✗ npm --version
8.1.2

```

## Configuration

For the initial setup, below webpack bundles were installed:

`npm install --save-dev webpack webpack-cli html-webpack-plugin clean-webpack-plugin copy-webpack-plugin`


> `webpack.development.js`

For Development Purposes, you can configure this script and run the command `npm run build` to reflect changes.

> `webpack.production.js`

For production release, you can configure this script and run the command `npm run release`  to reflect changes.

> `webpack.common.js`

This script contains all the common bundler config common between development and production scripts above.

> `src`

All the html/css files and manifest.json are added in this directory.

Includes:
- background.js
- content.js
- popup (js + html + css)
- options (js + html)


> `src/manifest.json`

This is the entry point for your extension.


```
{
  "manifest_version": 3,
  "version": "0.1",
  "name": "MV3 Extension with Webpack",
  "description": "Webpack Modular Framework!",
  "action": {
    "default_popup": "./popup.html",
    "default_icon": {
      "16": "./src/icons/get_started16.png",
      "32": "./src/icons/get_started32.png",
      "48": "./src/icons/get_started48.png",
      "128": "./src/icons/get_started128.png"
    },
    "default_title": "Getting Started MV3!"
  },
  "permissions": [
    "storage",
    "activeTab",
    "scripting"
  ],
  "content_scripts": [
    {
      "matches": [
        "<all_urls>"
      ],
      "js": [
        "content.js"
      ]
    }
  ],
  "background": {
    "service_worker": "background.js"
  },
  "icons": {
    "16": "./src/icons/get_started16.png",
    "32": "./src/icons/get_started32.png",
    "48": "./src/icons/get_started48.png",
    "128": "./src/icons/get_started128.png"
  },
  "options_page": "options.html"
}
```


# How to use it

1. Clone the repo
2. Run command `npm install` to install all node-modules / dependencies
4. Run command `npm run build`
5. This will build the `dist` folder
6. Load the Chrome Extension you just build by pointing to this `dist` folder

Note: `gitignore` will help ignore the `node_modules` and `dist` folder to be pushed to the github


# What's Next!

Feel free to use this template as boilerplate and update as per your own requirements. As I mentioned this bundling would help when you want to access some remotely hosted code / libraries, and in my next blog you will see an example of how I utilized it.