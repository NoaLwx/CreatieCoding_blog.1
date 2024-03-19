---
title: Creative Coding blog week 1 :33
published_at: 2024-03-06
snippet: I cant code...
disable_html_sanitization: true
---

Hello, world!

# **Week 1 of coding rabbit hole** 
## putting things inside the blog post (crying)


<iframe src="https://editor.p5js.org/NoaLwx/full/IaH4veEs5" width="100%" height="242px"></iframe>

## Making the grid
![:3](/week1/index.png)

I stopped all the size changing function so I can work better and set the height differently so it make a grid. I tried increasing the number of height/x until they match. (I don't know how to grid, this is the best I can do)

![half the grid](/week1/halfgrid.png)

Instead of dividing the height, I put increasing variable for the height, manually. 

![an actual grid](/week1/grid.png)

I also made another p5 sketch that changing the size like the initial sketch.

![changing size!!](/week1/size.png)

<iframe src="https://editor.p5js.org/NoaLwx/full/Njbz891S5" width=500 height= 300></iframe>

<iframe src="https://editor.p5js.org/NoaLwx/full/Vcr-J_mLX" width=500 height=300></iframe>

## Remaking goodbye farewell by Rafaël Rozendaal
 By observing the website, I identified 2 element in this web art: `the moon` and `the moving light reflection on the water surface`.

The moon is easy to code since it's just a circle in the middle of the width and around 3/4 up the height.

However, the animation for the water is way over my league,  so I decided to try different approach.


### I don't know know to make it liquify so i used random generated lines
#### Line codes

![Code I got from Happy Coding](/week1/random.png)

Since the original code doesn't match with what the art looks like, I changed the variable in the code to make it looks more like water: changed the weight of the line, made the framerate faster, changd the maximum length of the line... 

When i halved the size of the lines, it was on the wrong side.

![wrong half](/week1/wronghalf.png)

I then moved the lines down half the height of the canvas with translation code.

![half](/week1/half.png)

I also tried to make the line bounch but it didn't work.

![Animation code](/week1/bounce.png)

#### The moon
I put the circle in as the moon but it didn't show up. At first, I thought it was due to the wrong position (I put height*4 instead of height/4) but it still didn't show up.

`It was the background on top of the moon`

After removing the extra background, the result is kind of resemble the original art

![Final](/week1/final.png)

### **_Result_**
<iframe src="https://editor.p5js.org/NoaLwx/full/m_5UNaLnt" width="100%" height="600"></iframe>


***


