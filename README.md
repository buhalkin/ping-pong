# ping-pong
the old fashioned game
from pygame import *
clock = time.Clock()
w_w = 1500
w_h = 900
run = True
window = display.set_mode((w_w,w_h))
display.set_caption("Пинг-Понг")
background = transform.scale(image.load("neon.jpg"),(w_w,w_h))
player_x = 17
player_y = 150
class GameSprite(sprite.Sprite):
    def __init__(self, play_image, play_x, play_y, play_speed):
        super().__init__()
        self.image = transform.scale(image.load(play_image), (player_x,player_y))
        self.speed = play_speed
        self.rect = self.image.get_rect()
        self.rect.x = play_x
        self.rect.y = play_y
    def reset(self):
        window.blit((self.image), (self.rect.x, self.rect.y))


class Patron(sprite.Sprite):
    def __init__(self,weight,height,pos_x,pos_y,colour,):
        super().__init__()
        self.image = Surface((weight,height))
        self.image.fill(colour)
        self.rect = self.image.get_rect()
        self.rect.x = pos_x
        self.rect.y = pos_y
    def reset(self):
        window.blit((self.image), (self.rect.x, self.rect.y))
class Player(Patron):
    def move1(self):
        key_key = key.get_pressed()
        if key_key[K_w] and self.rect.y > 0:          
            self.rect.y -= 10         
        if key_key[K_s] and self.rect.y < w_h - player_y:           
            self.rect.y += 10 
    def move2(self):
        key_key = key.get_pressed()
        if key_key[K_UP] and self.rect.y > 0:          
            self.rect.y -= 10         
        if key_key[K_DOWN] and self.rect.y < w_h - player_y:           
            self.rect.y += 10 
play1 = Player(player_x+5,player_y+5, 1/10*w_w-player_x, w_h/2-player_y/2,(0,255,255)) 
play2 = Player(player_x+5,player_y+5, 9/10*w_w, w_h/2-player_y/2,(255,0,255))
    
while run:
    window.blit(background,(0,0))
    play1.reset()
    play1.move1()
    play2.reset()
    play2.move2()
    for e in event.get():
        if e.type == QUIT:          
            run = False
        if e.type == KEYDOWN:
            if e.key == K_F10:
                window = display.set_mode((w_w,w_h))
            if e.key == K_F11:
                window = display.set_mode((w_w,w_h),FULLSCREEN) 
    clock.tick(60)
    display.update()
