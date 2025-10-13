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
repo-link: https://github.com/PurpleMB/MCC
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
I've always had a desire to know obscure statistics regarding the places I am or the media I am interacting with. Frequently during my degree, for example, I would wonder at the average population of each floor of the library over the course of different days of the week (I wanted to be on the least populated floor). 
</p>

<p>
As a lifelong fan of battling pocket-sized monsters, I have similarly wondered about the properties of arbitrary subsets of possible monsters. "If I created two groups, each containing only monsters of certain types, which would tend to be faster?" As such, when I began to develop my skillset at interacting with SQL databases the first thought that came to my mind was, "Perhaps I can use this to finally answer all those little questions that pop into my mind." 
</p>

<p>
I decided to take this idea as an opportunity to experiment with a number of different libraries and languages, breaking the project up into the rough phases of data acquisition, database creation and interaction, and user interface development. The project began with a Python script that gathers all necessary data from an existing API, before transitioning to C++ development for creating the database environment as well as the interface users may use to interact with the database.
</p>

<p>
I continued to develop the functionality and ease-of-use of <span class="book-title">MCC</span> until I felt I had achieved the goal I set out with: making a tool that allows calculating extremely niche and specific statistics about fictional monsters. To accomplish that goal, I gained knowledge on effective API querying, data processing, database usage, UI development, and designing flexible code systems.
</p>

<span class="anchor" id="api"></span>
<div>
<p class="section-title">
API Querying
</p>

<p>
When beginning the development of <span class="book-title">MCC</span>, I began by evaluating the data requirements of the task at hand. Ultimately, I was looking to generate a database with 1000+ columns each comprised of 20+ rows. Additionally, I wanted to generate an intermediate, human-readable file that would be dynamically converted into a database. This approach would allow me to more easily change the information gathered/processed and allow for database restoration in the event the database file was corrupted or lost.
</p>

<p>
Fortunately, during a previous project I had gained experience interacting with <a href="https://pokeapi.co/" target="_blank">PokéAPI</a>, a RESTful API with an intuitive and easy to process data structure. Knowing that the later parts of this project would take place in C++ (I had decided by this point to construct the eventual GUI in C++), I elected to create the script for querying the API in Python due to its easy to use networking libraries.
</p>     

<p>
<a href="https://pokeapi.co/" target="_blank">PokéAPI</a> contains a truly massive amount of data, much of which is simply not pertinent to <span class="book-title">MCC</span>. As such, the key purpose of the querying script was to identify the list of queries containing information I did require, obtain the data from those queries, and prune down the obtained information to contain only the data which I cared about.
</p>

<p>
Using <a href="https://pokeapi.co/" target="_blank">PokéAPI</a>, I was able to retrieve a list of all monsters with query links to additional information for each monster. With this list I could construct a dictionary of information for each monster, ultimately combining all the entries together into a single JSON file. This cumulative JSON file, thanks to its list & dictionary structure, was easy to visually evaluate, making debug quick as well as making it easy to maintain a connection between column names and values for easier database generation.
</p>

<p>
The data for a single monster is comprised of information relating to that monster, its overall species, and its specific form, meaning that to generate the compiled information for 1000+ monsters required more than 3000 queries. This number of requests, when processed in sequence, could lead to data gathering taking almost a minute. During the process of development, where I was frequently regathering data to fix bugs or add new data fields, this meant that I was spending significant amounts of time simply waiting for my data to compile. 
</p>

<p>
Each final entry is independent of each other final entry. As such, instead of processing each query in sequence it was possible to break them up into ~1000 asynchronous groups each containing only a few queries. Switching to this asynchronous request grouping drastically reduced the time needed to regather my data, reducing it to typically less than 10 seconds. As such, I had completed the first phase of <span class="book-title">MCC</span> by developing a script that allowed me to quickly and easily gather the large amount of data needed for my database.
</p>

<span class="anchor" id="database"></span>
<div>
<p class="section-title">
Database Creation & Interaction
</p>

<p>
To contain and process the data generated by my Python script, I elected to utilize SQLite to form a database to serve as the heart of <span class="book-title">MCC</span>. I chose to use SQLite as opposed to other SQL flavors due to its self-contained nature, lightweight size, and intuitive C++ integration. These factors combined to make SQLite an ideal choice for my application devoted to processing static data without the need for a central remote database or server.
</p>     

<p>
SQLite features excellent C++ support that allows for the easy conversion of simple string data to SQL queries that can be efficiently evaluated in a number of ways. SQLite's statement preparation system works by outlining the statement fields before sanitizing and substituting in the specific statement values. As such, it is easy to dynamically build statements capable of handling a wide range of situations. During this project, I frequently used a pattern of creating string "formats" that I could combine in different arrangements to handle the data refinement and value calculation features that I wished to support. This approach naturally synergized with the similar tactic used by SQLite, meaning that developing database features was primarily an exercise in pattern deconstruction.
</p>

<p>
Beginning with table creation, table schemas are comprised of a series of column specifications. As a typical schema has one row per column definition, I elected to develop a system wherein I could define an arbitrary list of column specifications where each entry contains information such as the name of the column, its data type, and any additional column arguments. This list is then converted to a single query that defines and populates a table using my previously gathered data. This system allowed me to maintain a large degree of flexibility, providing me the ability to easily modify the names and types of data processed as I iterated on the database and its source information.
</p>

