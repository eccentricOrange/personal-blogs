---
layout: default
title: Embedded Systems and Robotics
---

# Embedded Systems and Robotics
{: .no_toc }

## Table of Contents
{: .no_toc }

1. TOC
{:toc}

## How to learn embedded systems?

I typically say that I am a robotics and embedded systems developer, so a whole lot of people ask me how to get into embedded systems. Honestly, my path into it wasn't a textbook approach but I'll lay it out anyway, and try to figure out some structured resources for any readers too.


### Suggested way to start

1.  **Learn the basics of electronics:** If you're an electrical/electronics engineer/student, you can probably skip this. Otherwise, it's a good idea to learn some of the core concepts of electrical engineering. If you have the time, a textbook like the _Art of Electronics_ is a good place to start; otherwise, consider the following concepts as a bare minimum (and yes, it is worth it to rigorously practice problems on these, not just to watch videos or read material):

    -   Ohm's law, voltage divider rule, P=IV, P=I2R, P=V2/R, capacitance formula (parallel plates), inductance formula (loops)
    -   RC filters, at least first order. RL filters, first order
    -   pull-up and pull-down resistors, weak/strong pull-up/down
    -   digital logic gates, truth tables, some basic logic circuits

2.  **Learn C:** I cannot stress this one enough - getting a handle on C before diving into embedded systems itself gives you a massive boost in understanding. The _CS50_ course by Harvard is my favourite source, but you may initially learn from basically anywhere.

3.  **Dive into a specific embedded system platform:**

    -   **Hobbyists:** Start with Arduino, ESP32, or Raspberry Pi. Pick Arduino if are a complete beginner; pick ESP32 if you have some experience or intuition; pick Raspberry Pi if you want more focus on the software side of things.
    -   **Engineering students:** Start with STM32, unless you have some aversion to ARM. In that case, NXP,  Microchip, or Atmel (now part of Microchip) are good alternatives.
    -   **Professional developers:** STM32 and ESP32 are good common choices.


### How I did it
I was part of a weekly robotics course in middle school. In sixth grade, I was just handed an Arduino board, told "This is a way to add intelligence to your robots," and given some guidance on getting started with Arduino. At the time I didn't know what microcontrollers, didn't know that Arduino code is built on top of C++, and certainly didn't set out to learn embedded systems. But it was interesting.

{ .note-title }
> If you can, find someone who can teach you **in-person.** Unlike programming on a normal computer, embedded systems has a lot more nuances and pitfalls, and having someone to guide you through the process is invaluable. Once you can digest tutorials, then learning by yourself gives you a lot of freedom to explore.

This is my "unconventional" path: it is not unconventional in the sense that it's not common (many people get their start on Arduino in much the same way), but it is unconventional in the sense that you typically wouldn't be advised to do it this way. In any case, after learning the basics of Arduino, the path was straightforward: find something interesting to work on, and throw whatever new stuff you learn into it. Then take a step back and re-build the same project with only relevant stuff (not necessarily everything you learned) to solidify your engineering skills.

### Comparison of the approaches

| Factor | Conventional Approach | My Approach |
| --- | --- | --- |
| Difficulty | Low | High |
| Learning curve | Steep | Gentle |
| Time to first work project | Long | Short |
| Academic focus | High | Low |
| Practical focus | Low | High |
| Community support | High | High |
| Are you guaranteed to learn the important stuff? | Yes | No |
| Breadth vs depth | Depth | Breadth |

## Random advice

### Build and then rebuild the same thing once
One piece of advice missing from most sources is learning to analyse stuff and make proper architectural decisions. When you first build something, the goal is to just get it to work. You will learn a lot of new stuff, and you will have a lot of fun. But once you have a working prototype, take a step back and think about how you can improve it. What parts are not necessary? What parts are not modular? What parts are not reusable? What parts are not well documented? What parts are not well tested? Then rebuild the same thing with the new knowledge you have gained.

If you sit back with a piece of paper and a pen/pencil, you **design with actual intent.** This is a very important but somewhat rare skill.

### Find case studies
I don't know any good resources for this, but do the absolute best you can to find analyses of projects, reviews, and seek feedback. **You need to know where you went really wrong**, and you will often not be able to figure this out by yourself. If you can, find a mentor who can help you with this. If you can't, try to find a community of people who are willing to give you feedback on your work - stuff like Arduino forums, Raspberry Pi forums, or Reddit are excellent.

Even watching reviews of other projects helps a lot. For (somewhat advanced) PCB design work, Phil's Lab on YouTube does excellent reviews. Channels like Low Level Learning have excellent material on deep dives.

For software projects (or software components of embedded projects), the Code Review Stack Exchange is an excellent and underrated resource. Make frequent use of it, but keep in mind that they are a little strict about how your post is formatted and so on...

### There is no escape from the hardware
Sorry, no matter how much you hate it, you will be a vastly better embedded systems developer if you understand a little bit about electricity and the tools available to you to manipulate it.

You don't have to learn much - if you look at the introductory course of any electrical/electronics engineering program, most of them will have a 101 class. In my case, it was called "Basic Electrical and Electronics Engineering." This is sufficient for most people.

### Learn networking, you will need it but you won't know when
Sooner or later, you will need to connect your embedded system to the internet or some other network. This is a very important skill to have, and it is not as hard as it seems. You can start with the basics of TCP/IP, HTTP, and MQTT protocols. Then move on to more advanced topics like WebSockets, REST APIs, and so on.

A good place to start is to get a Raspberry Pi and a laptop; two laptops; an ESP32 and a laptop; or any such combination. Mess around with them.

### Make an effort to learn complex stuff
Look, I will never undervalue basics. Without that, your projects will always be a house of cards. If you do not know basics of your field, please focus there.

Buttttttt, it is nice to have further aspirations - they drive you to learn and build more interesting stuff. Attend workshops and watch videos on stuff that is ever so slightly out of your reach. This is one of the fastest ways to grow.