---
title: Creative Coding blog week 3 orz
published_at: 2024-03-26
snippet: ueuueueueue (sound of me crying)
disable_html_sanitization: true
---

# **WEEK 3 (I am balling)**

## Cute in effective complexity

### What is cute? How did Ngai define cute?

![kaomoji](/w3/kaomoji.jpeg)

`Cute` is intimate, fuzzy and warm, it can be handle and fold and shape the way we want, it incites us to take care of it.

And this make me wondering if cute can be the fuzzy feeling of looking at a cat and want to pet with it. 


![cute chibi chikawa and friend](/w3/chikawa.png)

Cute can also be dangerous. Our brain thinks of cute and would try to touch things that aren't meant to touch. For example, the internet phenomenal with associating dangerous animal as cute, saying that, "if it's not friend, why friendshape?" (why they look fluffy and cute).

![bears are pettable](/w3/friend-shape.png)

### Effective Complexity

Effective complexity is something that is coherence, having a set action/form but is not completely static/staying the same form. It might appear random, but all of it actions/forms are similiar to one another in a way, like leaves or probability of a set of number. Or like the picture down here, cables with differen colours (non-redundant) but are actually the same shape/form (coherence).

![wires/cables](/w3/effcom.png)


## So how cute can be intergrating into effective complexity

I was inspired by Rafeal's 'fill this up' website.

With the pastel colours shapes that might seems random but still very coherence, and the way that you can control where the shapes will go and is able erase the shapes, the website fits the description of being cute. 

Therefore, I used the same ideas of the work and add some of my personal elements into it. The theme is cats!! 

To start it, I put the basic code for the shapes to follow the mouse using mouseX and mouseY coordinates; and the randomised colours. At this stage, it was very simple, however, when I put them in class, things starts to get different.
![follow the mouse](/w3/first.png)

The colours put in using 
```javascript
colour (random ()*360, 25,100)
```
makes the colours flashing instead of the shapes staying the same colour, so I changed it to

```javascript
 getRandomColor() {
    return color(random(255), 25, 100);
```
With this, the colour stay the same for each shape, just like how Rafeal did. 

![based codes](/w3/basic.png)
^ *using basic shape at this moment to see if the coding is working correctly*

I then put define the class and put 
```javascript
   let shapeType = int(random(3)); 
```
and making the shapes below using if - else if so that p5.js can randomly draw the already existed shapes with random colours.

![shapes](/w3/shapes.png)

There are 3 types of shape in my code: cat head, cat paw and fish. This goes along with the theme.

**Trials**

I was trying to make a yarn shape but the bevel doesn't look that good so I scrapped it and went with the solid shapes.

![yarn](/w3/yarn.png)
![strokes](/w3/stroke.png)

#### the result
After making the codes for each shape through trials and errors, I filled the whole page to see if it's working
![fill the whole thing!!!](w3/fill-in.png)
then added a border (I don't know why, I think it looks better with a border)
![border](/w3/border.png)


<iframe src="https://editor.p5js.org/NoaLwx/full/2OjcK8hpd" width=800 height=848 ></iframe>

