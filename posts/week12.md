---
title: WEEK 12
published_at: 2024-06-22
snippet: uh
disable_html_sanitization: true
---

# Process of an image collage website

## Planning

For my planning, I wanted to create a website where I can put images in and rearrange them to create a collage.

At first, I thought about a fixed postion for each of the image, like the duet function of tiktok. So I carefully arrange each canvas with the grid function.

[multicanvas](/w12/multicanvas.png)

But this idea is not possible because I also want to download the canvas as an image but this is multiple canvas (9 in total). Therefore I scrapted that idea and create a better solution.

I made a single canvas with the function to import multiple images using arrays and then adding the function of dragging them around the canvas.

[canvas](/w12/canvas.png)

This was a bit different from my initial idea but it works well too.

## Coding

Coding was the hardest part in this whole project.

At first, doing the input function and the dragging function is easy because I watched some tutorials online.

However, when it get to the sockets, everything was a pain.

[bug](/w12/bug.png)

Because I want the images data to store in a server and then put back onto the canvas, I have to use deno kv. Importing it in was fine, but the images data is too big, so I had to resize all of them, which pixelated the images a lot.

[getting data](/w12/gettingdata.png)

I actually wanted to replicate those online drawing website where they have the position data sent across the server. However, I was too tired to do that but this actually create a fun idea where people can create different outcomes. Well, if it works, it works.

[socket](/w12/socket.png)

This process took me 2 weeks and I still amazed that it does work out. I was so close to give up multiple times but I am glad I didn't.

However, due to the shortage of time, I couldn't make the server connecting together, so only the people who live in the same region/country can access each other input images.

## Finish

[website link](https://s4004087-a3.deno.dev)

It actually work very well and I got my highschool friends to test it out for me and we had a session where we arranged the images we put in.

[finish](/w12/finish.png)

# Evaluation

## Community of Practice

The community i had for this project was my highschool friends who I played with back then and still hangout sometimes too.

Our domain is the discord server that we are all in, with the same shared favourite games, movies, activity.

However, they don't do coding or anything relating to computer, so I was the broker who bring this experience to them. Maybe for them, it was just some website, but for me, it's something I created from the ground up.

It was really fun connecting with them again and creating something together, since we were so busy with university.

## Mycelial Creativity

In some way, this is like foraging things and decoration together. It's something about group activity that is really human to me, how we do things together, even thought this was through the scene but we are having fun creating things together.

Also I might be reaching but the images really pop up like mushroom, and them when we drag them around, it create connection, a colony.

# Ending

It was really fun, i think. I was too tired toward the end, and the video editing was not my best at all. I apologise for that.

But thank you Tom for helping me with the website. I really appreciate it even though I didn't express it well enough.

The whole class was really fun. It was painful, yes, I suffered so much, but it was fun. Painfully fun.

(It's something on my mind but are you in the spectrum. I'm just curious no offense. Please dont grade this part.)
