import pygame


pygame.init()


back = (200, 255, 255)
mw = pygame.display.set_mode((500, 500))
mw.fill(back)


clock = pygame.time.Clock()


class Area():
    def __init__(self, x = 0, y = 0, width = 10, height = 10, color = None):
        self.rect = pygame.Rect(x, y, width, height)
        self.fill_color = back


    def color(self, new_color):
        self.fill_color = new_color


    def fill(self):
        pygame.draw.rect(mw, self.fill_color, self.rect)
    

    def colliderect(self, rect):
        return self.rect.colliderect(rect)


class Picture(Area):
    def __init__(self, filename, x = 0, y = 0, width = 10, height = 10):
        super().__init__(x = x, y = y, width = width, height = height, color = None)
        self.image = pygame.image.load(filename)


    def draw(self):
        mw.blit(self.image, (self.rect.x, self.rect.y))


class Label(Area):
    def set_text(self, text, fsize=12, text_color=(0, 0, 0)):
        self.image = pygame.font.SysFont('verdana', fsize).render(text, True, text_color)


    def draw(self, shift_x=0, shift_y=0):
        self.fill()
        mw.blit(self.image, (self.rect.x + shift_x, self.rect.y + shift_y))


RED = (255, 0, 0)
GREEN = (0, 255, 51)
BlUE = (198,186,253)
ORANGE = (255, 123, 0)
WHITE = (255, 255, 255)
YELLOW = (255, 255, 0)
LIGHT_GREEN = (200, 255, 200)
LIGHT_RED = (250, 128, 114)
BLACK = (0, 0, 0)
DARK_BLUE = (0, 0, 100)
LIGHT_BLUE = (200,200,254)
PINK = (255, 192, 203)


racket_x = 200
racket_y = 330
dy = 3
dx = 3
move_left = False
move_right = False
game = False
start_x = 5
start_y = 5
count = 9


monsters = []
for j in range(3):
    y = start_y + (55 * j)
    x = start_x + (27.5 * j)
    for i in range(count):
        d = Picture('enemy.png', x, y, 50, 50)
        monsters.append(d)
        x = x + 55
    count = count - 1


platform = Picture('platform.png', racket_x, racket_y, 100, 30)


ball = Picture('ball.png', 160, 200, 50, 50)


while not game:
    platform.fill()
    ball.fill()


    for event in pygame.event.get():
        if event.type == pygame.QUIT:
            game = True
        if event.type == pygame.KEYDOWN:
            if event.key == pygame.K_LEFT:
                move_left = True
            if event.key == pygame.K_RIGHT:
                move_right = True
            if event.key == pygame.K_e:
                game = True
        elif event.type == pygame.KEYUP:
            if event.key == pygame.K_LEFT:
                move_left = False
            if event.key == pygame.K_RIGHT:
                move_right = False
            if event.key == pygame.K_e:
                game = False


    if move_right:
        platform.rect.x += 3
    if move_left:
        platform.rect.x -=3 


    if platform.rect.x >= 400:
        platform.rect.x -= 3
    if platform.rect.x <= 0:
        platform.rect.x += 3


    ball.rect.x += dx
    ball.rect.y += dy
    

    if ball.rect.y < 0:
        dy *= -1
    if ball.rect.x < 0 or ball.rect.x > 450:
        dx *= -1
        if ball.rect.y > 500:
            lose_text = Label(0, 0, 500, 500)
            lose_text.set_text('Вы проиграли!', 60, RED)
            lose_text.draw(110, 180)
            game = True

        if len(monsters) == 0:
            win_text = Label(0, 0, 500, 500)
            win_text.set_text('Вы выиграли!', 60, GREEN)
            win_text.draw(140, 180)
            game = True


    if ball.rect.colliderect(platform.rect):
        dy *= -1


    for m in monsters:
        m.draw()
        if m.rect.colliderect(ball.rect):
            monsters.remove(m)
            m.fill()
            dy *= -1


    platform.draw()
    ball.draw()


    pygame.display.update()
    clock.tick(40)
