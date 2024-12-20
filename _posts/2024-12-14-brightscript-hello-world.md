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

<img alt="Folder structure for the Hello World channel" src="/assets/img/posts/2024/folderStructure.png" width="250" align="right" style="background: #f7f7f7; border: 1px solid #eee; margin: 0 0 30px 30px; padding: 10px;" />

The `.vscode` folder contains files that are exclusive to the VSCode IDE. They are not required to create a Roku channel, but will make your life easier and speed up your development process.

The `components` folder holds programming code that extends BrightScript and SceneGraph components. Both of these languages provide a core set of components we can use, but we can extend them to alter or add to their functionality and display.

The `images` folder is where you store your image files. No surprises there.

The `source` folder holds your channel's custom code. Your main program code will be located within this folder.

And finally the `root` folder of your project holds at least one file that is required to build and deploy your channel.

## Explanation of Files

`.vscode/extensions.json`
Tells VSCode which extensions to recomend users install for this project.

`.vscode/launch.json`
Debug launch instructions for VSCode to deploy and run our channel on a Roku device.

`components/mainScene.brs`
Backend code and logic for the scene we load and display in our channel. You can roughly think of this as the JavaScript of our channel.
`components/mainScene.xml`
The rendering configuration for the scene we load and display in our channel. You can roughly think of this as the HTML of our channel.

`images/channel_fhd.jpg`
`images/channel_hd.jpg`
`images/channel_sd.jpg`
Images shown in the user's channel list. These images are specified in the manifest file and provide different image sizes for different display resolutions.

`images/splash_fhd.jpg`
`images/splash_hd.jpg`
`images/splash_sd.jpg`
Images shown when a channel is launched and is loading. These images are specified in the manifest file and provide different image sizes for different display resolutions.

`images/tv.png`
Used in the channel to show how to display an image.

`source/main.brs`
The main program file for our channel. This is the file Roku will first look for and call when it launches your channel. This file will have our primary code loop.

The `main()` sub in this file is the starting point of every Roku channel.

`.env`
Holds the username and password for our development Roku device. This file is loaded by our `launch.json` commands so we can push our files to the Roku.

`.gitignore`
Instructions to GitHub to ignore our build folder.

`LICENSE.md`
The license file for the Hello World project.

`README.md`
The readme file for the Hello World project. Used by GitHub to display content on the project's main page.

`manifest`
Holds important information and instructions telling Roku how to load and launch our channel along with our settings for various options.

## Launch Order

After the Hello World channel is deployed to your Roku, here's the order that things are run to give you an idea of the general flow of a channel.

`manifest` instructs Roku to show the mm_icon_focus image for our set resolution in the list of channels.

When we choose the channel from the list, `manifest` instructs Roku to display our splash_screen image and wait for the splash_min_time amount of time.

`main()` inside `source/main.brs` is called.

Inside `main()` we setup our screen and instruct it to create and display the mainScene component.

`init()` inside `components/mainScene.brs` is called.

The code from `components/mainScene.brs` is applied to the display instructions in `components/mainScene.xml` and pushed to the screen.

Back inside `main()` in `source/main.brs` we wait inside a loop for an event to occur.
