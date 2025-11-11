---
layout: post
title:  "Boba Eye"
date:   2025-03-21 12:16:30 -0600
prev-page: /projects
prev-page-name: Projects
topic-list: Decoupling, ScriptableObjects, Event-driven Programming, Shaders
description: <span class="book-title">Boba Eye</span> is a cozy 2D game about creating drinks for a cast of cute critters. It utilizes tools such as ScriptableObjects and Event Channels to keep systems designer-friendly, extensible, and decoupled. It also uses some fun shaders to create unique-looking drinks!
preview_img: /assets/gifs/BobaEyePreviewWIP.gif
engine: Unity(C#)
role: Programmer & Designer
team-size: 2
itch-link: https://purpleml.itch.io/boba-eye-wip
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
Reflecting on my experiences with previous development projects, namely <span class="book-title">PUNCHERMAN!</span>, I began <span class="book-title">Boba Eye</span> with one main directive: constructing a game that I could return to and develop over time. After navigating the rather large amount of tech debt <span class="book-title">PUNCHERMAN!</span> accumulated during its first development cycle, I gained a renewed appreciation for the necessity of constructing systems that are durable, easily understood, and easily extended. Where we had spent months untangling messy, codependent systems to add new elements to <span class="book-title">PUNCHERMAN!</span>, I wished to be able to occasionally return to <span class="book-title">Boba Eye</span> and easily add in a new character or an additional component to the drink construction process.
</p>       

<p>
In order to achieve this, I would need a project capable of being easily understood again after some time away. Forming systems that function independently, thus reducing the number of elements requiring direct manipulation at any time, would ease the process of re-learning the game's workings. Additionally, designing systems to be data-driven would allow me to make defining new game content largely a matter of creating new data to feed into existing, flexible systems. As such, the paradigms I followed to help achieve my ultimate goal of a long-term supportable game were decoupling and being data-driven.
</p>       

<p>
With these core design principles in mind, I created documentation outlining the features and development roadmap of the game, noting which elements were absolutely essential and which would be nice to have someday. To construct systems adhering to my goals, I would need a strong understanding of what possibilities each system must be capable of handling and which systems would be in communication with each other. During <span class="book-title">PUNCHERMAN!</span>, I learned how great the challenge can be to adapt a system to accommodate previously unconsidered possibilities. Thus, this early mapping of game systems, their interactions, and possible future additions would help to construct stronger systems capable of handling continued development.
</p>

<span class="anchor" id="scriptableobjects"></span>
<div>
<p class="section-title">
Scriptable Objects
</p>  

<p>
ScriptableObjects are a potentially unassuming feature of Unity that proved vital at developing systems that were more modular and data-driven. 
</p>

<p>
ScriptableObject is, much like the more prevalent MonoBehaviour, a base class which scripts may inherit from in order to be easily utilized within the Unity editor. Similarly to a MonoBehaviour, ScriptableObjects are capable of containing state and functions that can be utilized by objects during a game's execution. 
</p>

<p>
However, ScriptableObjects differ from MonoBehaviours in several crucial aspects. They do not share the same lifecycle as a MonoBehaviour and are not created as components of GameObjects. Instead, ScriptableObjects are created as assets which may be referenced by more standard GameObjects. Due to existing as assets, they are outside the standard scene-based lifecycle of most objects and are usable without requiring any explicit instantiation. As such, ScriptableObjects are able to serve as easily-accessible bundles of data and functions that do not need to be located within a currently active scene
and are not tied to specific GameObject instances.
</p>

<p>
As an example of their potential usefulness, consider ScriptableObjects as they could be utilized as part of a game's weapon systems. 
</p>

<p>
If designed with ScriptableObjects in mind, the class <code>Weapon</code> may expose the variables <code>_firingSO</code> and <code>_projectileSO</code>, each being references to ScriptableObject assets. The functions in <code>Weapon</code> may call functions and use data from the ScriptableObjects, using those implementations to guide its own behavior. In this way, <code>FiringScriptable</code> assets could be created that allow a weapon to fire automatically or semi-automatically. Similarly, certain <code>ProjectileScriptable</code> implementations could allow some weapons to fire projectiles using raycasts while others use physics projectiles.
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
In a situation such as this example, <code>Weapon</code> could be used to define a wide range of different weapons by using different ScriptableObject assets to define aspects of the weapon's behavior. Furthermore, if, for example, all rocket-based weapons eventually need to switch to a different projectile, updating the <code>ProjectileScriptable</code> they reference will propagate those changes to all impacted <code>Weapon</code> instances. In this way, ScriptableObjects can improve the flow of development by creating systems that can easily combine reusable parts while allowing for those shared parts to be simultaneously updated across all usages.
</p>

<p>
Within <span class="book-title">Boba Eye</span>, this general technique is used for defining data that may need to be shared by different instances of objects across scenes. For example, all flavors are defined as ScriptableObjects that contain information such as the name of the flavor and its color. Thus, I can create assets outlining each possible flavor and pass those assets to any GameObject that requires flavor information (such as drink particles). Furthermore, I can easily define more flavors or alter the definition of existing flavors without having to manually update the related information across multiple locations.
</p>

<p>
ScriptableObjects are widely used across <span class="book-title">Boba Eye</span>. They also serve as the basis of systems such as customer definition, where a combination of ScriptableObjects defining the appearance, taste preferences, and speech patterns of a customer can be combined to easily create new cafe guests. 
</p>

<p>
In this way, ScriptableObjects were a key component in creating maintainable, extensible game systems as they allowed me to develop frameworks which could be easily filled to create new flavors, customers, and more. To tie this back to my initial thesis, ScriptableObjects are an easy-to-use and convenient tool in Unity that promote a more data-driven approach to system design. However, don't forget about ScriptableObjects just yet as they are also a key ingredient in a powerful decoupling technique!
</p>

<span class="anchor" id="channels"></span>
<div>
<p class="section-title">
Event Channels
</p>

<p>
Event-driven programming is a common and extremely useful paradigm when programming games and other user-driven pieces of software. Generally speaking, an event system allows for the creation of events that may be "fired" when certain conditions are met. These events often include data about the inciting incident, such as what object initiated it or when the event occured. Other objects then listen for events, each declaring what response it will make when it finally receives any events it is awaiting. This simple pattern allows for the creation of chains of functions to be called across objects without each object in the chain needing to know what consequences its own action will have.
</p>

<p>
As an example, consider a scoring system in a game where the player obtains points every time they click a coin. In a direct, naive approach, this could be handled by letting coins know about the UI that shows the score. When clicked, a coin uses its reference to the UI and calls a function that increases the score and updates the UI. While seemingly innocuous at first, this approach is ripe for the accumulation of tech debt due to its tightly-coupled nature. The coin needs to be directly aware of the UI and must tell the UI what to do. If eventually it is decided that collecting coins should also play a sound and cause another coin to spawn, suddenly a coin also requires direct knowledge of the systems for playing audio and spawning coins. In this instance, it is easy to see how designing systems to be tightly-coupled reduces flexibility and increases the likelihood of individual objects becoming bloated and unwieldy.
</p>

<p>
Designing the same system with an event-driven approach, each coin would instead fire an event when it is clicked. The UI, audio, and additional miscellaneous responses would all then be individually handled by the corresponding objects and systems, which would each listen for the event of a coin being collected. With this approach, adding any additional responses to a coin being collected does not require any direct modification to the coin itself. In this way, event-driven programming allows for the decoupling of systems and objects.
</p>

<p>
There is, however, a potential caveat that technically-inclined readers may have considered: how do the objects gain knowledge of the specific events they are listening for? There are a number of reasonable ways to provide event information to eager listeners, each with its own strengths and weaknesses. Objects of certain types may be dynamically found and listened to, references to event broadcasting objects may be manually provided, events may be static members of their classes, and so on. Ultimately, however, a listener does need some way to know what events it is listening for.
</p>

<p>
Additionally, events require careful consideration of the lifecycles of involved objects and their listening patterns. If used wantonly, events can prohibit garbage collection from functioning at full efficiency and can introduce difficult to dissect memory leaks. Events can, as a worst case, also lead to null exceptions if they are carelessly fired or listened to without ensuring they exist and have listeners.
</p>

<p>
Thankfully, ScriptableObjects can help to mitigate these potential weaknesses. ScriptableObjects are, just like any other object, capable of possessing and firing events. Furthermore, they are, as mentioned previously, exempt from the standard lifecycle and scene restrictions of standard Unity GameObjects. These factors allow them to be utilized as "channels" for events.
</p>

<p>
 An EventChannel is a ScriptableObject that contains an event that may be publicly listened to as well as a public function for firing that event. Due to its nature as an asset as opposed to a GameObject instance in a scene, it does not need to "exist" in a scene to be referenced and used by objects in any scene. Any object that wishes to send a message along a channel can be given a reference to the desired channel and call its public firing function when in need of sending a message. Similarly, objects that want to listen for events along a channel can be given the channel reference without it being tied to any specific set of scene objects.
</p>

<p>
Utilizing ScriptableObjects like this, it is possible to create an event-driven system where objects do not need to be concerned with who may be sending or listening to events or whether anyone is even utilizing a given event channel. This decreases the burden placed on listeners to acquire event information while also removing the actual event launching code from objects that wish to communicate, allowing for easier decoration or modification of event functions. 
</p>

<p>
As a bonus, EventChannels also serve as an easy way to group related events into a single channel without needing to explicitly declare lists of objects or events that are related. Returning to the previous coin example, all coins could communicate in an EventChannel for coin collecting without the need for a shared static class event or a list of all coins waiting to be collected. 
</p>

<p>
EventChannels also increase the safety of events by reducing the risk of firing or listening to non-existent events by connecting the events to objects that have a less volatile lifecycle. ScriptableObjects are always accessible during runtime, and as such will never be null if properly provided to an object. As such, a coin will always be able to fire its event and a coin responder will always be able to listen for its event, regardless of if any other active objects are around to broadcast/receive the same event.
</p>

<p>
Within <span class="book-title">Boba Eye</span>, EventChannels are used frequently to allow communication between objects from distinct systems that may wish to respond to one another. For example, the UI system for displaying characters and their dialogue lines is activated in response to an EventChannel that is activated when an occupied table is interacted with. The table has no knowledge of the UI; the UI has no knowledge of the table. They each only need to know of the EventChannel, which is a durable project asset capable of being easily provided in-editor. 
</p>

<p>
Using this technique, ScriptableObjects are able to combine with event-driven programming to allow for even more flexible, safe decoupling. This, combined with the data-driven design of systems utilizing ScriptableObjects in a more standard manner, allows for the creation of gameplay systems that are easily extended and responsive without becoming brittle or codependent.
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

