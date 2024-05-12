import pygame
import random

# Definir colores
BLANCO = (255, 255, 255)
NEGRO = (0, 0, 0)
VERDE = (0, 255, 0)

# Definir dimensiones de la pantalla
ANCHO = 800
ALTO = 600

class Residuo(pygame.sprite.Sprite):
    def __init__(self, color):
        super().__init__()
        self.image = pygame.Surface([30, 30])
        self.image.fill(color)
        self.rect = self.image.get_rect()
        self.rect.x = random.randint(0, ANCHO - self.rect.width)
        self.rect.y = random.randint(-100, -40)
        self.velocidad = random.randint(1, 5)

    def update(self):
        self.rect.y += self.velocidad
        if self.rect.y > ALTO:
            self.rect.y = random.randint(-100, -40)
            self.rect.x = random.randint(0, ANCHO - self.rect.width)

# Inicializar Pygame
pygame.init()

# Configurar la pantalla
pantalla = pygame.display.set_mode((ANCHO, ALTO))
pygame.display.set_caption("EcoSorting: Separación de Residuos")

# Reloj para controlar la velocidad de actualización de la pantalla
reloj = pygame.time.Clock()

# Grupo de sprites para los residuos
todos_los_sprites = pygame.sprite.Group()

# Función para generar residuos
def generar_residuos():
    residuos = Residuo(random.choice([BLANCO, NEGRO, VERDE]))
    todos_los_sprites.add(residuos)

# Bucle principal del juego
jugando = True
while jugando:
    # Manejo de eventos
    for evento in pygame.event.get():
        if evento.type == pygame.QUIT:
            jugando = False

    # Generar residuos aleatoriamente
    if random.randint(1, 100) < 10:
        generar_residuos()

    # Actualizar la posición de los residuos
    todos_los_sprites.update()

    # Limpiar la pantalla
    pantalla.fill(BLANCO)

    # Dibujar todos los sprites
    todos_los_sprites.draw(pantalla)

    # Actualizar la pantalla
    pygame.display.flip()

    # Limitar la velocidad de fotogramas
    reloj.tick(60)

# Salir del juego
pygame.quit()


