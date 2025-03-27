---
layout: post
title:  "PUNCHERMAN!"
date:   2025-03-20 12:16:30 -0600
prev-page: /projects
prev-page-name: Projects
topic-list: AGILE Development, User Interface, Playtesting, Player Communication, Steam
description: PUNCHERMAN! is a comedic first-person dad simulator where the player is tasked with completing chores despite only being able to punch. Developed in Unity across two development cycles, PUNCHERMAN! is currently free to download on Steam.
preview_img: /assets/gifs/puncherman-preview.gif
engine: Unity (C#)
role: Programmer & Designer
team-size: 8
itch-link: https://noahkuhn.itch.io/puncherman
steam-link: https://store.steampowered.com/app/2364050/PUNCHERMAN_First_Day/
video-link: https://youtu.be/wZH0PFK7jYw
sections: Introduction, AGILE, UI, Playtesting, Steam, Lessons
section-anchors: intro, agile, ui, playtesting, steam, lessons
---

<div class="overview">
    <span class="overview-title">Overview</span>
    <br>
    <p>
        PUNCHERMAN! was developed utilizing <span class="accent">AGILE techniques</span> across two development cycles before an eventual <span class="accent">release on Steam</span>. My work on the game as a programmer and designer ranged from developing the audio systems to <span class="accent">gathering playtest feedback</span>. However, the aspect of the game that I am most proud of is the work I did crafting thematic, <span class="accent">diegetic UI elements</span> that mesh with the world and gameplay of PUNCHERMAN!.   
    </p>
</div>

<span class="anchor" id="intro"></span>
<div>
<p class="section-title">
Introduction
</p>

<p>
PUNCHERMAN! was born as a capstone project being worked on by an interdisciplinary team of 6 members, including myself. Utilizing AGILE development practices, we nurtured the game from preproduction and prototyping through playtesting and refinement until reaching our initial launch on Itch.io.
</p>     

<p>
After a period of dormancy, PUNCHERMAN! re-entered development with a new team, containing 2 returning members and 2 new members. Armed with the knowledge gained from the previous development cycle, we iterated on virtually every aspect of the game. After months of redefining the visual style, game design, and underlying code architecture we released the game for free on Steam under the name PUNCHERMAN!: FIRST DAY.
</p>

<p>
Ultimately, PUNCHERMAN! came together as a comedic, first-person game that blends elements of puzzle, simulation, and classic shooter games to create a stylish and charming experience that I am still proud to have been a part of. While it may not be perfect, I can attest to the love and learning that went into PUNCHERMAN! over the course of more than a year.
</p>
</div>

<span class="anchor" id="agile"></span>
<div>
<p class="section-title">
AGILE Development
</p>

<p>
At the risk of sounding like a broken record, PUNCHERMAN!'s development was structured using AGILE methodology. From the onset of the project, we had a dedicated SCRUM master who ensured everyone adhered to a schedule of daily standups and regular sprint review and planning meetings. At these meetings we maintained, updated, and added to our project development board, being sure to note any tendencies in time estimation and consumption in order to improve our timeline management as the project progressed.
</p>

<p>
Due to the environment that the initial development of PUNCHERMAN! was taking place in, it was paramount that we maintained a firm grasp on our development timeline in order to meet playtest and release deadlines (an aspect of the project I will delve into later). As such, having a framework for project organization and communication that granted us the ability to easily determine development velocity and priorities leading up to these deadlines was invaluable.
</p>

<p>
The consistency and frequency of this communication also ensured that every member of the team had a solid idea of how each facet of development was progressing. Due to the horizontal nature of the development team's structure, this unified understanding of the project's formation and growth ensured that we were constantly able to source new ideas and solutions from all members of the team. 
</p>


<p>
As the project advanced from early documentation and prototyping, we gained a larger and larger pool of data with which to evaluate our own capabilities. Once the time for playtesting arrived, the time spent cultivating an understanding of the production realities of our team granted us a clearer view of the ways we would be able to adjust in tandem with player feedback. 
</p>

<p>
AGILE, ultimately, provided us channels for communication and evaluation that allowed us to better define the possibility space of development. The mixture of restriction and freedom this provided allowed us to parse feedback more effectively, collaborate more seamlessly, and, most importantly, actually ship the project. 
</p>
</div>

<span class="anchor" id="ui"></span>
<div>
<p class="section-title">
User Interface
</p>

<p>
Something every game needs and that many developers dread: a user interface. During the course of PUNCHERMAN!'s development, I wound up gravitating towards being the programmer primarily responsible for building out the UI elements of the game. However, far from being a cross I bore through development, the various screens, menus, and indicators of PUNCHERMAN! are features I am thrilled to have been able to construct alongside the visual artists.
</p>

<p>
From the beginning of the project, we knew we wanted to lean heavily into the comedic aspects of the fact that this is a game, despite any other pretensions, about being a dad. The first area of the game is a suburban neighborhood and the quests feature such fantastical feats as "doing laundry" or "buying groceries". As such, we knew that the standard slew of sleek, serious interface designs seen in other games weren't going to fit our needs.
</p>

<ul class="img-row">
    <li>
        <img src="/assets/gifs/wallet.gif" height="150">
    </li>
    <li>
        What dad  doesn't have a wallet crammed with too many cards?
    </li>
</ul>

<p>
As the game takes place in a largely realistic setting, we considered the everyday objects people, and particularly dads, might have to facilitate their daily activities. Thus, classic symbols of fatherhood, such as an iconic leather wallet or sticky notes haphazardly scrawled with to-dos, became obvious choices to present standard UI information in a more thematically-appropriate manner.
</p>

<ul class="img-row">
    <li>
        <img src="/assets/gifs/journal-ui.gif" height="150">
    </li>
    <li>
        <img src="/assets/gifs/stopwatch.gif" height="150">
    </li>
    <li>
        Most UI elements have some element of physical movement to them.
    </li>
</ul>

<p>
As most elements of the UI were now tangible objects, as opposed to abstract boxes filled with information, I made sure to pay attention to developing the ways the UIs presented themselves to and interacted with the player. For example, the stopwatch and journal gradually move in and out of the screen, serving to evoke an object being removed from a pocket instead of a menu materializing in view. 
</p>

<p>
These animations are a mix of "static" animations made using the Unity animator window and "dynamic" animations driven by interpolating and manipulating position values via code. During the second development cycle, the adoption of DOTween for use in the project made the development of more complex animations, such as the stopwatch's rolling, much easier to adjust and tweak.
</p>

<p>
Overall, I spent considerable time and effort striving to create a set of interfaces and menus that worked to build and deepen the themes of the game as much as the gameplay itself. During playtesting, the glowing praise testers gave to innocuous and often forgettable elements, such as the travel loading screen, served to vindicate these efforts.
</p>
</div>

<span class="anchor" id="playtesting"></span>
<div>
<p class="section-title">
Playtesting
</p>

<p>
PUNCHERMAN! is, in some ways, an unorthodox game. It strives to deliver fairly standard gameplay filtered through a level of genre commentary that primarily manifests in limiting the way the player interacts with the game world. Or rather: it's a game where pretty much all you do is punch things, even things you would really rather not punch.
</p>

<p>
As PUNCHERMAN! was, from its inception, predicated on the idea of limiting the player, we had to spend considerable time finding out how to do that in a way that wasn't frustrating or obtuse. This is where another development boogeyman appeared to save the day with some tough love: playtesting.
</p>

<p>
PUNCHERMAN! had, truth be told, some rough playtests. As PUNCHERMAN! showcased what was supposed to be a beta build, we got one resounding piece of feedback: "I don't know what I'm doing, and whatever I am doing is not fun".
</p>

<p>
Playtesting is, ultimately, an exercise in translation. Players give you feedback, but filtered through an entirely different relationship to the game than a developer. With the additional context clues of notes gathered during live play sessions, it then falls to the developer to translate "I don't know what I'm doing" into something concrete like "The feedback for actions doesn't let me know if I did them successfully".
</p>

<p>
Thus, we had two main tasks: translate what "I don't know what I'm doing" and "Whatever I am doing is not fun" into actionable changes we could make to the game given our development constraints.
</p>

<p>
The issue of player communication expressed by "I don't know what I'm doing" was a fairly easy problem to triage. Observing players revealed very obvious shortcomings in aspects of the game, such as the level design and art direction, that were making it difficult for players to dig into the game.
</p>

<ul class="img-row">
    <li>
        <img src="/assets/gifs/busstop.gif" height="150">
    </li>
    <li>
        <img src="/assets/gifs/pb.gif" height="150">
    </li>
    <li>
        Turns out, people look at the objects that are actually visible.
    </li>
</ul>

<p>
The solution was, of course, simply to communicate more with the player. Some changes required only implicit information (such as coloring important objects more brightly) while some mandated we swallow a bit of pride and just tell the player something (the task UI telling the player how to check their tasks). Regardless, making it easier for the player to simply gain comprehension about the game and its possibility space led to more testers actually having meaningful game experiences.
</p>

<p>
Beyond that, however, lay the much more troubling sentiment of "Whatever I am doing is not fun". We did not have the ability to completely rebuild the game mechanics, so we had to identify ways that the existing systems could be leveraged into more enjoyable gameplay moments. Considering that the game was built around the comedy of doing everyday tasks via punching, it seemed our only recourse was to lean into that as much as possible.
</p>

<p>
Thus, we got to work making changes such as adding a host of particles to every punch, making more objects in the world punchable, and just generally increasing the sense of chaos and exploration the player was able to express through their punches. As it turns out, in a game with one central mechanic you don't have too many places to look to in order to improve the gameplay experience.
</p>

<ul class="img-row">
    <li>
        <img src="/assets/gifs/store.gif" height="150">
    </li>
    <li>
        There's no chaos like physics-object chaos.
    </li>
</ul>

<p>
The best example of these changes is the grocery store. Shopping as a task was present from the very first build of the game, though it experienced almost constant evolution through development. Early on, there was a level of restraint in terms of asking questions like "how can we have the player get a fruit into the cart by punching it?". By the end of development, the question had shifted to something more akin to "how many fruits need to be in this pile that when it explodes from a punch some fly into the cart?".
</p>

<p>
That paradigm shift, of going from ways to work around punching as a limitation to designing the world to accommodate punching as a fun activity, marked a change in our understanding of the game that would not have occurred without getting a lot of negative playtest feedback. We continued to showcase PUNCHERMAN!, even getting to go to Unity Developer Day at Unity's Austin office, and each time feedback got better and better as we learned ways to leverage feedback into an improved understanding of the game.
</p>
</div>

<span class="anchor" id="steam"></span>
<div>
<p class="section-title">
Steam Release
</p>

<p>
After around a year of collective active development, it was time for PUNCHERMAN! to fly the coop of its itch.io nest. After receiving industry guidance from some of the lovely folks over at Graffiti Games, we began navigating the process of obtaining Steam certification.
</p>

<p>
While not quite the impenetrable bastion that it once was, seeking certification from Steam did mandate that we reach a level of consistency, usability, and compatibility that is less than certain after a game undergoes two distinct periods of development with two different teams. Ultimately, we utilized the extensive amount of feedback that we had already gathered in terms of player communication, user controls, and interface presentation to craft a more unified, market-ready version of the game to submit for certification.
</p>

<p>
After a review process that went surprisingly smoothly, PUNCHERMAN! was ready to take the next step towards becoming a "real game". Despite being a small drop in the Steam bucket, releasing PUNCHERMAN! was a fantastic moment for the game and a great learning experience as we explored the asset and software requirements of being on an organized storefront. For a time after launch, PUNCHERMAN! even had an few speedrunners competing for records (and of course also competing to discover how many bugs we had missed).  
</p>
</div>

<span class="anchor" id="lessons"></span>
<div>
<p class="section-title">
Lessons Learned
</p>

<p>
PUNCHERMAN! was, when all is said and done, a learning experience. Having walked the long, winding road from preproduction to post-release, I now possess a greater understanding of and appreciation for the fine mixture of adaptability and clarity required to navigate long-term development.
</p>

<p>
We didn't always find a perfect balance, some aspects of the game linger as fossils of designs and ideas abandoned as we struggled to retool the game into at least being playable and fun, but we did always strive to do better than we'd done before. 
</p>

<p>
Having recently read <span class="book-title">Blood, Sweat, and Pixels</span> and seeing similar tails of attempts to wrangle or redirect the chaos of making games, I feel confident in saying that if I had to take only a single lesson from the development of PUNCHERMAN! it would be this understanding of games and their development as living, imperfect things. I say this not to condone our shortcomings on this project but to acknowledge the ways I can leverage the experience of them into becoming a stronger developer.
</p>

<p>
Beyond such intangible niceties, however, do lie some concrete technical lessons from PUNCHERMAN!. 
</p>

<p>
First and foremost: code architecture. It's important. Always have a clear idea of what your systems need to accommodate and ways to ensure they can do so cleanly. When PUNCHERMAN! returned to active development, a considerable amount of time was spent relearning the pathways of code previously carved and then trying to redirect those channels to be more conducive to further development. The methods of inter-object communication used were, for example, not adequately flexible or durable and caused considerable headache as we expanded the game.
</p>

<p>
Additionally, game state was managed primarily through a mixture of eye-shutting and ear-plugging for most of development. This led to haphazard attempts to manage state in the moments we identified it necessary, leading to less than ideal solutions that engendered gameplay inconsistencies and a lack of player agency. If you ever find yourself softlocked or just disappointed the game erased something you did then you have felt the consequences of our mistakes on this front.
</p>

<p>
While I could continue to enumerate every single misstep and its corresponding lesson from PUNCHERMAN!, that would prevent me from continuing to make more mistakes and learn more lessons on other projects. I am, despite anything else, grateful for every aspect of PUNCHERMAN!'s development and will strive to continue to learn from it and my future endeavors.
</p>
</div>

