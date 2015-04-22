---
layout: post
title: "Crafting Minecraft"
date: 2015-04-22 15:38:52 -0500
comments: true
categories:
---

### Introduction

![Minecraft FA 310](http://i.imgur.com/RhbniNM.jpg)

Minecraft is a popular indie game developed by Mojang [1], that has the following premise: build something. Well, not exactly, but the game is known to have inspired a large variety of creative work, similar to the one above. A couple examples are as follows:

![Ancient metropolis](http://rack.0.mshcdn.com/media/ZgkyMDEzLzAyLzA4L2NjL2FuY2llbnRtZXRyLjIzYmU5LmpwZwpwCXRodW1iCTg1MHg4NTA-CmUJanBn/f7574d0c/f85/ancient-metropolis.jpg)

![Pinterest example](https://s-media-cache-ak0.pinimg.com/originals/9b/ef/6c/9bef6ccf510d60444cb043619421d713.jpg)

![Golden city](http://static3.businessinsider.com/image/537b99b16bb3f7913c6473d0-1200/minecraft-golden-city.png)

Furthermore, players aren't limited to just creating structures within the game. People have made [animation](https://www.youtube.com/user/CaptainSparklez), [fanart](https://www.pinterest.com/explore/minecraft-fan-art/), and [texture packs](http://www.minecrafttexturepacks.com/), which gives the game an entirely new aesthetic.

With such a broad range of possibilities, Minecraft has been often analyzed through the lens of formalism. Does this game conform to the standards of what we define as a video game? Can it be considered a game at all? If so, what category or genre does it classify as? These questions have been asked frequently by not only scholars but also by gamers alike. It isn't rare to find someone decrying Minecraft for not being a "true" game, while touting the merits of Call of Duty per se. One work that I find particularly helpful in the creation of this post is The Craft of Data Mining [2], which explores the innate constraints set on the game. This analysis, however, is not one of formalism. Instead, I explore the technical aspects of Minecraft and modding culture through the lens of reader-response theory, and attempt to define the game in terms of its mechanics.

### Mechanics

From a gameplay perspective, Minecraft has two main player modes: survival and creative. Survival introduces the notion of a health bar and a hunger bar, and forces the user to forge for their own survival. You can craft with a 3x3 grid based system and form complex materials and weapons by doing so, similar to some RPGs. Creative removes all of these restrictions and simply enables the user to build, explore, or destroy the world.
As mentioned before, the game tends to be pretty open-ended. However, it is possible to "beat" the game in survival mode by going to the END and slaying the Ender Dragon. Ironically enough, once you clear the game, you are respawned as if nothing happened [3].

More interestingly, the creators of Minecraft, Mojang, have been proactive in encouraging users to mod, or modify, the game. These mods could range from [introducing Chocobos from Final Fantasy](http://www.minecraftmods.com/chococraft/) to [extending and simplifying the HUD](http://www.minecraftmods.com/toomanyitems/). How one could create such a mod would involve using a modding API, such as Minecraft Forge [4]. An API stands for Application Programmer Interface, which is essentially a set of tools to build an application with. In the case of Minecraft, an API could expose such methods as creating a block or equipping an item.

Now where Minecraft begins to differ from most other games is the extent to which the API is exposed. For example, take a SNES game. One could modify the textures, animations, and even maybe the display of the game, but it would be very difficult to go beyond that. Even more lenient games, such as Skyrim, still restrict which code is publicly accessible. In contrast, Minecraft has nearly no restrictions. One can modify anything from the HUD to the very mechanics of the game, as this one mod did with [quantum physics](http://qcraft.org/about/). To understand why, we have to delve into the internals of the Minecraft application.

Minecraft is shipped as a jar file. Jar stands for Java Archive, similar to a .zip file as well. This file contains the entirety of Minecraft. The file is responsible for user validation, networking, terrain generation, graphics display, chat, and more. Mods work by modifying this Jar file, such as adding and rewriting sections of the source code. There's a clear security issue, however, in that any user could access the entirety of your source code by simply unzipping this archive. Minecraft, and other enterprise applications, gets around that by obfuscating the source code. So for example, the word "World" would be translated to "2ja10".

Gamers tend to be pretty persistent, however, and soon enough they were able to deduce a schematic for the obfuscation. From there, they were able to extend and modify the game. A guide on how to install a mod can be found [here](http://minecraft.gamepedia.com/Mods/Installing_mods#How_to_Install_Mods).

Now, with modding APIs such [Minecraft Sponge](https://www.spongepowered.org/), a new API that attempts to combine both server side and client side modifications, enabling users to modify nearly anything, we are faced with the following question. Where do we draw the boundary between a modification of Minecraft and a new game entirely?

Furthermore, Minecraft inspired a variety of clones, such as Terraria and [Planets3](https://www.kickstarter.com/projects/1247991467/planets3). Developers all across the world have implemented Minecraft in [C++](http://www.minetest.net/), [Python](https://mcpipy.wordpress.com/), and even [Haskell](https://github.com/nandor/hcraft). These clones are just as fleshed out, if not better, than Minecraft. What is the difference between Minecraft and these games as well? Can they be considered as the same game?

### Argument

My argument is that the defining aspects of a game are found in not only its mechanics, but also in its concept. In other words, a game must be considered in terms of its concepts primarily. The mechanics of a game is simply an implementation of the concept. Take Call of Duty as an example. The game's concept is quite simple and naive. Nearly anyone could come up with it. Yet, it's implementation was great, involving years of development. Call of Duty is a case of a game where it relies more heavily on the implementation rather than the concept. Minecraft would be the opposite.

To answer the questions I've stated above, I believe that the clones of Minecraft can be regarded as the same game. Of course it would be difficult in the case of drastic changes, such as Terraria to Minecraft. What classifies a mod of a game as distinct from the game itself is when the concepts between the two have diverged distinctly. Take Team Fortress 2, a game that originated from a Quake mod, as an example. Originally, Team Fortress Classic, simply added the notion of classes to Quake. Team Fortress 2 extended that concept into maps of play, where new play styles, strategies, and art has been created, resulting in a distinct concept from Quake.

In conclusion, Minecraft has encouraged a healthy population of mods and artistic work. The open-endedness of the game is one of the defining aspects of the game and I believe that there is no "right" way to play Minecraft. However, I do believe there is a distinction between the modding Minecraft and creating a separate game entirely. Hopefully this argument will be of use to anyone who wishes to mod the game as well.

### Citations
1. https://minecraft.net/
2. The Craft of Data Mining, Minecraft and the Constraints of Play - Tremblay, Colangelo, and Brown
3. http://minecraft.gamepedia.com/The_End
4. http://files.minecraftforge.net/

Regarding the images used throughout the post,
besides those I've created personally, all of the images in the post can be found in the page document in my Github to the left.
