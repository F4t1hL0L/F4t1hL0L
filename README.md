- 👋 Hi, I’m @F4t1hL0L
- 👀 I’m interested in ...
- 🌱 I’m currently learning ...
- 💞️ I’m looking to collaborate on ...
- 📫 How to reach me ...
- 😄 Pronouns: ...
- ⚡ Fun fact: ...

<!---
F4t1hL0L/F4t1hL0L is a ✨ special ✨ repository because its `README.md` (this file) appears on your GitHub profile.
You can click the Preview link to take a look at your changes.
import pygame
import sys
import random

# Oyun ekranı boyutları
SCREEN_WIDTH = 800
SCREEN_HEIGHT = 600

# Renkler
WHITE = (255, 255, 255)
BLUE = (0, 0, 255)
RED = (255, 0, 0)

# Oyun başlangıç fonksiyonu
def main():
    pygame.init()
    screen = pygame.display.set_mode((SCREEN_WIDTH, SCREEN_HEIGHT))
    pygame.display.set_caption("Kaçan Top")

    clock = pygame.time.Clock()

    # Top
    ball_radius = 20
    ball_x = SCREEN_WIDTH // 2
    ball_y = SCREEN_HEIGHT // 2
    ball_dx = 5
    ball_dy = 5

    # Oyuncu
    player_width = 100
    player_height = 20
    player_x = (SCREEN_WIDTH - player_width) // 2
    player_y = SCREEN_HEIGHT - player_height - 10
    player_speed = 10

    # Oyun döngüsü
    running = True
    while running:
        for event in pygame.event.get():
            if event.type == pygame.QUIT:
                running = False

        # Klavye kontrolleri
        keys = pygame.key.get_pressed()
        if keys[pygame.K_LEFT]:
            player_x -= player_speed
        if keys[pygame.K_RIGHT]:
            player_x += player_speed

        # Oyuncu sınırları
        player_x = max(0, min(player_x, SCREEN_WIDTH - player_width))

        # Topun hareketi
        ball_x += ball_dx
        ball_y += ball_dy

        # Topun sınırları
        if ball_x - ball_radius <= 0 or ball_x + ball_radius >= SCREEN_WIDTH:
            ball_dx *= -1
        if ball_y - ball_radius <= 0 or ball_y + ball_radius >= SCREEN_HEIGHT:
            ball_dy *= -1

        # Topun oyuncu ile çarpışması
        if ball_y + ball_radius >= player_y and ball_x >= player_x and ball_x <= player_x + player_width:
            ball_dy *= -1

        # Ekranı temizle
        screen.fill(WHITE)

        # Topu çiz
        pygame.draw.circle(screen, BLUE, (ball_x, ball_y), ball_radius)

        # Oyuncuyu çiz
        pygame.draw.rect(screen, RED, (player_x, player_y, player_width, player_height))

        # Ekranı güncelle
        pygame.display.flip()

        clock.tick(60)

    pygame.quit()
    sys.exit()

if __name__ == "__main__":
    main()

