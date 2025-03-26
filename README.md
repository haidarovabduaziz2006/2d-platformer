import pygame

# Инициализация Pygame
pygame.init()

# Параметры экрана
SCREEN_WIDTH = 800
SCREEN_HEIGHT = 600
screen = pygame.display.set_mode((SCREEN_WIDTH, SCREEN_HEIGHT))
pygame.display.set_caption("2D Platformer")

# Цвета
WHITE = (255, 255, 255)
BLACK = (0, 0, 0)
GREEN = (0, 255, 0)
BLUE = (0, 0, 255)

# Класс игрока
class Player(pygame.sprite.Sprite):
    def __init__(self):
        super().__init__()
        self.image = pygame.Surface((50, 50))
        self.image.fill(BLUE)
        self.rect = self.image.get_rect()
        self.rect.center = (100, 550)
        self.speed = 5
        self.gravity = 1
        self.velocity = 0
        self.on_ground = False

    def update(self):
        keys = pygame.key.get_pressed()

        # Движение влево/вправ
        if keys[pygame.K_LEFT]:
            self.rect.x -= self.speed
        if keys[pygame.K_RIGHT]:
            self.rect.x += self.speed

        # Гравитация
        self.velocity += self.gravity
        self.rect.y += self.velocity

        # Проверка на землю
        if self.rect.bottom >= SCREEN_HEIGHT:
            self.rect.bottom = SCREEN_HEIGHT
            self.velocity = 0
            self.on_ground = True
        else:
            self.on_ground = False

        # Прыжок
        if self.on_ground and keys[pygame.K_SPACE]:
            self.velocity = -15

# Основная функция игры
def game():
    clock = pygame.time.Clock()
    player = Player()
    all_sprites = pygame.sprite.Group()
    all_sprites.add(player)

    platforms = pygame.sprite.Group()

    # Платформы
    ground = pygame.Surface((SCREEN_WIDTH, 50))
    ground.fill(GREEN)
    ground_rect = ground.get_rect()
    ground_rect.topleft = (0, SCREEN_HEIGHT - 50)
    platforms.add(pygame.sprite.Sprite())
    platforms.sprites()[-1].image = ground
    platforms.sprites()[-1].rect = ground_rect

    # Главный игровой цикл
    running = True
    while running:
        for event in pygame.event.get():
            if event.type == pygame.QUIT:
                running = False

        # Обновление
        all_sprites.update()

        # Отображение
        screen.fill(WHITE)
        all_sprites.draw(screen)
        platforms.draw(screen)

        pygame.display.flip()

        clock.tick(60)

    pygame.quit()

# Запуск игры
if __2d платформер__ == "__main__":
    game()
