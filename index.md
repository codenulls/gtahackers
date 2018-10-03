---
title: "Welcome"
keywords: GTA III, GTA VC, GTA SA, GTA classes
sidebar: gta_sidebar
permalink: index.html
---

## PURPOSE

We all know how popular GTA games are but when it comes to technical documentation, it takes a lot of effort to find what you're looking for, wouldn't it be better to find all technical information on a website, which is not going to disappear someday? There are many people who have tried to document old GTA games like III, VC, and SA but none of them have ever finished. Some time ago, gtamodding.com went down out of the blue, and it's only possible to access the website's contents via web archive. Now, we're only left with modding forums with hundreds of posts on a single thread, which is fine for the most part, it just gets harder when you want to learn about a specific topic in detail. We're here to fix that.

## WHAT TO EXPECT

There are 700+ GTA classes in GTA III, VS, and SA with little to no documentation. The only ones who understand how they work are people that are active in GTA modding communities, if anyone else wishes to learn how they work, they'll need to open up IDA and understand the workflow. This is a very time-consuming process. Our goal here is to document every global variable, enumeration, class, and function. This will help newbies to start quickly without getting lost in piles of ASM. 

## TWO IMPORTANT PROJECTS

There are two helpful projects which are actively maintained, and you should know about them since the reversed classes and code examples are based on them.

### 1. PLUGIN-SDK [(GITHUB)](https://github.com/DK22Pac/plugin-sdk) 

plugin-sdk contains header files for almost all GTA classes. There are wrappers within .cpp files for calling GTA functions, and the best part is that you don't need to worry about memory addresses across different game versions, just include the header files in your plugin-sdk C++ project and you're ready to go. It supports Visual Studio and CodeBlocks.

### 2. GTA-REVERSED [(GITLAB)](https://gitlab.com/gtahackers/gta-reversed/) 

gta-reversed is a project where all SA header files are inherited from plugin-sdk with the goal to reverse all GTA SA US 1.0 functions and rewrite them accurately in C++. I know it sounds very laborious but the good news is that it's possible because we have idbs from plugin-sdk which are nearly complete. Here are the SA idbs: 

{% include warning.html content="Do not extract them separately. First download both of these files, select them both, and then extract them together to generate a single gta_sa.idb." %}

* [gta_sa_27.03.2018.part01.rar](https://cdn.discordapp.com/attachments/392628519471153153/428126475712069633/gta_sa_27.03.2018.part01.rar)
* [gta_sa_27.03.2018.part02.rar](https://cdn.discordapp.com/attachments/392628519471153153/428126481802067988/gta_sa_27.03.2018.part02.rar)

You'll need at least IDA Pro 7.0 or higher to open them because it comes with HexRays Decompiler. Pressing F5 on a function will decompile it, and it will be more readible, you can press Y on a variable to rename its type and N to rename it, this will reformat the code and look like this:

{% include image.html file="HexRays_Output.PNG" url="http://jekyllrb.com" alt="IDA Pro Output" caption="Ouptut of HexRays for GTA SA IDB" %}

## DISCORD

I believe that communication is the key. If you need help with a mod or you simply wish to contribute then why not join our discord server? We're always discussing on how we can improve the modding community.

<div class="iframe-container-discord">
    <iframe src="https://discordapp.com/widget?id=479682870047408139&theme=dark" allowtransparency="true" frameborder="0"></iframe>
</div>
