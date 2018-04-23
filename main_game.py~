import pygame
import os
import random
import time

pygame.init()

os.environ['SDL_VIDEO_WINDOW_POS'] = "400, 100"
display_width = 600
display_height = 600

black = (0, 0, 0)
white = (255, 255, 255)
red = (255, 0, 0)

car_width = 73

gameDisplay = pygame.display.set_mode((display_width, display_height))
pygame.display.set_caption('Save The Minion!!!')
clock = pygame.time.Clock()

minionImg = pygame.image.load('minion.png')
minionImg_crushed = pygame.image.load('minion_crashed.png')


def things_dodged(count):
    font = pygame.font.SysFont(None, 25)
    text = font.render("Score: "+str(count), True, black)
    gameDisplay.blit(text, (0, 0))


def things(thing_x, thing_y, thing_w, thing_h, color):
    pygame.draw.rect(gameDisplay, color, [thing_x, thing_y, thing_w, thing_h])


def car(x, y, car_img):
    gameDisplay.blit(car_img, (x, y))


def button(msg, x, y, w, h, ic, ac, action=None):
    mouse = pygame.mouse.get_pos()
    click = pygame.mouse.get_pressed()

    if x+w > mouse[0] > x and y+h > mouse[1] > y:
        pygame.draw.rect(gameDisplay, ac,(x,y,w,h))

        if click[0] == 1:
            action()
    else:
        pygame.draw.rect(gameDisplay, ic, (x, y, w, h))

    smallText = pygame.font.SysFont("comicsansms", 20)
    textSurf, textRect = text_objects(msg, smallText)
    textRect.center = ((x+(w/2)), (y+(h/2)))
    gameDisplay.blit(textSurf, textRect)


def text_objects(text, font):
    text_surface = font.render(text, True, red)
    return text_surface, text_surface.get_rect()


def message_display(text):
    large_text = pygame.font.Font('freesansbold.ttf', 100)
    text_surf, text_rect = text_objects(text, large_text)
    text_rect.center = ((display_width / 2), (display_height / 2) - 50)
    gameDisplay.blit(text_surf, text_rect)

    pygame.display.update()

    # time.sleep(1)

    # game_loop()


def crash():
    button("Play Again", (display_width / 2 - 25), (display_height / 2), 100, 40, black, black, game_loop)
    message_display('Crashed !!!')


def game_loop():
    x = (display_width * 0.45)
    y = (display_height * 0.8)

    x_change = 0

    thing_start_x = random.randrange(0, display_width)
    thing_start_y = 0 - display_height
    thing_speed = 8
    thing_width = 60
    thing_height = 100

    crashed = 0

    dodged = 0

    game_exit = False
    image = minionImg

    while not game_exit:

        for event in pygame.event.get():

            if event.type == pygame.QUIT:
                game_exit = True

            if event.type == pygame.KEYDOWN and crashed == 0:
                if event.key == pygame.K_LEFT:
                    x_change = -6
                if event.key == pygame.K_RIGHT:
                    x_change = 6

            if event.type == pygame.KEYUP and crashed == 0:
                if event.key == pygame.K_LEFT or event.key == pygame.K_RIGHT:
                    x_change = 0

            # if crashed == 1:
            #     x_change = 0
        if crashed == 0:
            x += x_change
        gameDisplay.fill(white)

        things(thing_start_x, thing_start_y, thing_width, thing_height, red)
        if crashed == 0:
            thing_start_y += thing_speed
            image = minionImg
        car(x, y, image)
        things_dodged(dodged)

        if x > display_width - car_width or x < 0:
            crashed = 1
            image = minionImg_crushed
            crash()

        if thing_start_y > display_height:
            thing_start_y = 0 - thing_height
            thing_start_x = random.randrange(0, display_width)
            dodged += 1
            thing_speed += 0.5

        if y < thing_start_y + thing_height:
            if ((x > thing_start_x) and x < (thing_start_x + thing_width)) or (x + car_width > (thing_start_x) and (x + car_width) < (thing_start_x + thing_width)) or x == thing_start_x:
                crashed = 1
                image = minionImg_crushed
                crash()

        pygame.display.update()
        clock.tick(60)


game_loop()
pygame.quit()
quit()
