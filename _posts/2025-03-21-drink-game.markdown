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
ScriptableObjects are a potentially unassuming feature of Unity. ScriptableObject is, much like the more prevalent MonoBehaviour, a base class which scripts may inherit from in order to be easily utilized within the Unity editor. Similarly to a MonoBehaviour, ScriptableObjects are capable of containing state and functions that can be utilized by objects during a game's execution. However, ScriptableObjects differ from MonoBehavior in several crucial aspects. They do not share the same lifecycle as a MonoBehaviour and are not created as components of GameObjects. Instead, ScriptableObjects are created as assets which may be referenced by more standard GameObjects. Due to existing as assets, they are outside the standard scene-based lifecycle of most objects. As such, ScriptableObjects are able to serve as easily-accessible bundles of data and functions that do not need to be located within a currently active scene
and are not tied to specific GameObject instances.
</p>

<p>
As an example of their potential usefulness, consider ScriptableObjects as they could be utilized as part of a game's weapon systems. If designed with ScriptableObjects in mind, the class <code>Weapon</code> may expose the variables <code>FiringSO</code> and <code>ProjectileSO</code>, each being ScriptableObjects. The functions in <code>Weapon</code> may call functions and use data from the ScriptableObjects, using those implementations to guide its own behavior. In this way, <code>FiringScriptable</code> assets could be created that allow a weapon to fire automatically or semi-automatically. Similarly, certain <code>ProjectileScriptable</code> implementations could allow some weapons to fire projectiles using raycasts while others use physics projectiles.
</p>

<p>
<pre>
<code>
public class Weapon : MonoBehaviour
{
    [SerializeField] private FiringScriptable _firingSO;
    [SerializeField] private ProjectileScriptable _projectileSO;

    public bool TryToFireWeapon()
    {
        if(_firingSO.CanFire(WeaponState))
        {
            FireWeapon();
        }
    }

    private void FireWeapon()
    {
        _projectileSO.LaunchProjectile(WeaponState);
    }
}
</code>
</pre>

<pre>
<code>
public class FiringScriptable : ScriptableObject
{
    public bool CanFire(WeaponState)
    {
        // code checking if the parameters should allow this weapon to fire
    }
}
</code>
</pre>

<pre>
<code>
public class ProjectileScriptable : ScriptableObject
{
    public void LaunchProjectile(WeaponState)
    {
        // code creating a projectile using parameters
    }
}
</code>
</pre>
</p>

<p>
In a situation such as this example, similar weapons could share implementation details by utilizing shared ScriptableObjects while entirely new kinds of weapons could be created by defining a new ScriptableObject that fires in a novel way. Furthermore, if, for example, all rocket-based weapons eventually switch to a different projectile then updating the <code>ProjectileScriptable</code> they reference will propagate those changes to all impacted <code>Weapon</code> instances. In this way, ScriptableObjects can improve the flow of development by creating systems that can easily combine reusable parts while allowing for those shared parts to be easily updated across all usages.
</p>

<p>
Within <span class="book-title">Boba Eye</span>, this general technique is used for defining data that may need to be shared by different instances of objects across scenes. For example, all flavors are defined as ScriptableObjects that contain information such as the name of the flavor and its color. Thus, I can create assets outlining each possible flavor and pass those assets to any GameObject that requires flavor information (such as drink particles). Furthermore, I can easily define more flavors or alter the definition of existing flavors without having to manually update the related information across multiple locations.
</p>

<p>
ScriptableObjects are widely used across <span class="book-title">Boba Eye</span>, also being the basis of the system for defining new customers as a combination of ScriptableObjects defining the appearance, taste preferences, and speech patterns of a customer. In this way, ScriptableObjects were a key component in creating a maintainable, extensible game system as they allowed me to develop frameworks which could be easily filled to create new flavors, customers, and more. However, while these instances do display and benefit from the unique traits of ScriptableObjects, there is an even more powerful way they may be used.
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

