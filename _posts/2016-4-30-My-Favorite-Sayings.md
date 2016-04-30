---
layout: post
title:  My Favorite Sayings
---

> The greatest performance improvement of all is when a system goes from not-working to working. 
>   `    `  --John Ousterhout

 Programmers tend to worry too much and too soon about performance. Many college-level Computer Science classes focus on fancy algorithms to improve performance, but in real life performance rarely matters. Most real-world programs run plenty fast enough on today's machines without any particular attention to performance. **The real challenges are getting programs completed quickly, ensuring their quality, and managing the complexity of large applications.** Thus the primary design criterion for software should be *simplicity*, not speed.
 
 Occasionally there will be parts of a program where performance matters, but you probably won't be able to predict where the performance issues will occur. If you try to optimize the performance of an application during the initial construction you will add complexity that will impact the timely delivery and quality of the application and probably won't help performance at all; in fact, it could actually reduce the performance ("faster" algorithms often have larger constant factors, meaning they are slower at small scale and only become more efficient at large scale). **So, don't worry about performance until the application is running; if it isn't fast enough, then go in and carefully measure to figure out where the performance bottlenecks are (they are likely to be in places you wouldn't have guessed).** Tune only the places where you have measured that there is an issue. 
