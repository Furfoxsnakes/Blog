---
title: "20 Games Challenge - Project 2: Breakout"
date: 2023-11-07
layout: post
---

# Project 2: Breakout
### Completed: 11-08-2023
### Scope: Small
### Difficulty: Easy
### File size(zipped): 57.6 MB
### Repository: https://github.com/Furfoxsnakes/20_Games_Challenge_2_Breakout
### Download: https://furfoxsnakes.itch.io/20-games-challenge-2-breakout

# What went well

### Art

For this project, I again used Aesprite. I was able to reuse the <em>Ball</em> asset from the last Pong project. For the paddle and bricks, I simply turned the paddle from Pong vertically and updated the shading.
I couldn't find a way to 9-slice a <em>Sprite2D</em> so I just cut down the size of the paddle into a smaller sprite and used that for the bricks as well. I left the sprites in greyscale and used the modulation within Godot to change the brick colours.

Because breakout is a colourful game, I utilized a 32 colour palette: <a href="https://lospec.com/palette-list/endesga-32">Endesga_32 from LOSPEC</a>

Breakout has lives, which the player loses one of when the ball enters the <em>Pit</em>. For the lives, I made some hearts, and spiced them up with a bit of shading as well.

This project required very little unique assets thanks to the modulation on sprites in Godot

### Code/Mechanics

The mechanics of the game were again very straight forward. Everything was contained and laid out on a single screen. This allowed for easy linking of nodes (via [Export]) to the <em>Game</em> class. Speaking of the <em>Game</em> class, I focused on moving as much logic as I could into it instead of having the game objects handle their logic. This allowed me to utilize a very simple Enum state machine to handle game state.

I attempted to utilize Godot's built-in physics again, but found I couldn't figure out how to the ball stop pushing the paddle. After some trial-and-error, I settled on using a <em>CharacterBody2D</em> for the ball, which would allow me to use the <em>IsOnFloor(), IsOnCeiling()</em> and <em>IsOnWall()</em> functions that a provided with a <em>CharacterBody2D</em>. This allowed me to easily code the ball's trajectory when it hit a surface. Going forward, I think this process will be very handy for ball physics.

### Music/Audio

I wanted to add some music and sound effects to this project. This is not an area of game dev that overly interests me, so I decided not to waste time on making my own for this project. Instead I utilized music and sounds from [Asset Jesus](https://kenney.itch.io/kenney-game-assets). There were plenty of options for music and effects and implementing them in Godot was super simple and took maybe a half hour to do in total.

### Scope

Managed to keep the scope to a minimum on this project, and because of that I was able to complete it in a single day.

### Difficulty

I found this project pretty easy coming right off of the Pong project, as both had very similar mechanics. 

# What didn't go well

### UI

The UI was one of the last things for me to do in this project, and while it wasn't detrimental to implement last minute, it did remind me that I should be more aware of the game's UI before I get too far.

### Code/Mechanics

For the player paddle, to try and add difficulty layers, I made the paddle move with <em>MoveAndCollide()</em> so that the paddle didn't immediately snap to the player's mouse and lerped towards it instead. It felt OK, but produced some visual errors when the mouse position came close to the position of the paddle. With some tweaking, I'm sure I could get rid of this, but left it as it wasn't overly game breaking. As a plus, I could make the paddle move slower, or faster, to adjust the difficulty of the game. 

# Things I've learned from this project

I didn't know that _MoveAndSlide()_ also provided collision information. I also found out that you can get the angle of a moving node by using the [_GetTravel()_](https://docs.godotengine.org/en/stable/classes/class_kinematiccollision2d.html#class-kinematiccollision2d-method-get-travel) function provided by _KinematicCollision2D_. This provided the angle of the ball just before collision which I could then manipulate to update the new trajectory based on what surface it just hit (ie: floor, wall, ceiling). 