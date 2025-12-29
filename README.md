# FiveM and RedM Project Examples
This repository contains videos and a short description of the background/goal and how I tackled each project I made for FiveM and RedM. A lot of these projects are fairly rough, proof-of-concepts, which I made to try out certain fuctionalities within these platforms.
## FiveM-Projects

### Notebook
Video: https://www.youtube.com/watch?v=arIOmHJ5_T8

The actual notebook part of this project was fairly simple to do, the interesting parts came from some of the technical aspects, such as the pictures representing physical items in the inventory. However, the most interesting part for this project was figuring out how to properly store the drawings on each page. I didn't want to just save them as images because that would be very ineffecient. In the end I chose to use a combination of run-length encoding and variable-length encoding. The main reason behind this choice was to ensure that large spaces of the same color could be encoded effeciently, as well as making sure spaces with only a couple of same color pixels could be encoded with just a single byte instead of using 32 bit integers for everything. Another advantage of this method is that it's really fast to encode/decode the drawings. The final encoded size will, of course, also depend on the resolution of the canvas, so there is also a choice to make between the quality of the drawings and storage. However, changing the resolution is pretty simple as well. 

### Rappel
Video: https://www.youtube.com/watch?v=s1nF3YapO14

The weird part of this project is that, for some reason, I could not get to work with Lua (certain natives didn't work properly and there was also a thread on this on the forum with similar issues). To solve this problem, I had to switch over to C#, which wasn't thad bad as I have quite a lot of experience with C#. At the time when I was making this, ropes were also not synchronized accross the network, so I had to write my own synchronization code (which required a lot of optimization to make sure that there was a good balance between performance and real-timeliness of the synchronization). 

### Watertruck
Video Filling: https://www.youtube.com/watch?v=pjwxjCU1a-k </br>
Video Rope Collision: https://www.youtube.com/watch?v=IUDqZBNN7yQ </br>
Video Filling Container with Overflow: https://www.youtube.com/watch?v=FcNOqiyYNE0

For this project I wanted to combine some rope and water natives. My first idea was to use the native that allows you to change the water level of a water quad, so it would be possible to drain a pool, lake etc... However, it seems that most of the water sources in GTA don't make use of water quads. Luckily, an entity still counts as being inside water when standing inside non-water quad water (so the whole filling up the tanker part still works nicely). I also made sure that the rope that acts as the pump breaks whenever there is something colliding with it. This was pretty easy to do using the shape test natives, with of course making sure that there isn't a big hit on the performance. It's also possible to fill certain containers, for these I also made it so the pump doesn't automatically stop whenever the container is filled. So if the player isn't careful the container will start overflowing, which is indicated by a water particle effect.

### Graffiti
Video: https://www.youtube.com/watch?v=FsB7jdkmGlM

This resource was the very first programming I ever did in FiveM. The concept of DUIs really fascinated me, and the first thing I thought about was how it could be used to implement a graffiti system. It was an interesting choice to pick as the first thing to program, mainly because I needed to utilize a lot of different aspects of FiveM modding. For the DUI itself, I needed to create an interface that could interact with Lua which then could be displayed on an asset I made, and that asset also had to be transparent but still have collision etc... 


### Native Text Editing (no DUI)
Video: https://www.youtube.com/watch?v=A9OqGk6vRp8

One of the big downsides of using DUI is the heavy computational requirements, with this project I wanted to see if using the native DUI-like (i.e., 3D ScaleForms) functionality that is included in GTA could be used as a replacement. This project was really interesting because there wasn't that much research out there about using 3D ScaleForms, so I had to do a lot of digging through the decompiled scripts to see how they could be used. Although, you can get some nice results, performance is not that much better and you are much more limited in what you can do.

### Screen to World
Video: https://www.youtube.com/watch?v=f-o5Ykcn2oA

Before I got into FiveM programming, I had a period where I really was into learning low-level graphics programming. One aspect of this which I really found fascinating was the ability to convert screen coordinates to world coordinates and vice versa. The main reason why I wanted to implement this in FiveM was to improve the ability to interact with the envirnonment using the mouse (mainly for stuff like selecting objects, placing them, or removing them. There was quite a bit math I had to figure out to implement this properly, and especially optimization was also a big part of it. I think nowadays this fuctionality has actually been converted into a Cfx native, but it still was an interesting learning experience.

### Pool
Video: https://www.youtube.com/watch?v=zF0L7yxJmnI

Because physics and (especially) client synchronization in FiveM are a bit wonky, I decided I would make my own small physics engine that I could use to implement the pool game. At the time m so I had to do a lot of research on how the physics behind a pool game would work. This was pretty fun, because the "FiveM" aspect of this project mainly came down to optimizing.

### Cargo plane loading
Video: https://www.youtube.com/watch?v=a18sZxt1Bz8

I knew that there was a vehicle in the base game that could pick up containers and such, so I was curious to see how far I could take and maybe make it into a proper mechanic. Implementing it did require a lot of small things I had to do make sure that it worked properly (i.e., calling of the plane, picking up the container and loading it into the plane without the plane exploding), which did involve trying out a lot of different natives, and options for those natives.

### Spray paint truck
Video: https://www.youtube.com/watch?v=S1tegaHBMJQ

This was mainly a pure for fun project where I wanted to see if I could make a sort of custom vehicle that had custom functions (i.e., being able to paint other cars and shoot bombs). Pretty fun, but nothing too special.

### Custom Weather
Video: https://www.youtube.com/watch?v=wQnz-VvuMnA </br>
Video: https://www.youtube.com/watch?v=6JHsseZNOgc

One thing that, at least at the time, that wasn't well documented in FiveM is the ability to add custom weather or change existing one. This project was pretty interesting because it involved a lot of trying out random stuff to see the impact of certain parameters (and there were a lot of parameters). Pretty interesting, and has quite a lot of potential to integrate it with other mechanics.

### Forensics
Video: https://www.youtube.com/watch?v=5jj9avT1MFw

The goal of this project was to see out how ThreeJS could be incorperated within FiveM UIs to allow for easier interaction with 3D objects, as well as customizing these objects with certain decals (e.g., blood).


### Dog Fight
Video: https://www.youtube.com/watch?v=0uQOqqBC8iM

I heard several people always talk about how animals in GTA have this one shot mechanic where it essentially makes it impossible to have proper systems with them. After a while, I got curious and wanted to see if I could somehow disable the animal execution stuff. After a lot of trial and error with several natives, and native combinations I was able to figure out how to do it and used to implement a simple dog fighting system that uses custom damage but still utilized the default combat AI (in combination with tasks to fine-tune it). 

### Scratch Ticket
Video: https://youtu.be/GXzAVj_8tEE

Very simple resource, a 3x3 grid with scratch ticket mechanics. I probably want to extend this so players will be able to freely choose the symbols, rarity, and payout.

### Hacking Minigames
Video Minigame 1: https://youtu.be/1qCpW5LWsxA </br>
Video Minigame 2: https://youtu.be/we_t7vMoCSg </br>
Video Minigame 3: https://youtu.be/ywEALrKMPuw
A very common thing to see every server. Nothing too special, but wanted to see if I could replicate some hacking minigames that appear in other games.

# RedM-Projects
### Rust/Valheim like build system
Video: https://www.youtube.com/watch?v=-QwgvTx2zyQ

One of my most favourite resource I made, essentially a building system that is very similar to those in certain survival games. This was a pretty difficult thing to make, partially because it was made in RedM. The first thing that I decided when I thought of the idea was to not look up any code on how other people implemented similar stuff in game engines like Unity or Unreal, I purely wanted to learn how to do this on my own. For a lot of the object rotations I had to rely on quaternions, which is something I wanted to do for a long time as well. Although I had some basic knowledge of quaternions, I still needed to do some research on how to properly do the rotations and such (it's a fun topic, but sometimes it does feel like magic tbh). 

### Drag mechanic
Video: https://www.youtube.com/watch?v=g9v-2ErVIHI

I knew that there was a drag mechanic in one of the campaign missions but I was curious to see if it would work in multiplayer (and be synced). Based on the decompiled scripts I created this small resource where a player could drag another player once they were surrendering.

### Horse custom prop attach
Video: https://www.youtube.com/watch?v=o-eLTuopcAg

When I was looking through the different objects in RedM I found this attachment for a horse which didn't have anything attached at the end. I used this as the perfect opportunity to design a system where certain types of object could be attached to the end of the horse attachment.

### Vulture leading to downed players
Video: https://www.youtube.com/watch?v=fsXsohMPrlM

Because RedM doesn't have the concept of phones or the ability to alert EMS, I wanted to think of another method to inform players of a nearby downed player. I really liked this project because I do think that it's a pretty immersive way to alert other players. It also required a lot of trial-and-error to make it feel good (e.g., birds flying away when the player gets close, increasing bird size...).

### Hot Air Balloon
Video: https://www.youtube.com/watch?v=U5hYrVzZFbs

This mechanic was fairly easy to implement, but as with all RedM things, there was very little research done on how to do it. The coding aspect mainly came down to using the decompiled scripts to know which natives, model, controls to use where and in which order.

### Bear Trap
Video: https://www.youtube.com/watch?v=d1XhuhHXKm0 (player runs fast => traps gets stuck on player) </br>
Video: https://www.youtube.com/watch?v=kC5nDSczE8U (player runs fast => player trips) </br>
Video: https://www.youtube.com/watch?v=Kbqa5I2W8Zo (player walks => both player and trap are stuck in place)

I found a bear trap model and then looked through the decompiled scripts to see if it was every actually used. Discovered that it actually was used somewhere, and that there were entity animations for it. Sadly, the bear trap itself had no fuctionality so I had to manually code the detection logic, closing, and impact on the player when he sets of the trap.
