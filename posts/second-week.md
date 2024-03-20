---
title: Creative Coding blog week 2 orz
published_at: 2024-03-13
snippet: What even is CLASSSSSAAAAAAAAAAAHHHH
disable_html_sanitization: true
---
Crying.mp4

# Week 2 of staring at the screen for half a day without unnderstanding what happen

## Remaking Flying Frying by Rafaël Rozendaal
 
 The main elements of this piece are: ``eggwhite``, ``eggyolk`` and ``highlight``.
 Eggwhite is the hardest part with constantly moving point. In addition, the egg yolk is also wobbling around.

 ### Process
 At first, I tried looking up a tutorial for a liquified blob. 

 ![trial](/w2/trial.png) https://medium.com/@alptugan/trigonometric-blobs-f8a41fb7fba0

 However, for some reason, despite following the tutorial closely, the class function doesn't work for me, so I find another tutorial. 



 https://www.youtube.com/watch?v=rX5p-QRP6R4&t=141s

 ![the only tutorial i trust](/w2/eggwhite.png) 

 With this, i was able to get the foundation of the moving egg white part. Then I added the egg yolk in and change the rectMode to center so that all the objects are in the center of the screen. 

 Using the let function for ellipseX, ellipseY, xSpeed and ySpeed, i was able to make the yolk move around. I put the speed as 1 at first but it was too fast for the small area so i decreased it down to 0.1. 

 ![moving](/w2/movingyolk.png)

 During this part, I also added the shadow for the egg using drawingContext.shadowBlur and shadowColor following this tutorial 

 ![tutorial for shadow](/w2/shadowtut.png)
  -> ![shadow](/w2/shadow.png)

However, the shadow also appeared on the yolk, so I just recoloured the shadow so it wouldn'd show on the yolk

  ![egg yolk](/w2/yolk.png)

For the last part, I used arc to draw the highlight of the yolk.I couldn't figure out the radiants for the arc and they keep messing up, but it looks decent so i guess it worked. I didn't do any animation here because it would destroy the whole thing. It still looks good, so...

![highligh!!!!](/w2/highlight.png)

<iframe src="https://editor.p5js.org/NoaLwx/full/hIllDNXOV" width=400 height=443></iframe>


## Putting things into class

I cant, i just cant, gave up.