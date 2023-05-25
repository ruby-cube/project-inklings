<div align="center">
<picture>
  <img width="520" src="https://github.com/ruby-cube/project-inklings/blob/main/inklings-logo.png" alt="inklings logo"/>
</picture>
</div>

⚠️ **Under Active Development**: Inklings is still at an early stage of development and currently lives in a private repository. It will eventually be released as open source. Early prototypes have so far been extremely promising :)

<p align="right"><a href="#">[top]</a></p>

## Overview

A local-first rich text/content block editor with an intuitive UI design for capturing and organizing thoughts. Features a clean, minimal graphical interface and innovative UI elements that enable users to edit with ease. Built with Typescript, [Vue.js](www.vuejs.org), and [Rue.js](https://github.com/ruby-cube/rue).

<p align="right"><a href="#">[top]</a></p>





## Motivation

The idea of incorporating draggable items into a clean, minimal text editing interface has captivated me since the early days of Workflowy. Years later, [Notion](http://Notion.so) took the concept even further in a mind-blowing way. I was in love.

However, as much as I love Notion and Workflowy and can’t help but sing their praises, there are aspects of the UI that get in the way of my productivity, and I often find myself wishing I could achieve what I want more intuitively, with less bulky menus, less unintentional pop-ups, and less surprises. Many of these are not small tweaks that can be requested to the Notion team.

In recent years, there has been an explosion of apps following in Notion and Workflowy’s footsteps (see [Prior Art](#prior-art)). I have tried many of them and although they each add their own unique take on content block editing, none of them deliver the simple, easy experience I’m looking for in a thought-organization/thinking tool.

So I’ve set out to build my ideal content block editor—one that feels as simple to use as sitting down with a journal. A place to lay out your thoughts and plan out your month. A place to list your to-dos, dump all your ideas and organize them. A place to draft a document. Local-first and syncable across devices.

<p align="right"><a href="#">[top]</a></p>

## UI/UX Notes

Below are some thoughts on how user experience can be improved based on issues I encountered with Notion, along with some visuals of early-stage implementations from prototypes of Inklings.

**Jump to:**

- [provide more ui hints](#provide-more-ui-hints)
- [reduce distracting pop-ups](#reduce-distracting-pop-ups)
- [favor tools that can be “picked up, used, and set down” over large menus](#favor-tools-that-can-be-picked-up-used-and-set-down-over-large-menus)
- [offer a pen-and-paper experience](#offer-a-pen-and-paper-experience)
- [implement collaboration through Git-like synchronization](#implement-collaboration-through-git-like-synchronization)

<p align="right"><a href="#">[top]</a></p>

### Provide more UI hints

Notion’s unobtrusive item handles that only appear on item hover is undoubtedly one of the most brilliant UI designs I’ve encountered. It’s there when you might need it and out of sight when unnecessary, keeping the interface clean and free of distractions. 

Sometimes though, I wish there could be more of these kinds of unobtrusive UI hints. I love Notion’s ultra-minimal interface, but there are times when I accidentally do things that I don’t mean to do or feel unsure of what I should expect if I interact with a given area.

For example, sometimes I drag a heading thinking the section text will move along with it, only to find I have left everything behind. 

We can reduce these sorts of experiences with subtle spotlighting of the items that will be moved so users know beforehand if they will be moving a single item or a family of items.

https://user-images.githubusercontent.com/68570184/236367086-e47029cb-03a1-4bfd-9c5b-29cdfadd7a7f.mov

A spotlight is also visually helpful when moving items via keyboard (inspired by VSCode):

https://user-images.githubusercontent.com/68570184/236367086-e47029cb-03a1-4bfd-9c5b-29cdfadd7a7f.mov

Another example of a “UI surprise” encountered in Notion is the unintentional existence of columns. I have more than once discovered hidden columns in my document that I didn’t mean to create, because I misplaced an item I was dragging. Even for intentional columns, finding the boundaries of a column feels like guesswork. There is little indication where precisely a column exists.

We can address this by offering UI hints for column borders when the mouse hovers over the document.


<p align="right"><a href="#uiux-notes">[toc]</a></p>

### Reduce distracting pop-ups

While I understand the UI design choice of having toolbars and menus pop up where a user’s mouse is, I find more often than not menus popping up when I don’t actually need them, doing nothing but obstructing my ability to see the content I’m working on.

One example of an overly-offered menu in Notion is the slash command menu. Most of the time, I just want to type a forward slash as part of my text. Instead, a huge menu offering pops up to obstruct the rest of my text. 

We can address this by designating a partner-less closing bracket as the trigger key instead of the forward slash. This more-or-less eliminates unintended menu pop-ups, offering the command menu when the user actually intends to use it. When the closing bracket key is pressed, an algorithm searches preceding text for the opening bracket it’s meant to close. If none is found, it displays the command menu.

<p align="right"><a href="#uiux-notes">[toc]</a></p>

### Favor tools that can be “picked up, used, and set down” over large menus

The typical user flow of formatting text is to select text, then choose the desired formatting from a menu or toolbar. This is a nice user flow for rich text formatting. However, with text color and highlighting, the user flow becomes slightly more involved, requiring the user to open up a color palette. It turns the simple, light format menu into a bulky obstruction on the screen.

It doesn’t have to be this way. For text coloring and highlighting, a more intuitive flow would be to grab a highlighter, choose a color, and highlight. You can highlight multiple things without having to re-select the highlighter tool each time. With the text-formatting user flow, you have to go through the toolbar and menu for every single highlight, resulting in more clicks to achieve the task.

https://user-images.githubusercontent.com/68570184/236367086-e47029cb-03a1-4bfd-9c5b-29cdfadd7a7f.mov

When you’re done with the tool, setting down the tool should take nothing more than clicking any non-highlightable area (with the cursor visually indicating escape areas). This tool-escape strategy differs from most drawing applications, where in order to escape a tool, you need to find the default tool in the toolbar, move your mouse over to that tiny button, and click. That takes too much brain energy and coordination. In real life, you would simply set a highlighter down to the side with little thought. Escaping a tool in an app should be just as mindless.

<p align="right"><a href="#uiux-notes">[toc]</a></p>

### Offer a pen-and-paper experience

The highlighter user flow mentioned above is an example of a user flow that mimics a pen-and paper experience. We can continue along these lines by implementing two features based on my bullet journaling workflow: 

- I list out all my to-do’s
- I mark the items I want to focus on for the current block of time with an erasable highlighter
- Once the task is complete, I cross off the item and erase the highlighter mark

This differs from Notion which visually emphasizes completed items with a bright blue mark. I can understand how some people may like this, as it serves as a visual reward for completing a task. However, I personally prefer completed items to visually recede and to reserve visual emphases for the to-do items I plan to focus on.

In this implementation of strikethrough, the user initiates strikethrough with a horizontal stroke, mimicking real life, but more efficient.

https://user-images.githubusercontent.com/68570184/236367086-e47029cb-03a1-4bfd-9c5b-29cdfadd7a7f.mov

Mimicking the pen-and-paper experience through these small details transform the standard rich-text editing experience into something a bit more intuitive and perhaps even delightful.

<p align="right"><a href="#uiux-notes">[toc]</a></p>

### Implement collaboration through Git-like synchronization

Real-time collaboration is not a goal of this app as it is meant to be local-first, which means versions of a document may diverge significantly before synchronization happens.

I experience a blast of anxiety when I see a message that says a document I’m working on has a different version out there. I don’t know what updating my current version with the other version will do to the document. … will I lose work?

As tempting as it is to aim for automatic eventual consistency in rich text editing, I don’t believe it’s possible to write an algorithm that can mind-read. Even an AI can’t guess correctly 100% of the time how two user’s would want their content to merge. 

There will always be cases where users must manually resolve conflicts. Git understands this. The best we can do is make the process as user-friendly as possible. Do automatic merging when possible, but provide a clear, easy-to-use interface for resolving conflicts so that users feel like they have control over their document.

<p align="right"><a href="#uiux-notes">[toc]</a></p>

## A note on accessibility

The aesthetics of this project focuses on creating a clean, minimal user interface with subtle UI hints. This is not great for accessibility. My hope is to eventually incorporate accessibility options that will allow the interface to be more usable for people who may need starker contrast for visibility.

Screen reader and keyboard navigation accessibility is also a concern that I hope to address.

<p align="right"><a href="#uiux-notes">[toc]</a></p>

## Prior Art

- [Workflowy](https://www.workflowy.com/)
- [Notion](https://www.notion.so/)
- [Craft](https://www.craft.do/)
- [Walling](https://walling.app/)
- [Microsoft Loop](https://www.microsoft.com/en-us/microsoft-loop)
- [Dynalist](https://dynalist.io/)
- [Affine](https://affine.pro/)
- [AppFlowy](https://appflowy.io/)
- [Obsidian](https://obsidian.md)
- [Dropbox Paper](https://www.dropbox.com/paper/start)

<p align="right"><a href="#">[top]</a></p>

© 2023 - present [Ruby Y Wang](https://github.com/ruby-cube)
