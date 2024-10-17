# Ex.No: 5  Implementation of Jumping behavior 
### DATE:23/8/24
### REGISTER NUMBER : 212221240047
### AIM: 
To write a python program to simulate Jumbing behavior. 
### Algorithm:
1. Start the program
2. Import the necessary modules
3. Initiate the pygame engine and window
4. Specify the necessary parameter for player height,depth,gravity,jump power. 
5. Create a game loop to simulate the continuous behavior.
6. If Quit button is pressed then quit the pygame window.
7. Move the player left when left button is pressed
8. Move the player right when right button is pressed
9. If space bar is pressed then enable the jump by increasing y axis value.
10. land the player and display the player at every timestep
11.  Stop the program
 ### Program:
```
import pygame

# Initialize Pygame
pygame.init()

# Screen dimensions
width, height = 800, 600
screen = pygame.display.set_mode((width, height))
pygame.display.set_caption("Simple Jumping with Sprite and Rectangles")

# Colors
black = (0, 0, 0)
white = (255, 255, 255)
red = (255, 0, 0)
green = (0, 255, 0)

# Player class definition
class Player(pygame.sprite.Sprite):
    def __init__(self, image_path):
        super().__init__()
        self.image = pygame.image.load(image_path)  # Load the PNG image
        self.image = pygame.transform.scale(self.image, (80, 100))  # Optionally scale the image to fit
        self.rect = self.image.get_rect()
        self.rect.x = 100  # Initial x-position
        self.rect.y = height - self.rect.height  # Initial y-position at the bottom of the screen
        self.velocity = 5  # Horizontal movement velocity
        self.jump_power = -15  # Jump power
        self.gravity = 1  # Gravity affecting the player
        self.is_jumping = False  # Track if the player is jumping
        self.vertical_speed = 0  # Initial vertical speed for jumping

    def update(self, keys):
        # Horizontal movement
        if keys[pygame.K_LEFT]:
            self.rect.x -= self.velocity
        if keys[pygame.K_RIGHT]:
            self.rect.x += self.velocity

        # Jumping logic
        if not self.is_jumping and keys[pygame.K_SPACE]:
            self.is_jumping = True
            self.vertical_speed = self.jump_power

        # Apply gravity when jumping
        if self.is_jumping:
            self.rect.y += self.vertical_speed
            self.vertical_speed += self.gravity

            # Check if player lands on the ground
            if self.rect.y >= height - self.rect.height:
                self.rect.y = height - self.rect.height
                self.is_jumping = False

# Path to the PNG image file
image_path = "C:\\Users\\91994\\Downloads\\file.png"  # Ensure you use double backslashes or a raw string for file paths on Windows

# Create a player instance with the PNG image
player = Player(image_path)

# Create a sprite group for easy management
all_sprites = pygame.sprite.Group()
all_sprites.add(player)

# Rectangle positions and sizes
rect1 = pygame.Rect(300, height - 100, 100, 50)  # First rectangle at (300, height - 100)
rect2 = pygame.Rect(500, height - 150, 100, 50)  # Second rectangle at (500, height - 150)

# Game loop
running = True
while running:
    for event in pygame.event.get():
        if event.type == pygame.QUIT:
            running = False

    # Get the keys pressed
    keys = pygame.key.get_pressed()

    # Update all sprites (in this case, just the player)
    all_sprites.update(keys)

    # Clear the screen
    screen.fill(black)

    # Draw two rectangles
    pygame.draw.rect(screen, red, rect1)  # Draw first red rectangle
    pygame.draw.rect(screen, green, rect2)  # Draw second green rectangle

    # Draw all sprites (player sprite)
    all_sprites.draw(screen)

    # Update the display
    pygame.display.flip()

    # Frame rate control
    pygame.time.delay(30)

# Quit Pygame
pygame.quit()

```

### Output:

![image](https://github.com/user-attachments/assets/57f2e161-bee8-4ab7-a31a-b422667a7b5b)
![image](https://github.com/user-attachments/assets/e732ec12-7993-4a62-8f4c-bde58237359d)



### Result:
Thus the simple jumping behavior  was implemented.
