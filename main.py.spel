import pygame
import math
import random
from pygame import mixer

# Startar spelt
pygame.init()
# Skapar en skärm
scrren_w = 800
scrren_l = 600
screen = pygame.display.set_mode((scrren_w, scrren_l))

# bakgrund
background = pygame.image.load("bilder/bakrund spel.jpg")

# bakgrunds musik

# skapar titel och ikon
pygame.display.set_caption("Cops vs Terrorist")
icon = pygame.image.load("bilder/police-officer.png")
pygame.display.set_icon(icon)

# Spelare
playerImg = pygame.image.load("bilder/policeman.png")
spelareX = 370
spelareY = 480
spelareX_change = 0

# Fiende
enemyImg = []
fiendeX = []
fiendeY = []
fiendeX_change = []
fiendeY_change = []
num_av_fiender = 6

for i in range(num_av_fiender):
    enemyImg.append(pygame.image.load("bilder/terrorist.png"))
    fiendeX.append(random.randrange(0, 735))
    fiendeY.append(random.randrange(50, 150))
    fiendeX_change.append(0.5)
    fiendeY_change.append(40)

# skotten
# Redo betyder att man inte ser skotten på skärmen, men Avfyra betyder att skotten rör sig
bulletImg = pygame.image.load("bilder/bullet.png")
skottX = random.randint = 0
skottY = 480
skottX_change = 0
skottY_change = 1
skott_läge = "redo"

# poäng

poäng_value = 0
font = pygame.font.Font('freesansbold.ttf', 30)
textX = 340
textY = 20

def visa_poäng(textX,textY):
    poäng = font.render('Poäng :' + str(poäng_value), True, (0, 0, 0))
    screen.blit(poäng, (textX,textY))


def spelare(x, y):
    screen.blit(playerImg, (spelareX, spelareY))


def fiende(x, y, i):
    screen.blit(enemyImg[i], (fiendeX[i], fiendeY[i]))


# x + 16 0ch y + 10 gör så att skotten är i mitten av våran figur
def avfyra_skott(x, y):
    global skott_läge
    skott_läge = "avfyra"
    screen.blit(bulletImg, (x + 16, y + 10))


def iskollision(fiendeX, fiendeY, skottX, skottY):
    avstånd = math.sqrt((math.pow(fiendeX - skottX, 2)) + math.pow(fiendeY - skottY, 2))
    if avstånd < 27:
        return True
    else:
        return False


# Skapar en loop som är konsatant
running = True
while running:
    # RBG Färger, RBG = Röd, Blå, Grön
    screen.fill((0, 0, 0))
    # bakgrund
    screen.blit(background, (0, 0))
    for event in pygame.event.get():
        if event.type == pygame.QUIT:
            running = False

        # Om Tangenterna blir trycka kontrollera om det är höger eller vänster
        if event.type == pygame.KEYDOWN:
            if event.key == pygame.K_LEFT:
                spelareX_change = -1
            if event.key == pygame.K_RIGHT:
                spelareX_change = 1
            if event.key == pygame.K_SPACE:
                if skott_läge is "redo":
                    # ger oss x kordinaten av våran spelare/ polis
                    skottX = spelareX
                    avfyra_skott(spelareX, skottY)

        if event.type == pygame.KEYUP:
            if event.key == pygame.K_LEFT or event.key == pygame.K_RIGHT:
                spelareX_change = 0

    # kollar så att de finns gränser så att man inte försvinner utanför skärmen när man spelar
    spelareX += spelareX_change

    if spelareX <= 0:
        spelareX = 0
    elif spelareX >= 736:
        spelareX = 736

    # Fiende movment
    for i in range(num_av_fiender):
        fiendeX[i] += fiendeX_change[i]
        if fiendeX[i] <= 0:
            fiendeX_change[i] = 0.3
            fiendeY[i] += fiendeY_change[i]
        elif fiendeX[i] >= 736:
            fiendeX_change[i] = -0.3
            fiendeY[i] += fiendeY_change[i]

        # Kollision
        kollision = iskollision(fiendeX[i], fiendeY[i], skottX, skottY)
        if kollision:
            skottY = 480
            skott_läge = "redo"
            poäng_value += 1
            fiendeX[i] = random.randrange(0, 735)
            fiendeY[i] = random.randrange(50, 150)

        fiende(fiendeX[i], fiendeY[i], i)

    # skott movment
    if skottY <= 0:
        skottY = 480
        skott_läge = "redo"

    if skott_läge is "avfyra":
        avfyra_skott(skottX, skottY)
        skottY -= skottY_change

    spelare(spelareX, spelareY)
    visa_poäng(textX, textY)
    pygame.display.update()
