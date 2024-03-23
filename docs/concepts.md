---
layout: default
title: Concepts I find cool
---

<style>
h2 {
    // make underline go across entire page
    border-bottom: 1px solid #eaecef;
}
</style>


# Concepts I find cool

These are things I learnt during classes, projects, or workshop, and I find them cool, fascinating, or useful. I hope you do too.

{: .note-title }
> **A note on CS/programming concepts**
> 
> I maintain a separate website for CS/programming concepts.. Even though it was designed for the CAIE Computer Science syllabus, it is useful for anyone learning CS/programming. You can find it at [https://eccentricOrange.github.io/CAIE-Computer-Science/](https://eccentricOrange.github.io/CAIE-Computer-Science/). I won't cover as many CS/programming concepts here.

## 1.   Differential pairs
Think about a signal traveling in a wire. Specifically, think of a digital signal, which is just a voltage that is either high or low (1 or 0, 5V or 0V etc). This is called a **single-ended signal**, because it is referenced to a single point, usually ground.

Now, let's do a weird thing. Let's take another wire, and copy the above signal onto it, but with the opposite polarity. So if the first wire is at 5V, the second wire is at 0V, and vice versa. This is called a **differential signal**, because it is referenced to two points, and the voltage between them is what matters.

![Differential vs single-ended signals](https://www.allaboutcircuits.com/uploads/articles/DS_TimingDiagramm_2.jpg)
(image from [allaboutcircuits](www.allaboutcircuits.com))

At this point, let's assume that there is some noise in our signal.

The single-ended signal is referenced to ground, so the noise is added to the signal. This is bad, because it means that the noise is now part of the signal, and we can't tell them apart.

![noise in single-ended](https://media.licdn.com/dms/image/C4E12AQFJgPhpGzC91g/article-cover_image-shrink_600_2000/0/1526946849737?e=2147483647&v=beta&t=m-Kj3UTfoB_Fc_mqzzcSev1fI5ckFW14M8NQbkwc4Ek)
(image from [LinkedIn](https://www.linkedin.com/pulse/what-differential-signaling-why-use-it-alexander-witkowski/))

The differential signal is referenced to itself, so the noise is added to the signal, but also to its "opposite". Guess what? We can simply subtract the two signals, and the noise will cancel out, leaving us with the original signal!


<img src="https://i.stack.imgur.com/Fc6Nt.png" style="background-color: white;" alt="noise in differential"/>

(image from [StackExchange](https://electronics.stackexchange.com/questions/231297/noise-can-be-differential-or-common))


This is why differential signals are used in many applications, such as USB, Ethernet, and HDMI. They are also used in high-speed digital circuits, such as FPGAs and microprocessors.

### Read more:
*   [_What Are Differential Pairs and Differential Signals?_, article by Altium](https://resources.altium.com/p/what-are-differential-pairs-and-differential-signals)
*   [_The Why and How of Differential Signaling_, article by All About Circuits](https://www.allaboutcircuits.com/technical-articles/the-why-and-how-of-differential-signaling/)
*   [Definition of differential signaling, Analog Devices](https://www.analog.com/en/design-center/glossary/differential-signal.html)
*   [_How does a USB keyboard work?_, YouTube video by Ben Eater](https://www.youtube.com/watch?v=wdgULBpRoXk)
*   [_Analyzing actual Ethernet encoding \| Networking tutorial (4 of 13)_, YouTube video by Ben Eater](https://www.youtube.com/watch?v=i8CmibhvZ0c)