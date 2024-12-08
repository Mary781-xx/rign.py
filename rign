import pygame
import math
import random
import sys
import time
pygame.init()
WIDTH, HEIGHT = 800, 600
FPS = 60
RADIUS = 200  
CENTER = (WIDTH // 2, HEIGHT // 2)  
SPEED = (4 * math.pi / FPS) / 2  
MIN_ANGLE_RANGE = (2 * math.pi) / 9  
MAX_ANGLE_RANGE = (6 * math.pi) / 9  
WHITE = (255, 255, 255)
RED = (255, 0, 0)
BLACK = (0, 0, 0)
def main():
    screen = pygame.display.set_mode((WIDTH, HEIGHT))
    pygame.display.set_caption("Игра Кольцо")
    clock = pygame.time.Clock()

    angle = 0  
    score = 0  
    target_start_angle = random.uniform(0, 1.2*math.pi)  
    target_end_angle = (target_start_angle + random.uniform(MIN_ANGLE_RANGE, MAX_ANGLE_RANGE))  
    start_time = time.time()
    last_click_time = time.time() 
    running = True

    while running:
        for event in pygame.event.get():
            if event.type == pygame.QUIT:
                running = False
            if event.type == pygame.MOUSEBUTTONDOWN:
                ball_x = CENTER[0] + RADIUS * math.cos(angle)
                ball_y = CENTER[1] + RADIUS * math.sin(angle)
                if (target_start_angle <= angle <= target_end_angle):
                    score += 1
                    target_start_angle = random.uniform(0, 1.2*math.pi)
                    target_end_angle = (target_start_angle + random.uniform(MIN_ANGLE_RANGE, MAX_ANGLE_RANGE))
                else:
                    score -= 1 
                last_click_time = time.time()  
        screen.fill(WHITE)
        pygame.draw.circle(screen, BLACK, CENTER, RADIUS, 5)
        for i in range(1000): 
            start_angle = target_start_angle + (i / 1000) * (target_end_angle - target_start_angle)
            end_angle = target_start_angle + ((i + 1) / 1000) * (target_end_angle - target_start_angle)
            pygame.draw.polygon(screen, RED,
                                [CENTER,
                                 (CENTER[0] + RADIUS * math.cos(start_angle), CENTER[1] + RADIUS * math.sin(start_angle)),
                                 (CENTER[0] + RADIUS * math.cos(end_angle), CENTER[1] + RADIUS * math.sin(end_angle))])
        ball_x = CENTER[0] + RADIUS * math.cos(angle)
        ball_y = CENTER[1] + RADIUS * math.sin(angle)
        pygame.draw.circle(screen, BLACK, (int(ball_x), int(ball_y)), 10)
        angle += SPEED
        if angle >= 2 * math.pi:
            angle -= 2 * math.pi
        if time.time() - start_time >= 60: 
            print("Время вышло! Ваш финальный счет:", score)
            running = False
        if time.time() - last_click_time > (2 * math.pi / SPEED): 
            score -= 1
        font = pygame.font.Font(None, 60)
        text = font.render(f"Очки: {score}", True, BLACK)
        screen.blit(text, (10, 10))
        pygame.display.flip()
        clock.tick(FPS)
    pygame.quit()
    sys.exit()
if __name__ == "__main__":
    main()
