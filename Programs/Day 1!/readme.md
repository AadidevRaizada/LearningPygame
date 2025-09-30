Yo, for day 1 I used this tutorial:
https://www.youtube.com/watch?v=Ongc4EVqRjo&list=PLjcN1EyupaQnHM1I9SmiXfbT6aG4ezUvu

What'd I learn?

Q) What packages do we need to import?
A)We imported pygame and everything in pygame.locals

Q) How do you create the screen in PyGame?
A) We created a screen in PyGame, this screen will be used to play and run any games we will create in pygame.
For the screen we used:
screen_width = 750
screen_height = 750

screen = pygame.display.set_mode((screen_width, screen_height))

Q)How does the game run?
A)We created a loop that will keep running [while run == True] until user presents a command which will make the game exit, which in our case was closing the window.
run = True
while run:
    for event in pygame.event.get():
          if event.type == pygame.QUIT:
                run = False
    pygame.display.update()

Q) How do I add images in PyGame?
A) We use pygame's inbuilt function: pygame.image.load('image/path') to load any image within the game
bg_img = pygame.image.load('img/bg.png')
to display the image in the game, in the game running loop, we use  screen.blit(bg_img, (0, 0))

Q) How do I create a world in Pygame?
A) [Optiona]But create a grid which will divide your screen into equal sections. 
In the case of my code, I divided my grid into 5x5 sections of tile_size = 150 each.


Create a variable called world_data which will have your world's outline in 0's and 1's.
Then using the world_data variable [which is a list of lists] and the tile_size of each tile, we create a class "world".
This class has the data of the entire world which we would like to create for pygame.
world_data = [
[1,1,1,1,1],
[1,0,0,0,1],
[1,0,0,0,1],
[1,0,0,0,1],
[1,1,1,1,1]
]

We can load images for tiles here.

The tiles are transformed using a very basic loop:
 if tile == 1:
                           img = pygame.transform.scale(dirt_img, (tile_size, tile_size))
                           img_rect = img.get_rect()
                           img_rect.x = col_count * tile_size 
                           img_rect.x = row_count * tile_size 
                           tile = (img, img_rect)
                           self.tile_list.append(tile)
This loop states that if you want your game data to have a tile at a given place [based on your world data], you can transform and scale it into the size of your tile's length and width,
Then we convert it into a rectangle for convenience, and define its x and y coordinates based on which row, column needs to be transformed.
Finally, we create a tuple which will give us where all the tiles are and what are their values.

Q) Okay okay now we have a world but how will pygame load that world?
A) We create a basic function within the class world called draw(self)
def draw(self):
            for tile in self.tile_list:
                screen.blit(tile[0], tile[1])
                
based on our tuple and world data, this function will create tiles on our map accordingly.

Finally use these 3 functions in the final game running loop to load your world:
world.draw(), draw_grid(), print(world.tile_list)
<img width="935" height="958" alt="image" src="https://github.com/user-attachments/assets/a8c36580-2f4b-481d-9660-55a00f944ffe" />

