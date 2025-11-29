---
source_url: "https://tailwindcss.com/docs/installation/play-cdn"
title: "Play CDN - Tailwind CSS"
crawl_date: "2025-11-29T13:43:49.811202Z"
selector: ".isolate .mx-auto"
---

# Play CDN - Tailwind CSS

Installation

# Get started with Tailwind CSS

Tailwind CSS works by scanning all of your HTML files, JavaScript components, and any other templates for class names, generating the corresponding styles and then writing them to a static CSS file.

It's fast, flexible, and reliable — with zero-runtime.

## Installation

* ## [Using Vite](/docs/installation/using-vite)
* ## [Using PostCSS](/docs/installation/using-postcss)
* ## [Tailwind CLI](/docs/installation/tailwind-cli)
* ## [Framework Guides](/docs/installation/framework-guides)
* ## [Play CDN](/docs/installation/play-cdn)

### Using Play CDN

Use the Play CDN to try Tailwind right in the browser without any build step. The Play CDN is designed for development purposes only, and is not intended for production.

01

#### Add the Play CDN script to your HTML

Add the Play CDN script tag to the `<head>` of your HTML file, and start using Tailwind’s utility classes to style your content.

index.html

```
<!doctype html><html>  <head>    <meta charset="UTF-8" />    <meta name="viewport" content="width=device-width, initial-scale=1.0" />    <script src="https://cdn.jsdelivr.net/npm/@tailwindcss/browser@4"></script>  </head>  <body>    <h1 class="text-3xl font-bold underline">      Hello world!    </h1>  </body></html>
```

02

#### Try adding some custom CSS

Use `type="text/tailwindcss"` to add custom CSS that supports all of Tailwind's CSS features.

index.html

```
<!doctype html><html>  <head>    <meta charset="UTF-8" />    <meta name="viewport" content="width=device-width, initial-scale=1.0" />    <script src="https://cdn.jsdelivr.net/npm/@tailwindcss/browser@4"></script>    <style type="text/tailwindcss">      @theme {        --color-clifford: #da373d;      }    </style>  </head>  <body>    <h1 class="text-3xl font-bold underline text-clifford">      Hello world!    </h1>  </body></html>
```