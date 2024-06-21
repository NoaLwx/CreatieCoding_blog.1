---
title: WEEK 10
published_at: 2024-05-15
snippet: uh
disable_html_sanitization: true
---

# Live Coding (with Charlene)

## Idea

Charlene and I first thought of making something a bit unhinged, something attract you in a bad way that made you nausseous. Therefore, we took the inspiration from those hypnosis video with repeating circle and adding bright colours in to make it more chaotic in a way.

## Process

We divided the work into two, I did the visual and Charlene did the music.

I started off with the looking at hynosis videos and gather some elements from them and they all have the same thing: Looping, smoothly moving geometrical images. So I created a few ideas to go with it.

### Noise

Using noise with colorama created a cool moving effect. It's unpredictable and interesting to look at.
I blended this with osc to further making the colour more complex and attractive.

```
noise(10).color(10, 2).colorama().blend(osc(10, 0.1, 1.2)).out()
```

![noise](/w10/noise.png)

### Noise with shapes

I then made a similar idea but now using shape with different filter. I reduced the ammount of noise in this one so that it wouldn't be too contradicting with the shape in the middle.

```
noise(1).color(10, 20).colorama().diff(shape(360, 0.8)).out()
```

![different](/w10/diffnoise.png)

### Kaleid

Those ideas above were good but it doesn't feel like a hypnosis video so I changed my way of doing it and use kaleid with colorama instead. With kaleid, I was able to make the looping cicle effect, although I made the shape not too circle to that it looks more interesting.
I then add the shape in but instead of making it fully circle, I only put 10 sides to the shape so that I can make it rotate more noticably.

```
noise(1).color(10, 20).colorama().kaleid(260).diff(shape(10, 0.8).rotate(20,0.6)).out()
```

![kaleid](/w10/kaleid.png)

## Final result

After considering with Charlene, we decided to go with the kaleid option.
As I mentioned before, we were going for a hypnosis video style ~~to brainwash you into giving us high score~~ . However, as the codes progressed, the piece become more and more like a torture, both visually and auditory. My head hurt so bad after staring at it for too long...

### [Result](https://flok.cc/s/distinguished-crimson-smelt-c1549367)

https://youtu.be/dV31DC44BSw

# Live-coding community

This experience with Charlene was really fun. I think what the live-coding community are trying to do is to see how the progress of their codes go from the blank canvas to a pleasing visual or a full music piece. It was great seeing the changes and the decision we made before reaching the end result.

Collabing with other people also created a sense of community on sharing ideas and perspective, working together to create art by using coding.
