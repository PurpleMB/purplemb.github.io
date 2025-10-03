---
layout: post
title:  "Monster Curiosity Calculator"
date:   2025-10-01 12:16:30 -0600
prev-page: /projects
prev-page-name: Projects
topic-list: API Querying, Database Interaction, User Interfaces, Libraries
description: Monster Curiosity Calculator is a statistics application created in C++. It utilizes the DearImGui library to facilitate user interaction with an SQLite database that is populated with data about pocket-sized monsters!
preview_img: /assets/gifs/drinkgame-preview-rough.gif
tools: C++, SQLite, Dear ImGui, Python 
role: Programmer & Designer
team-size: 1
sections: Introduction, API Querying, Database Creation & Interaction, User Interface Development, Lessons
section-anchors: intro, api, database, interface, lessons
---

<div class="overview">
    <span class="overview-title">Overview</span>
    <br>
    <p>
        <span class="book-title">Monster Curiosity Calculator (MCC)</span> is a <span class="accent">database-driven</span> statistics application developed to help answer niche questions about pocket-sized monsters. It uses a <span class="accent">Python</span> script to query an existing <span class="accent">RESTful API</span>, gathering all needed data into an easy to parse file. That data is then processed in a <span class="accent">C++</span> application to generate a <span class="accent">SQLite database</span> that can be interacted with using a GUI developed using the <span class="accent">Dear ImGui</span> library.
    </p>
</div>

<span class="anchor" id="intro"></span>
<div>
<p class="section-title">
Introduction
</p>

<p>
I've always had a desire to know obscure statistics regarding the places I am or the media I am interacting with. Frequently during my degree, for example, I would wonder at the average population of each floor of the library over the course of different days of the week (I wanted to be on the least populated floor). As a lifelong fan of battling pocket-sized monsters, I have similarly wondered about the properties of arbitrary subsets of possible monsters. "If I created two groups, each containing only monsters of certain types, which would tend to be faster?" As such, when I began to develop my skillset at interacting with SQL databases the first thought that came to my mind was, "Perhaps I can use this to finally answer all those little questions that pop into my mind." 
</p>

<p>
I decided to take this idea as an opportunity to experiment with a number of different libraries and languages, breaking the project up into the rough phases of data acquisition, database creation and interaction, and user interface development. The project began with a Python script that gathers all necessary data from an existing API, before transitioning to C++ development for creating the database environment as well as the interface users may use to interact with the database.
</p>

<p>
Ultimately, I continued to develop the functionality and ease-of-use of <span class="book-title">MCC</span> until I felt I had achieved the goal I set out with: making a tool that allows calculating extremely niche and specific statistics about fictional monsters. To accomplish that goal, I gained knowledge on API usage, data processing, database usage, UI development, and developing flexible code systems.
</p>

<span class="anchor" id="api"></span>
<div>
<p class="section-title">
API Querying
</p>

<p>
When beginning the development of <span class="book-title">MCC</span>, I began by evaluating the data requirements of the task at hand. Ultimately, I was looking to generate a database with 1000+ columns each comprised of 20+ rows. Additionally, I wanted to generate an intermediate, human-readable file that would be dynamically converted into a database. This approach would allow me to more easily change the information gathered/processed and allow for easier database restoration in the event the database file was corrupted or lost.
</p>

<p>
Fortunately, during a previous project I had gained experience interacting with <a href="https://pokeapi.co/" target="_blank">PokéAPI</a>, a RESTful API with an intuitive and easy to process data structure. Python seemed like the natural tool to use to quickly develop a script that would 
</p>     

<span class="anchor" id="database"></span>
<div>
<p class="section-title">
Database Creation & Interaction
</p>

<p>
This section has not been written yet!
</p>     

<span class="anchor" id="interface"></span>
<div>
<p class="section-title">
User Interface Development
</p>

<p>
This section has not been written yet!
</p>     

<span class="anchor" id="lessons"></span>
<div>
<p class="section-title">
Lessons Learned
</p>

<p>
This section has not been written yet!
</p>    

