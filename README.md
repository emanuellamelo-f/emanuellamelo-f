# 👩🏻‍💻 Emanuella de Cássia Fragoso de Melo Amorim

**`Engenheira (Engenharia Elétrica & Computação) | Assistente Administrativa Plena | Robótica`**

> "Profissional proativa com sólida base em Administração (4 anos de experiência), complementada por conhecimento técnico em Engenharia Elétrica e Engenharia da Computação, Desenvolvimento (Lógica de Programação) e Análise de Dados. Buscando aplicar habilidades em otimização de rotinas e suporte operacional para o sucesso da equipe."

---

## 🔵 Contato & Redes

* **Telefone:** (82) 99909-3075
* **Email:** manufragoso.melo@gmail.com
* **GitHub:** [emanuellamelo-f](https://github.com/emanuellamelo-f)
* **LinkedIn:** [Emanuella Fragoso](https://www.linkedin.com/in/emanuella-fragoso-98b305237/)

<p align="left">
    <a href="https://www.linkedin.com/in/emanuella-fragoso-98b305237/">
        <img alt="LinkedIn" title="Meu Perfil no LinkedIn" src="https://img.shields.io/badge/LinkedIn-0077B5?style=for-the-badge&logo=linkedin&logoColor=white"/>
    </a>
    <a href="mailto:manufragoso.melo@gmail.com">
        <img alt="Email" title="Mande um Email" src="https://img.shields.io/badge/Email-D14836?style=for-the-badge&logo=gmail&logoColor=white"/>
    </a>
</p>

---

## 🎓 Formação Acadêmica

| Instituição | Curso | Situação | Período |
| :--- | :--- | :--- | :--- |
| **Universidade Federal de Alagoas (UFAL)** | Engenharia Elétrica | Cursando | 2022 - 2027 |
| **Centro Universitário - UFBRA** | Engenharia da Computação | Cursando | Início em 2025 |
| **SENAI - Alagoas** | Técnico em Edificações | Concluído | 2011 - 2013 |

---

## 🔴 Experiência Profissional e Projetos

### 1. 🤖 Projeto de Robótica SUMO - IEEE UFAL
* **Função:** Componente da Equipe Cyber Dragon (UFAL IEEE RAS)
* **Atuação:** Central na concepção e engenharia completa do robô de SUMO.
* **Responsabilidades:** Projeto mecânico (chassi e "pa") e seleção de componentes eletrônicos (motores e sensores); desenvolvimento da inteligência autônoma, programando as lógicas de busca, ataque e evasão.

### 2. 🗃️ Assistente Administrativo | Bolsista de Extensão UFAL - Conexões de Saberes
* **Período:** 2021 - Atualmente
* **Atuação:** Assistente administrativo com 4 anos de experiência na área, focado em organização, suporte operacional e otimização de rotinas de escritório.
* **Destaques:** Domínio do Pacote Office (especialmente Excel), gestão de agendas, controle de documentos e elaboração de relatórios.

### 3. 📐 Estagiária Técnica em Edificações | Camila Santos Arquitetura
* **Período:** Concluido em 2018
* **Destaques:** Experiência em leitura de plantas baixas (elétricas, hidráulicas e estruturais) e criação/aprimoramento de projetos em **AutoCAD**.

---

## 🛠️ Habilidades Técnicas

* **PACOTE OFFICE:** Avançado
* **GESTÃO DE PROJETOS:** Avançado
* **CANVA:** Intermediário
* **AUTOCAD:** Intermediário
* **Lógica de Programação:** Conhecimento técnico
* **Em Desenvolvimento:** JavaScript (300h), HTML (300h), POO Python (300h)
* **Análise de Dados:** Cursando (60h - Google-CIEE)

---

## 🗣️ Idiomas & Cursos

### Idiomas
* **Inglês:** Leitura de textos Avançado; Básico
* **Espanhol:** Básico

### Cursos Complementares
* **Certificação/Curso Técnico (NetAcad/Cisco):** [Acesse o Currículo](https://www.netacad.com/launch?id=da0847b7-e6fc-4597-bc31-38ddd6b07a2e&tab=curriculum&view=69de6c15-5a17-5e25-849d-e2a9884de14a)
* **Administração Financeira:** 40 horas (IFRS - 2005)
* **Lógica de Programação: mergulhe em programação com JavaScript:** 6 horas (ALURA - Out/2025)

  </p>
import pygame
import math
import sys

# --- 1. Inicialização e Configurações ---
pygame.init()

# Configurações da Tela
SCREEN_WIDTH = 800
SCREEN_HEIGHT = 800
screen = pygame.display.set_mode((SCREEN_WIDTH, SCREEN_HEIGHT))
pygame.display.set_caption("O Estômago Rotativo - Pac-Man Inédito")

# Cores
BLACK = (0, 0, 0)
WHITE = (255, 255, 255)
RED = (200, 50, 50)
BLUE = (50, 50, 200)
PURPLE = (150, 0, 150)
GREEN = (0, 150, 0)
ORANGE = (255, 100, 0)

# Configurações do Jogo
CENTER_X = SCREEN_WIDTH // 2
CENTER_Y = SCREEN_HEIGHT // 2
FPS = 60
clock = pygame.time.Clock()

# --- 2. Classe do Jogador (O Comilão) ---
class Comilao(pygame.sprite.Sprite):
    def __init__(self):
        super().__init__()
        self.image = pygame.Surface([20, 20], pygame.SRCALPHA)
        pygame.draw.circle(self.image, ORANGE, (10, 10), 10)
        self.rect = self.image.get_rect()
        self.rect.center = (CENTER_X, CENTER_Y + 50)  # Posição inicial no Anel 1
        self.speed = 3

    def update(self, keys):
        # Movimento Básico
        new_x = self.rect.x
        new_y = self.rect.y

        if keys[pygame.K_LEFT]:
            new_x -= self.speed
        if keys[pygame.K_RIGHT]:
            new_x += self.speed
        if keys[pygame.K_UP]:
            new_y -= self.speed
        if keys[pygame.K_DOWN]:
            new_y += self.speed

        # **Simplificação**: A lógica real de colisão e rotação seria implementada aqui.
        # Por exemplo, recalcular a posição baseada na rotação do anel em que ele está.
        self.rect.x = new_x
        self.rect.y = new_y

# --- 3. Lógica do Labirinto Rotativo ---
class LabirintoRotativo:
    def __init__(self):
        # Dimensões dos Anéis (Raio)
        self.r_nucleo = 50
        self.r_anel1 = 120  # Anel Estreito
        self.r_anel2 = 250  # Anel Principal
        self.r_anel3 = 350  # Anel Exterior

        # Variáveis de Rotação
        self.angulo_anel1 = 0  # Gira Anti-Horário
        self.velocidade_anel1 = -0.5  # graus por frame

        self.angulo_anel2 = 0  # Gira Horário
        self.velocidade_anel2 = 0.8  # graus por frame

    def update(self):
        # Atualiza a rotação dos anéis a cada frame
        self.angulo_anel1 += self.velocidade_anel1
        self.angulo_anel2 += self.velocidade_anel2

        # Garante que o ângulo permaneça entre 0 e 360
        self.angulo_anel1 %= 360
        self.angulo_anel2 %= 360

    def draw_labyrinth(self, surface):
        # Desenha o Fundo (Contexto Biológico/Orgânico)
        surface.fill((10, 30, 40)) # Azul Marinho Escuro

        # 1. Anel 3 (Exterior - Fixo)
        pygame.draw.circle(surface, ORANGE, (CENTER_X, CENTER_Y), self.r_anel3, 40)
        pygame.draw.circle(surface, RED, (CENTER_X, CENTER_Y), self.r_anel3 + 5, 2)
        
        # 2. Anel 2 (Principal - Rotativo)
        # Para simular a rotação visualmente (usando um efeito de luz/caminho)
        # Desenha um anel interior para delimitar
        pygame.draw.circle(surface, PURPLE, (CENTER_X, CENTER_Y), self.r_anel2, 40)
        
        # Simulação de Luz/Caminho Rotativo (Visualização)
        for i in range(8):
            angle = math.radians(self.angulo_anel2 + i * (360 / 8))
            x = CENTER_X + int(math.cos(angle) * (self.r_anel2 - 20))
            y = CENTER_Y + int(math.sin(angle) * (self.r_anel2 - 20))
            pygame.draw.circle(surface, (100, 255, 255), (x, y), 8)
            
        # 3. Anel 1 (Estreito - Rotativo)
        pygame.draw.circle(surface, GREEN, (CENTER_X, CENTER_Y), self.r_anel1, 20)
        
        # 4. Núcleo Central (Spawn)
        pygame.draw.circle(surface, RED, (CENTER_X, CENTER_Y), self.r_nucleo, 10)
        
        # 5. Vias Radiais (Simulação)
        # Desenha 4 vias fixas que ligam os anéis
        for i in range(4):
            angle = math.radians(i * 90)
            start_x = CENTER_X + int(math.cos(angle) * self.r_nucleo)
            start_y = CENTER_Y + int(math.sin(angle) * self.r_nucleo)
            end_x = CENTER_X + int(math.cos(angle) * self.r_anel3)
            end_y = CENTER_Y + int(math.sin(angle) * self.r_anel3)
            
            # Desenha a Via (Estrutura)
            pygame.draw.line(surface, WHITE, (start_x, start_y), (end_x, end_y), 5)
            
            # **Lógica de Portões Vilosos:**
            # O código real aqui verificaria se o angulo_anel2 se alinha com o angulo da via
            # para determinar se o jogador pode passar.

# --- 4. Loop Principal do Jogo ---
def game_loop():
    all_sprites = pygame.sprite.Group()
    player = Comilao()
    all_sprites.add(player)

    labirinto = LabirintoRotativo()
    
    running = True
    while running:
        # Gerenciamento de Eventos
        for event in pygame.event.get():
            if event.type == pygame.QUIT:
                running = False
            # Permite fechar a janela com ESC
            if event.type == pygame.KEYDOWN:
                if event.key == pygame.K_ESCAPE:
                    running = False

        # --- Lógica de Jogo ---
        
        # Captura as teclas pressionadas
        keys = pygame.key.get_pressed()
        
        # Atualiza a posição do jogador
        player.update(keys)
        
        # Atualiza a rotação do labirinto
        labirinto.update()
        
        # **Atenção**: Aqui entraria a lógica complexa de colisão e
        # a força de rotação sendo aplicada ao jogador (ex: player.rect.x += force_x)
        
        # --- Desenho ---
        
        # Desenha o labirinto (fundo)
        labirinto.draw_labyrinth(screen)
        
        # Desenha todos os sprites (jogador, fantasmas, pontos)
        all_sprites.draw(screen)
        
        # Atualiza a tela
        pygame.display.flip()
        
        # Define o FPS
        clock.tick(FPS)

    pygame.quit()
    sys.exit()

if __name__ == "__main__":
    game_loop()
```
