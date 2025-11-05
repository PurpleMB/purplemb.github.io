---
layout: post
title:  "Boba Eye"
date:   2025-03-21 12:16:30 -0600
prev-page: /projects
prev-page-name: Projects
topic-list: Event-driven Programming, ScriptableObjects, Dialogue Systems, Shaders, Decoupling
description: <span class="book-title">Boba Eye</span> is a cozy 2D game about creating drinks for a cast of cute critters. It utilizes tools such as ScriptableObjects and Event Channels to keep systems designer-friendly, extensible, and decoupled. It also uses some fun shaders to create unique-looking drinks!
preview_img: /assets/gifs/drinkgame-preview-rough.gif
engine: Unity(C#)
role: Programmer & Designer
team-size: 2
sections: Introduction, Scriptable Objects, Event Channels, Shaders, Lessons
section-anchors: intro, scriptableobjects, channels, shaders, lessons
---

<div class="overview">
    <span class="overview-title">Overview</span>
    <br>
    <p>
        <span class="book-title">Boba Eye</span> is a casual game about making bubble drinks developed in Unity. During development, constructing systems that were <span class="accent">data-driven</span> and <span class="accent">decoupled</span> was a top priority. <span class="accent">ScriptableObjects</span> and <span class="accent">Event Channels</span> were two of the most important tools utilized to keep systems extensible and untangled. As an extra little treat, <span class="accent">shaders</span> helped to provide some visual flair and diversity to the primary gameplay task of making drinks!
    </p>
</div>

<span class="anchor" id="intro"></span>
<div>
<p class="section-title">
Introduction
</p>

<p>
Reflecting on my experiences with previous development projects, namely <span class="book-title">PUNCHERMAN!</span>, I began <span class="book-title">Boba Eye</span> with one main directive: constructing a game that I could return to and develop over time. After navigating the rather large amount of tech debt <span class="book-title">PUNCHERMAN!</span> accumulated during its first development cycle, I gained a renewed appreciation for the necessity of constructing systems that are durable, easily understood, and easily extended. Where we had spend months untangling messy, codependent systems to add new elements to <span class="book-title">PUNCHERMAN!</span>, I wished to be able to occasionally return to <span class="book-title">Boba Eye</span> and easily add in a new character or an additional component to the drink construction process.
</p>       

<p>
In order to achieve this, I would need a project capable of being easily understood again after some time away. Forming systems that function independently, thus reducing the number of elements requiring direct manipulation at any time, would ease the process of re-learning the game's workings. Additionally, designing systems to be data-driven would allow me to make defining new game content largely a matter of creating new data to feed into existing, flexible systems. As such, the paradigms I followed to help achieve my ultimate goal of a long-term supportable game were decoupling and being data-driven.
</p>       

<p>
With these core design principles in mind, I created documentation outlining the features and development roadmap of the game, noting which elements were absolutely essential and which would be nice to have someday. To construct systems adhering to my goals, I would need a strong understanding of what possibilities each system must be capable of handling and which systems would be in communication with each other. During <span class="book-title">PUNCHERMAN!</span>, I learned how great the challenge can be to adapt a system to accomodate previously unconsidered possibilities. Thus, this early mapping of game systems, their interactions, and possible future additions would help to construct stronger systems capable of handling continued development.
</p>

<span class="anchor" id="scriptableobjects"></span>
<div>
<p class="section-title">
Scriptable Objects
</p>

<p>
This paragraph should explain what scriptableobjects are. They are scene-independent assets capable of containing variables and code outside of the MB lifecycle.
</p>     

<p>
This paragraph will go on to explain how SOs can be used to provide information and implementations to be used by MB objects to make those classes more flexible and decoupled.
</p>       

<p>
This paragraph will explain that they also make it easier to expose data for non-programmer designers to interact with. In this way, they ease development for both parties.
</p> 

<p>
This paragraph will now explain an example of the SOs being used in the project: customer data.
</p>  

<span class="anchor" id="channels"></span>
<div>
<p class="section-title">
Event Channels
</p>

<p>
This paragraph will now explain Event Channels as a combination of event-driven programming and SOs. 
</p>  

<p>
This paragraph will explain how Event Channels reduce the amount of information listeners require, promoting decoupling.
</p>  

<p>
This paragraph will explain how they can serve to group related events from different sources.
</p>

<span class="anchor" id="channels"></span>
<div>
<p class="section-title">
Shaders
</p>

<p>
This paragraph will explain the need for shaders to represent a large number of possible drinks.
</p>  

<p>
This paragraph will explain the segment shader used to display the drink ingredients.
</p>  

<p>
This paragraph will explain how a simple effect can be used to make the stirring shader.
</p>  

<p>
This paragraph will go into using noise and randomization to create dynamic shaders like the finished shader.
</p>  

<span class="anchor" id="lessons"></span>
<div>
<p class="section-title">
Lessons Learned
</p>

<p>
This paragraph will acknowledge some of the successes of the BE architecture: capable of quickly defining new characters, flavors, etc.
</p>     

<p>
This paragraph will now go on to introduce some areas that could have gone better: such as systems becoming overengineered, difficulties with sprite layering and collision, and potential pitfalls with SOs and Events.
</p>  

<p>
This paragraph will explore the overengineering that happened and go into ways to prevent that in the future. Ways: clear, subdivided tasks; more planning.
</p>

<p>
This paragraph will explore issues with sprite layering and collision and discuss issues.
</p>  

<p>
This paragraph will explore issues with SOs and Events, such as being prone to editor corruption or potentially being hard to debug if sources become unclear.
</p>  

<p>
This paragraph will conclude the article by saying BE was a great experience that helped to learn about developing extensible systems and such.
</p>

