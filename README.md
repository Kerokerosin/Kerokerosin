# coding: utf8
import pygame
import random
high = 0
# задааем размер окна, создаем окно размера size
size = [400, 400]
window = pygame.display.set_mode(size)
# задаем имя - в кавычках, т.к. текст - это строка
pygame.display.set_caption('My second file')

screen = pygame.Surface(size)

class Sprite:
    def __init__(self, xpos, ypos, filename):
        self.x = xpos
        self.y = ypos
        self.bitmap = pygame.image.load(filename)
    def render(self):
        screen.blit(self.bitmap,(self.x, self.y))


def Intersect(s1_x, s2_x, s1_y, s2_y):
    if ((s1_x>s2_x-40) and (s1_x<s2_x+40) and (s1_y>s2_y-40) and (s1_y<s2_y+40)):
        return 1
    else:
        return 0

# создание персонажей
# герой

# переменные-"переключатели" движения для героя
#hero.right = True
#hero.up = True
# враг
enemy = Sprite(200, 10, 'png1.png')
# переменные-"переключатели" движения для врага
enemy.right = True

strela = Sprite (23121412, 10000, 'png3.png')
strela.up = False

count = 0
running = True


x_user = int(input('Input hero place X:  '))
y_user = int(input('Input hero place Y:  '))

hero = Sprite(x_user, y_user, 'png2.png')

enemy_new = True
pygame.key.set_repeat(1,1)
while running:
    # обработка событий
    for e in pygame.event.get():
        if e.type == pygame.QUIT:
            running  = False
        if e.type == pygame.KEYDOWN:
            if e.key == pygame.K_LEFT:
                if hero.x > 10:
                    hero.x -= 1
            if e.key == pygame.K_RIGHT:
                if hero.x < 350:
                    hero.x += 1
            if e.key == pygame.K_UP:
                if hero.y > 200:
                    hero.y -= 1
            if e.key == pygame.K_DOWN:
                if hero.y < 350:
                    hero.y += 1
            if e.key == pygame.K_SPACE:
                strela.x = hero.x
                strela.y = hero.y
                strela.up = True 
               
                
                
            
                

    # задайте фоновый цвет
    screen.fill([23, 198, 95])

    # движение персонажей - аналогично тому,
    # что делали с квадратом, но теперь по вертикали
    '''
    if hero.up == True:
        hero.y -= 1
        if hero.y < 0:
            hero.up = False
    else:
        hero.y += 1
        if hero.y > 360:
            hero.up = True
    '''
   
    if enemy.right == True:
        if enemy.x < 360:
            enemy.x += 5
        else :
            enemy.right = False
    if enemy.right == False:
        if enemy.x > 0 :
            enemy.x -= 5
        else:
            enemy.right = True
            
    
    if strela.up == True:
        strela.y -= 5
    


    # столкновение персонажей
    if Intersect(strela.x, enemy.x, strela.y, enemy.y):
        strela.up = False
        strela.x = -400
        strela.y = -400
       

       

    # отображение персонажей
    hero.render()
    enemy.render()
    strela.render()
    
    # отображение окна
    window.blit(screen, [0, 0])
    pygame.display.flip()
    pygame.time.delay(50)


pygame.quit()
