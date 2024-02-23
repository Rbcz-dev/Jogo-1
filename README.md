# Meus jogos




import random

import pygame

# Inicialização do Pygame
pygame.init()

# Definição das cores
BLACK = (0, 0, 0)  ; GREEN = (0, 255, 0) ; RED = (255, 0, 0)

# Configurações da janela do jogo
W = 1200
H = 700
CELL_SIZE = 20
FPS =8


# Criação da janela
window = pygame.display.set_mode((W, H))
pygame.display.set_caption('cobrinha Game')

clock = pygame.time.Clock()

# Função principal do jogo
def main():
    cobrinha = [[100, 100], [120, 100], [140, 100]]  # Inicialização da cobra
    direction = 'RIGHT'  # Direção inicial da cobra
    food_position = [random.randrange(1, (W//CELL_SIZE)) * CELL_SIZE,
                     random.randrange(1, (H//CELL_SIZE)) * CELL_SIZE]
    pontuação:int =+   1

    while True:
        for event in pygame.event.get():
            if event.type == pygame.QUIT:
                pygame.quit()
                quit()

            # Captura das teclas pressionadas para controlar a direção da cobra
            elif event.type == pygame.KEYDOWN:
                if event.key == pygame.K_LEFT:
                    direction = 'LEFT'
                elif event.key == pygame.K_RIGHT:
                    direction = 'RIGHT'
                elif event.key == pygame.K_UP:
                    direction = 'UP'
                elif event.key == pygame.K_DOWN:
                    direction = 'DOWN'

        # Movimento da cobra
        if direction == 'LEFT':
            cobrinha.insert(0, [cobrinha[0][0] - CELL_SIZE, cobrinha[0][1]])
        elif direction == 'RIGHT':
            cobrinha.insert(0, [cobrinha[0][0] + CELL_SIZE, cobrinha[0][1]])
        elif direction == 'UP':
            cobrinha.insert(0, [cobrinha[0][0], cobrinha[0][1] - CELL_SIZE])
        elif direction == 'DOWN':
            cobrinha.insert(0, [cobrinha[0][0], cobrinha[0][1] + CELL_SIZE])

        # Verifica se a cobra comeu a comida
        if cobrinha[0] == food_position:
            food_position = [random.randrange(1, (W//CELL_SIZE)) * CELL_SIZE,
                             random.randrange(1, (H//CELL_SIZE)) * CELL_SIZE]

        else:
            cobrinha.pop()

        # Atualiza a tela
        window.fill(BLACK)
        pygame.draw.rect(window, RED, (food_position[0], food_position[1], 
                                       CELL_SIZE, CELL_SIZE))
        for segment in cobrinha:
            pygame.draw.rect(window, GREEN, (segment[0], segment[1],
                                             CELL_SIZE, CELL_SIZE))
        font = pygame.font.Font(None, 36)
        text = font.render(f'Pontuação: {pontuação}',True,(255,255,255))
        window.blit(text, (10, 10))
        pygame.display.update()

        # Limita a taxa de quadros por segundo
        clock.tick(FPS)

if __name__ == '__main__':
    main()





