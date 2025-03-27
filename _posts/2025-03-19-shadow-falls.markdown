---
layout: post
title:  "Shadow Falls"
date:   2025-03-19 12:16:30 -0600
prev-page: /projects
prev-page-name: Projects
topic-list: Gameplay Systems, World Design, Game Jams
description: Shadow Falls is a puzzle game built around an innovative, multi-object shadow puzzle system. Created in Unity for Texas Game Jam, Shadow Falls was lauded for its novel tech and charming narrative.
preview_img: /assets/gifs/shadowfalls-preview.gif
engine: Unity(C#)
role: Programmer & Designer
team-size: 2
itch-link: https://purpleml.itch.io/shadow-falls
video-link: https://youtu.be/uZlRKLsu1sc
sections: Introduction, Shadow Puzzles, World Design, Lessons
---

<div class="overview">
    <span class="overview-title">Overview</span>
    <br>
    <p>
        Shadow Falls was a <span class="accent">jam game</span> created over the course of two days for Texas Game Jam. During its rapid development, I deepened my understanding of ways to twist standard game development concepts to <span class="accent">create novel gameplay systems</span>. The focal point of the game was its award-winning <span class="accent">shadow puzzle system</span>, which applied everyday graphics techniques in inventive ways to faciliate unique gameplay. Beyond that, however, its failures in areas such as <span class="accent">world design</span> and player communication also provided valuable development insights.
    </p>
</div>

<div>
<p class="section-title">
Note
</p>

<p>
Many of the topics discussed in this article, and more, are also addressed in a postmortem I have previously written for the game on its itch.io page. If you wish to see another deconstruction of the lessons gleamed from the development of this project, feel free to read that post <a href="https://purpleml.itch.io/shadow-falls/devlog/438456/shadow-falls-design-analysis-production-to-post-mortem" target="_blank">here</a>. 
</p>

</div>

<span class="anchor" id="Introduction"></span>
<div>
<p class="section-title">
Introduction
</p>

</div>

<span class="anchor" id="Shadow Puzzles"></span>
<div>
<p class="section-title">
Shadow Puzzles
</p>

</div>

<span class="anchor" id="World Design"></span>
<div>
<p class="section-title">
World Design
</p>

<p>
The world design of Shadow Falls serves as a microcosm of many of the design issues that held the game back in spite of its better ideas. Simply put: it doesn't help the player have fun. Many players were left stumbling around a relatively barren, if pretty, world trying to find where exactly we had hidden the fun stuff.
</p>

<ul class="img-row">
    <li>
        <img src="/assets/imgs/sfmap.jpg" height="150">
    </li>
    <li>
        If I removed the magenta dot, could you determine where the game started?
    </li>
</ul>

<p>
The image above shows an annotated aerial view of the game world. The magenta dot indicates the player spawn, lime dots indicate the location of puzzles, and the red lines indicate the visible pathways in the world. 
</p>

<p>
Upon seeing this image, something immediately becomes apparent: this world has no direction. If I removed the magenta dot, there is nothing in the construction of the surrounding area and its pathways that would lead one to conclude the game starts there. Additionally, the puzzles do not seem to be arranged in any fashion that provides the player an idea of which order to tackle them in. Beyond the spatial clue of the easiest puzzle being directly by the spawn, every puzzle may as well have been randomly placed. Finally, the cyclical nature of the central pathway introduces a strong sense of adirectionality that is only deepened by the way in which offshooting paths fail to reinforce any sort of structure.
</p>

<p>
When designing this world layout, I was attempting to provide the player a "free" and "unpressured" experience. However, in my uncritical attempts to do so I wound up making a world that is not designed to be navigated in a fun, intuitive way. In the time since the development of Shadow Falls, I have come to appreciate the ways in which adding some degree of structure and linearity can serve to augment and strengthen the sense of freedom provided by a game. If, instead of giving the player full freedom from the start of the game, I had placed them in a linear area that opened up into a freeform experience, then I am sure many more players would have walked away happy and feeling a sense of agency.
</p>

<ul class="img-row">
    <li>
        <img src="/assets/imgs/sfmapimproved.jpg" height="150">
    </li>
    <li>
        A mixture of linearity and freedom leads to more parsable, navigable game worlds.
    </li>
</ul>

<p>
If we consult this second, admittedly ugly, map then we can begin to image a way that Shadow Falls could have been structured to better accomodate a mixture of player direction and exploration. On this version of the map, geographical features, such as the lake, can be used to constrain the play space in a way that feels inoffensive. Thus, the designer can be certain where the player is actually going as they play the opening stretch of the game. Once the player has been properly introduced to the game and its mechanics, they can be given choices as seen in the triangle of puzzles at the southern end of the map. After the player has made a choice, the world then provides a way for the player to navigate back towards the path they did not travel by connecting them with a new, enticing path for the player to explore. 
</p>

<p>
While relatively simple and ripe for further improvement, a world designed in this way is much more understandable at both the macro and micro levels. A designer is able to have some degree of confidence in the order the player will progress through the game world while still facilitating player choice. Additionally, the player will, despite technically having less freedom, likely feel more engaged by the freedom they are later given as they have been placed in a space that wants to be explored.
</p>

<p>
As stated at the beginning of this section, this uncritical approach to player communication and freedom extends to other areas of the game, such as the tutorializing of the puzzle mechanics. As in this case, many of these related issues could be solved by a stronger balance between player agency and intentional design. In all, the failures of the world design of Shadow Falls serve as a good lesson in the ways that linearity and openness must be managed in all aspects of development.
</p>
</div>

<span class="anchor" id="Lessons"></span>
<div>
<p class="section-title">
Lessons Learned
</p>

</div>

