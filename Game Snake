# snake-game
import pygame
import time
import random

pygame.init()

name = input("Enter your username: ")

yellow = (249, 200, 14)
black = (13, 2, 33)
red = (255, 56, 100)
green = (255, 108, 17)
blue = (45, 226, 230)
purple = (38, 20, 71)

display_x = 600
display_y = 400

dis = pygame.display.set_mode((display_x, display_y))
pygame.display.set_caption("Snake Game")

clock = pygame.time.Clock()

snake_block = 10
snake_speed = 15

font_text = pygame.font.SysFont("opensans", 25)
font_score = pygame.font.SysFont("comicsansms", 35)


def display_snake(snake_block, snake_list):
    for x in snake_list:
        pygame.draw.rect(dis, black, [x[0], x[1], snake_block, snake_block])


def display_score(score):
    value = font_score.render(name + "'s Score: " + str(score), True, yellow)
    dis.blit(value, [0, 0])


def display_msg(msg, color):
    msg_rendered = font_text.render(msg, True, color)
    dis.blit(msg_rendered, [display_x / 6, display_y / 3])


def gameLoop():
    game_over = False
    game_close = False

    snake_x = display_x / 2
    snake_y = display_y / 2

    snake_dx = 0
    snake_dy = 0

    snake_blocks = []
    snake_length = 1

    food_x = round(random.randrange(0, display_x - snake_block) / 10.0) * 10.0
    food_y = round(random.randrange(0, display_y - snake_block) / 10.0) * 10.0

    while not game_over:
        while game_close == True:
            dis.fill(blue)
            display_msg("You Lost! Press Enter to Play Again or Q to Quit", red)
            display_score(snake_length - 1)
            pygame.display.update()

            for event in pygame.event.get():
                if event.type == pygame.KEYDOWN:
                    if event.key == pygame.K_q:
                        game_over = True
                        game_close = False
                    if event.key == pygame.K_RETURN:
                        gameLoop()

        for event in pygame.event.get():
            if event.type == pygame.QUIT:
                game_over = True
            if event.type == pygame.KEYDOWN:
                if event.key == pygame.K_LEFT:
                    snake_dx = -snake_block
                    snake_dy = 0
                elif event.key == pygame.K_RIGHT:
                    snake_dx = snake_block
                    snake_dy = 0
                elif event.key == pygame.K_UP:
                    snake_dy = -snake_block
                    snake_dx = 0
                elif event.key == pygame.K_DOWN:
                    snake_dy = snake_block
                    snake_dx = 0

        if snake_x >= display_x or snake_x < 0 or snake_y >= display_y or snake_y < 0:
            game_close = True

        snake_x += snake_dx
        snake_y += snake_dy
        dis.fill(blue)
        pygame.draw.rect(dis, green, [food_x, food_y, snake_block, snake_block])
        snake_Head = []
        snake_Head.append(snake_x)
        snake_Head.append(snake_y)
        snake_blocks.append(snake_Head)
        if len(snake_blocks) > snake_length:
            del snake_blocks[0]

        for x in snake_blocks[:-1]:
            if x == snake_Head:
                game_close = True

        display_snake(snake_block, snake_blocks)
        display_score(snake_length - 1)

        pygame.display.update()

        if snake_x == food_x and snake_y == food_y:
            food_x = round(random.randrange(0, display_x - snake_block) / 10.0) * 10.0
            food_y = round(random.randrange(0, display_y - snake_block) / 10.0) * 10.0
            snake_length += 1

        clock.tick(snake_speed)

    pygame.quit()
    quit()


gameLoop()
