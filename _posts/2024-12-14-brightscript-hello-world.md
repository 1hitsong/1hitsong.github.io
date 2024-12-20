---
title: Make a Roku channel: Part 1 - Hello World
date: 2024-12-20 17:00:00 -0500
categories: [programming, learning]
tags: [roku, brightscript, code, learning]     # TAG names should always be lowercase
---

When learning a new programming language, there's only one place to start.

Let's take a look at a [Hello World](https://github.com/1hitsong/Learn-BrightScript-Hello-World) channel!

## Folder Structure

Unlike some programming languages, BrightScript expects some, but not all, files to be in specific folders. Below is an explanation of each folder in our Hello World channel.
<img alt="Folder structure for the Hello World channel" src="/assets/img/posts/2024/folderStructure.png" width="300" />

The `.vscode` folder holds files that are exclusive to the VSCode IDE. They are not required to create a Roku channel, but will make your life easier and speed up your development process.

The `components` folder holds programming code that extends BrightScript and SceneGraph components. These languages provide a base set of components we can use, but we can extend them to add or alter their functionality and display.

The `images` folder is where you store your image files. No surprises there.

The `source` folder holds your channel's custom code. Your main program code will be located within this folder.

And finally the `root` folder of your project holds at least one file that is required to build and deploy your channel.

## Explanation of Files

`.vscode/extensions.json`

`.vscode/launch.json`

`components/mainScene.brs`
`components/mainScene.xml`

`images/channel_fhd.jpg`
`images/channel_hd.jpg`
`images/channel_sd.jpg`

`images/splash_fhd.jpg`
`images/splash_hd.jpg`
`images/splash_sd.jpg`

`images/tv.png`

`source/main.brs`

`.env`
`.gitignore`
`LICENSE.md`
`README.md`
`mainifest`

The `main()` sub in the file `/source/main.brs` is the starting point of every Roku channel.

## SceneGraph vs BrightScript
