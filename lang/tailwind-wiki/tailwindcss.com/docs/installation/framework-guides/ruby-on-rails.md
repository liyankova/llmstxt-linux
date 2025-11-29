---
source_url: "https://tailwindcss.com/docs/installation/framework-guides/ruby-on-rails"
title: "Install Tailwind CSS with Ruby on Rails - Tailwind CSS"
crawl_date: "2025-11-29T13:56:16.366837Z"
selector: ".isolate .mx-auto"
---

# Install Tailwind CSS with Ruby on Rails - Tailwind CSS

Installation

# Install Tailwind CSS with Ruby on Rails

Setting up Tailwind CSS in Ruby on Rails v8+ project.

01

#### Create your project

Start by creating a new Rails project if you don't have one set up already. The most common approach is to use the [Rails Command Line](https://guides.rubyonrails.org/command_line.html).

Terminal

```
rails new my-projectcd my-project
```

02

#### Install Tailwind CSS

Install the `tailwindcss-rails` gem then run the install command to set up Tailwind CSS in your project.

Terminal

```
bundle add tailwindcss-rails./bin/rails tailwindcss:install
```

03

#### Start your build process

Run your build process with `./bin/dev`.

Terminal

```
./bin/dev
```

04

#### Start using Tailwind in your project

Start using Tailwind's utility classes to style your content.

index.html.erb

```
<h1 class="text-3xl font-bold underline">  Hello world!</h1>
```