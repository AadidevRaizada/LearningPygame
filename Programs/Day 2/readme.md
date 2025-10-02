# 🎮 PyGame Learning Journey - Day 2

## 📚 Learning Resources
I used this tutorial for day 2:
[PyGame Tutorial Series](https://www.youtube.com/watch?v=W_JRd3ntyBg&list=PLjcN1EyupaQnHM1I9SmiXfbT6aG4ezUvu&index=2)

## 🎯 Overview
DAY 2 was a wild ride, here are the main changes in the code so far:

## 🔄 Recap of Day 1
Building the BASICS of our world and setting up the most important stuff such as:

- 🔁 Run function to keep our world running. [`Run loop`]
- 🖼️ Image loading. [`pygame.image.load`]
- 📏 Creating a grid (to scale our world). [`def_grid()`]
- 🌍 World data (to create our world). [`world= [["World data here"]]`]
- 🎨 Filling the tiles in world data using images of ours. [`class world: row_count, col_count, defined a loop`]

In the end we had a 5 x 5 world with some grids, to which we added images, and different tiles.

## 🚀 Major Changes in Day 2

### 👾 Adding a Player
**Q) How do we add a player to the game?**  
A) Well day 2 talks about exactly that, we first:
Created a class for player, exactly how we created one for world.
```python
class Player():
    def __init__(self, x, y):
        img = pygame.image.load('img/guy1.png')
```
Then, we needed to draw the player onto the screen, which is similar to how we drew the background image [sky.png] and the grass and dirt tiles.
So we created a function def update()
and added this to it:
```python
#draw player onto screen
		screen.blit(self.image, self.rect)
```
We then define the scale (how big the player will be):
player = Player(100, screen_height - 130)

We finally added the player onto the screen pretty easily by just calling the function 
player.update()

### 🏃 Player Movement
**Q) Now we have the player on the screen.. how do we make him move?**  
A) Simply, we used the created player class and defined the x and y axis of the player
by transforming the character into a rect with following characteristics:
```python
self.rect = self.image.get_rect()
self.rect.x = x
self.rect.y = y
```
Now, we want to use the x and y axis to make our player move.
We do that in our def update(self) function,
```python
    def update(self):
        dx = 0
		dy = 0
		#get keypresses
		key = pygame.key.get_pressed()
		if key[pygame.K_LEFT]:
			dx -= 2.5
		if key[pygame.K_RIGHT]:
			dx += 2.5
```
Then we update the player's coordinates using:
```python
self.rect.x += dx
self.rect.y += dy    
```
What we need is simple, the change in x axis of the player, the change in y axis of the player, this will define how much the player will move left and right based on the key pressed (We create a variable to get the key pressed by the user and then We use pygame's inbuilt function [pygame.K_LEFT], [pygame.K_RIGHT] in order to use the input in our program)

### 🦘 Implementing Jump Mechanics
**Q) Okay okay the player is now moving left and right from your code.. but how will he be able to jump?**  
A) Now in order to make the player jump, we need to define:
- The velocity of the player's jump
- The strength of the jump
- The gravity in the game

This will help us create a sort of ... working jump. (Once you run the code yourself you will know why I have not said that this is a completely working jump)

First we define the variables for velocity and checking wether the player has jumped or not.
self.vel_y = 0
self.jumped = False

Then, we check if space key pressed and define our jump based on that
```python
if key[pygame.K_SPACE] and self.jumped == False:
			self.jumped = True
			self.vel_y = -7.5
```

We then add:
```python
if key[pygame.K_SPACE] == False:
	self.jumped = False
```
This is used in order to ensure that the self.jumped is false so we do not fly away to the top of nowhere.

### 🌍 Adding Gravity & Collision
**Q) Okay okay so we have jumped now but you said that we have to add gravity too and how do you prevent the player from falling below the screen if we haven't defined collisions??**  
A) Let's become Newton for a second! 🍎

```python
#add gravity
self.vel_y += 0.25  
if self.vel_y > 10:
    self.vel_y = 10
dy += self.vel_y
```
Yeah that's basically it, here we are first of all:
 creating a cap on the amount of velocity that the player can generate. 
 Then we are reducing the y coordinates of the player respectively by changing "dy"


Also for the time being we prevent the player from falling below the screen by:
```python
if self.rect.bottom > screen_height:
			self.rect.bottom = screen_height
			dy = 0
```
this basically ensures that the bottom of our defined player character cannot be below the height of the screen, if it is, we need to make it atleast equal to the height of the bottom of the screen and make change in y = 0.

That's it for day 2,
Had a lot of fun going over how to create a player character in pygame!
Really goes to show that there are so many things to consider while creating a game :D.

See you all tomorrow!