<p>
Moving now to interaction with created tables, I proceeded by breaking queries up into three primary components: types, operations, and values. A query to the database is typically in the form:
<code>
SELECT * WHERE &#40;&lt;type&gt; &lt;operation&gt; &lt;value&gt;&#41;
</code>
. For example, to retrieve all Fire type monsters, we could evaluate something similar to: 
<code>
SELECT * WHERE &#40;'type' = "Fire"&#41;
</code>
. In this instance, our type is, funnily enough, "Type", our operation is "=", and our value is "Fire". It is easy to create a generic pattern that can be used to form any equation of this type, allowing for the utilization of the format system mentioned above. Furthermore, while using this pattern each parameter can be evaluated as a separate logical argument, allowing for any amount of parameters to be combined to form a detailed set of criteria. 
</p>

<p>
With some slight modifications to this approach, it is also easy to define a system for calculating values derived from database data. Mutating the previous approach to something like :
<code>
SELECT operation&#40;value&#41;
</code>, where 'operation()' is itself a format statement unique to each operation, we can achieve the same amount of uniformity and flexibilty as with parameter defintion. This approach, combined with SQLite's innate data cleaning while using the statement preparation system, allowed for the rapid formation of an easy to expand and secure system for defining and creating queries to the database.
</p>

<p>
Beyond these elements, the largest concern present was converting the raw database data to a prettier, user-facing format. To achieve this, I elected to use maps that were generated during the creation of each database "type". During type creation, when the list of possible values is being declared for the user to access, it was easy to add an additional stage linking raw values to the properly formatted "pretty" values. After a database query has been evaluated, the data, which is still associated with a column name, can be fed into the appropriate map to retrieve the data for use by the GUI.

<span class="anchor" id="interface"></span>
<div>
<p class="section-title">
User Interface Development
</p>

<p>
I utilized the <a href="https://github.com/ocornut/imgui" target="_blank">Dear ImGui</a> library to develop the interface for <span class="book-title">MCC</span> in C++. I chose to use <a href="https://github.com/ocornut/imgui" target="_blank">Dear ImGui</a> because it is open-source, allows for the rapid creation of a functional user-interface with only C++ code, and is designed to have functional similarities to the style of frame management and rendering used in video game engines. This allowed me to utilize some of my existing knowledge of graphics and game development while minimizing the amount of additional languages and tools required to create a user-friendly interface for my applicaiton.
</p>

<p>
Additionally, as I learned over the course of utilizing the library, <a href="https://github.com/ocornut/imgui" target="_blank">Dear ImGui</a> is designed to be "self-documenting". Once downloaded, the library comes with an extensive demo which explores and explains the range of features included in the library. The link between any aspect of the demo and the corresponding code is extremely easy to find and the demo code is written to be as spatially-continuous as possible, meaning it is almost always intuitive to identify the code snippet responsible for an element and then dissect how that code works. 
</p>

<p>
As such, learning and exploring <a href="https://github.com/ocornut/imgui" target="_blank">Dear ImGui</a> is a very hands-on, self-driven process. This, in my experience, leads to the development process with <a href="https://github.com/ocornut/imgui" target="_blank">Dear ImGui</a> being primarily defined by exploration, iteration, and curiosity in a way that many tools and libraries fail to be. Overall, the simple experience of getting to grips with <a href="https://github.com/ocornut/imgui" target="_blank">Dear ImGui</a> is more fun and engaging than many other interface development tools.
</p>     

<p>
While <a href="https://github.com/ocornut/imgui" target="_blank">Dear ImGui</a> already handles much of the boiler-plate work required to establish a rendering environment (it helpfully includes examples of establishing a functional application for a wide range of rendering backends), there is still a small amount of "ugly code" that goes into creating an application with <a href="https://github.com/ocornut/imgui" target="_blank">Dear ImGui</a>. 
</p>

<p>
To better isolate generic <a href="https://github.com/ocornut/imgui" target="_blank">Dear ImGui</a> code from project-specific code, I elected to migrate all backend and application preparation to an "App" class. In essense, App defined functions to contain any required preparation for <a href="https://github.com/ocornut/imgui" target="_blank">Dear ImGui</a> while leaving open virtual functions for project-specific code. As such, for any project that utilizes <a href="https://github.com/ocornut/imgui" target="_blank">Dear ImGui</a> I can now simply bring in this app framework and create a child class of App to contain the code for drawing the UI of that specific project.
</p>

<p>
Armed with <a href="https://github.com/ocornut/imgui" target="_blank">Dear ImGui</a>'s intuitive design patterns and a framework to make working with the library even easier, I fleshed out the interface for <span class="book-title">MCC</span> by determining its core features and use-stages and creating a simple, independently functional window for each stage of program usage. After creating windows for dataset refinement, dataset viewing, and dataset value calculation, I simply had to create a structure to encapsulate and preserve data that needed to be communicated between windows.
</p>

<span class="anchor" id="lessons"></span>
<div>
<p class="section-title">
Lessons Learned
</p>

<p>
During the course of developing <span class="book-title">MCC</span>, I learned much about data gathering and sanitization, 
</p>

<p>
While functional to my specifications, there are areas of <span class="book-title">MCC</span> that are still ripe for improvement.
</p>    

