---
layout: post
title:  My Favorite Sayings
---

> The greatest performance improvement of all is when a system goes from not-working to working. 
> &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;--John Ousterhout

Programmers tend to worry too much and too soon about performance. Many college-level Computer Science classes
focus on fancy algorithms to improve performance, but in real life performance rarely matters. Most real-world
programs run plenty fast enough on today's machines without any particular attention to performance.
**The real challenges are getting programs completed quickly, ensuring their quality, and managing the complexity
of large applications.** Thus the primary design criterion for software should be *simplicity*, not speed.
 
Occasionally there will be parts of a program where performance matters, but you probably won't be able to
predict where the performance issues will occur. If you try to optimize the performance of an application
during the initial construction you will add complexity that will impact the timely delivery and quality
of the application and probably won't help performance at all; in fact, it could actually reduce the performance
("faster" algorithms often have larger constant factors, meaning they are slower at small scale and only become
more efficient at large scale). **So, don't worry about performance until the application is running; if it isn't
fast enough, then go in and carefully measure to figure out where the performance bottlenecks are (they are likely
to be in places you wouldn't have guessed).** Tune only the places where you have measured that there is an issue. 

> A standard is definitely established by experiments. --Le Corbusier

Just as what Xiaoping Deng said aiming at emancipating Chinese people's mind forty years ago, "Practice is the sole
criterion for testing truth". When we come up with hypotheses, we had better solidify them into true codes. A
fact is a piece of information that can be observed or measured by practice; a truth or a standard or a concept
is a general rule that can be used to predict many facts or a solution to many problems.
Concepts are powerful and valuable, and acquiring them is the goal of most learning processes.
However, before you can appreciate or develop a concept you need to observe a huge
number of facts related to the concept by experiments. When we are trying to derive the underlying ground truth
for an unfarmilar area, initially our goal should be just to get experience (facts).
Once we have a collection of facts to work from, then we get chances to look for patterns; eventually these lead to
concepts. The learning processes of us human beings are exactly like how mordern artificial intelligence learn,
the same trail-and-error way, wherein before "eureka!" the trial processes may take long, but that is true research.
**Keep putting shoulders to the wheel!**

