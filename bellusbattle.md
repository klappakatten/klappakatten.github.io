---
layout: default
title: Martin Nyman
---

<link rel="stylesheet" href="/assets/css/custom.css">

# Bellus Battle

<iframe width="560" height="315" src="https://www.youtube.com/embed/PkmYMmFsUH0?si=mo3-0HpOYeLrlG4v" title="YouTube video player" frameborder="0" allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture; web-share" referrerpolicy="strict-origin-when-cross-origin" allowfullscreen></iframe>

Bellus Battle is a fast-paced, couch-style free-for-all game set in an arena style environment. Players can choose from a wide variety of fun and chaotic weapons to defeat their opponents.
The game features a round-based scoring system: the last player standing wins the round, then the battle continues on a new map. This cycle repeats until one player accumulates enough points to claim victory and win the game!
Feel free to try the game, you can download it for free from our Steam page.

# Weapons

I modeled most of the weapon models currently in the game such as the: railgun, revolver, grenade launcher, portal-gun, m-16, flintlock, bomb, x-bomb & shotgun. All the models where created in a stylized low poly style with sharp black outlines.
The silhouette was the most important for these models since the models are rarely ever seen up close. Also the textures had to fit together with the projects toon shader.

# Environment

I also created created many environment assets in all the different levels and themes. The focus was never on creating high detailed assets here since details are easily lost because of camera distance and shader style.

# Animations

I was also responsible for setting up behaviors and implementing all the animations & cloth physics currently in the game. I did use animation blending based on speed, used avatar masks to split up the different parts of the rig to use different animations when needed.
 I implemented some real time rig behaviors using the unity animation rigging package for the head and arms of the character. For the head we have a simple look at constraint which always points towards the camera, since the perspective is from the side we don't want the character to face away from the camera once they change direction.

he characters' arms are controlled using the gamepad sticks, they always point in the direction the stick is aimed. To achieve this, I had to ensure each arm continuously tracks a target that orbits around the character based on the stick's movement (or follows the mouse on PC). This part of development really taught me how tricky handling rotations can be.

# Cover Art

