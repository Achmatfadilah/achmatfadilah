# 👋 Hello, I'm Achmatfadilah (Prabu)

<h1 align="center">
  <a href="https://git.io/typing-svg">
    <img src="https://readme-typing-svg.herokuapp.com?font=Fira+Code&weight=700&size=40&duration=2000&pause=1000&color=58A6FF&center=true&vCenter=true&width=700&height=55&lines=Fullstack+Web+Developer;Game+Developer;Open+Source+Enthusiast;Software+Engineer" alt="Typing SVG" />
  </a>
</h1>

---

<p align="center">
  <a href="https://twitter.com/achmatfadilah" target="_blank">
    <img src="https://img.shields.io/badge/twitter-%2300acee?style=for-the-badge&logo=twitter&logoColor=white" />
  </a>
  <a href="https://linkedin.com/in/achmatfadilah" target="_blank">
    <img src="https://img.shields.io/badge/linkedin-%230077b5.svg?style=for-the-badge&logo=linkedin&logoColor=white" />
  </a>
  <a href="https://instagram.com/achmat_dillah" target="_blank">
    <img src="https://img.shields.io/badge/instagram-%23E4405F.svg?style=for-the-badge&logo=instagram&logoColor=white" />
  </a>
  <a href="https://facebook.com/achmatfadilah" target="_blank">
    <img src="https://img.shields.io/badge/facebook-%231877F2.svg?style=for-the-badge&logo=facebook&logoColor=white" />
  </a>
  <a href="mailto:prabudillah30@gmail.com">
    <img src="https://img.shields.io/badge/email-prabudillah30%40gmail.com-D14836?style=for-the-badge&logo=gmail&logoColor=white" />
  </a>
  <a href="https://github.com/achmatfadilah" target="_blank">
    <img src="https://img.shields.io/badge/github-%23181717.svg?style=for-the-badge&logo=github&logoColor=white" />
  </a>
</p>

---

<div align="center">
  <img src="https://komarev.com/ghpvc/?username=achmatfadilah&label=Profile%20Views&color=0e75b6&style=for-the-badge" />
  <img src="https://img.shields.io/github/followers/achmatfadilah?label=Followers&style=for-the-badge&color=181717" />
  <img src="https://img.shields.io/github/stars/achmatfadilah?label=Stars&style=for-the-badge&color=FFD700" />
  <img src="https://img.shields.io/github/repos-closed/achmatfadilah?label=Projects&style=for-the-badge&color=28A745" />
  <img src="https://img.shields.io/github/forks/achmatfadilah?label=Forks&style=for-the-badge&color=FF6B6B" />
</div>

---

## 🎮 MY GAMES SECTION 🎮

<p align="center">
  <img src="https://cultofthepartyparrot.com/parrots/hd/parrot.gif" width="50" />
  <img src="https://cultofthepartyparrot.com/parrots/hd/parrotpartyparrot.gif" width="50" />
  <img src="https://cultofthepartyparrot.com/parrots/hd/partyparrot.gif" width="50" />
  <img src="https://cultofthepartyparrot.com/parrots/hd/middleparrot.gif" width="50" />
  <img src="https://cultofthepartyparrot.com/parrots/hd/coffeeparrot.gif" width="50" />
</p>

---

## 🎯 Game 1: Snake Game (Python - Full Code)

```python
#!/usr/bin/env python3
"""
Snake Game
Created by: Achmatfadilah (Prabu)
Language: Python
Framework: Pygame

HOW TO RUN:
1. Install pygame: pip install pygame
2. Save this code as snake_game.py
3. Run: python snake_game.py

CONTROLS:
- Arrow Keys: Move the snake
- Q: Quit game
- C: Play again (when game over)
"""

import pygame
import time
import random
import sys

# Initialize Pygame
pygame.init()

# Define Colors (RGB format)
WHITE = (255, 255, 255)
YELLOW = (255, 255, 102)
BLACK = (0, 0, 0)
RED = (213, 50, 80)
GREEN = (0, 255, 0)
BLUE = (50, 153, 213)
DARK_GREEN = (0, 200, 0)
ORANGE = (255, 165, 0)
PURPLE = (128, 0, 128)

# Display Dimensions
DIS_WIDTH = 600
DIS_HEIGHT = 400

# Create Display
dis = pygame.display.set_mode((DIS_WIDTH, DIS_HEIGHT))
pygame.display.set_caption('🐍 Snake Game by Achmatfadilah')

# Clock for controlling frame rate
clock = pygame.time.Clock()

# Snake Block Size
SNAKE_BLOCK = 10
SNAKE_SPEED = 15

# Font Styles
font_style = pygame.font.SysFont("bahnschrift", 25)
score_font = pygame.font.SysFont("comicsansms", 35)
title_font = pygame.font.SysFont("comicsansms", 50)

def your_score(score):
    """Display current score"""
    value = score_font.render("Score: " + str(score), True, YELLOW)
    dis.blit(value, [0, 0])

def your_level(level):
    """Display current level"""
    value = score_font.render("Level: " + str(level), True, ORANGE)
    dis.blit(value, [DIS_WIDTH - 150, 0])

def our_snake(snake_block, snake_list):
    """Draw the snake on the screen"""
    for x in snake_list[:-1]:
        pygame.draw.rect(dis, GREEN, [x[0], x[1], snake_block, snake_block])
    # Draw head in different color
    pygame.draw.rect(dis, DARK_GREEN, [snake_list[-1][0], snake_list[-1][1], snake_block, snake_block])

def message(msg, color, y_offset=0):
    """Display message on screen"""
    mesg = font_style.render(msg, True, color)
    text_rect = mesg.get_rect(center=(DIS_WIDTH/2, DIS_HEIGHT/2 + y_offset))
    dis.blit(mesg, text_rect)

def draw_food(x, y, block):
    """Draw food on screen"""
    pygame.draw.rect(dis, RED, [x, y, block, block])

def draw_grid():
    """Draw grid lines on background"""
    for x in range(0, DIS_WIDTH, SNAKE_BLOCK):
        pygame.draw.line(dis, (30, 30, 30), (x, 0), (x, DIS_HEIGHT))
    for y in range(0, DIS_HEIGHT, SNAKE_BLOCK):
        pygame.draw.line(dis, (30, 30, 30), (0, y), (DIS_WIDTH, y))

def gameLoop():
    """Main game loop"""
    game_over = False
    game_close = False
    
    # Starting position
    x1 = DIS_WIDTH / 2
    y1 = DIS_HEIGHT / 2
    
    x1_change = 0
    y1_change = 0
    
    snake_List = []
    Length_of_snake = 1
    level = 1
    score = 0
    
    # Generate first food
    foodx = round(random.randrange(0, DIS_WIDTH - SNAKE_BLOCK) / 10.0) * 10.0
    foody = round(random.randrange(0, DIS_HEIGHT - SNAKE_BLOCK) / 10.0) * 10.0
    
    while not game_over:
        while game_close == True:
            dis.fill(BLACK)
            message("GAME OVER!", RED, -50)
            message("Press C-Play Again or Q-Quit", WHITE, 0)
            your_score(Length_of_snake - 1)
            your_level(level)
            pygame.display.update()
            
            for event in pygame.event.get():
                if event.type == pygame.KEYDOWN:
                    if event.key == pygame.K_q:
                        game_over = True
                        game_close = False
                    if event.key == pygame.K_c:
                        gameLoop()
        
        # Event Handling
        for event in pygame.event.get():
            if event.type == pygame.QUIT:
                game_over = True
            if event.type == pygame.KEYDOWN:
                if event.key == pygame.K_LEFT:
                    x1_change = -SNAKE_BLOCK
                    y1_change = 0
                elif event.key == pygame.K_RIGHT:
                    x1_change = SNAKE_BLOCK
                    y1_change = 0
                elif event.key == pygame.K_UP:
                    y1_change = -SNAKE_BLOCK
                    x1_change = 0
                elif event.key == pygame.K_DOWN:
                    y1_change = SNAKE_BLOCK
                    x1_change = 0
                elif event.key == pygame.K_p:
                    # Pause functionality
                    paused = True
                    while paused:
                        dis.fill(BLACK)
                        message("PAUSED", YELLOW, 0)
                        message("Press C to continue", WHITE, 40)
                        pygame.display.update()
                        for event in pygame.event.get():
                            if event.type == pygame.KEYDOWN:
                                if event.key == pygame.K_c:
                                    paused = False
        
        # Check boundary collision
        if x1 >= DIS_WIDTH or x1 < 0 or y1 >= DIS_HEIGHT or y1 < 0:
            game_close = True
        
        # Update position
        x1 += x1_change
        y1 += y1_change
        
        # Draw background
        dis.fill(BLACK)
        draw_grid()
        
        # Draw food
        draw_food(foodx, foody, SNAKE_BLOCK)
        
        # Update snake
        snake_Head = []
        snake_Head.append(x1)
        snake_Head.append(y1)
        snake_List.append(snake_Head)
        
        if len(snake_List) > Length_of_snake:
            del snake_List[0]
        
        # Check self-collision
        for x in snake_List[:-1]:
            if x == snake_Head:
                game_close = True
        
        # Draw snake
        our_snake(SNAKE_BLOCK, snake_List)
        
        # Display score and level
        your_score(Length_of_snake - 1)
        your_level(level)
        
        pygame.display.update()
        
        # Check food collision
        if x1 == foodx and y1 == foody:
            foodx = round(random.randrange(0, DIS_WIDTH - SNAKE_BLOCK) / 10.0) * 10.0
            foody = round(random.randrange(0, DIS_HEIGHT - SNAKE_BLOCK) / 10.0) * 10.0
            Length_of_snake += 1
            score += 10
            
            # Level up every 50 points
            if score % 50 == 0:
                level += 1
        
        # Speed up as level increases
        current_speed = SNAKE_SPEED + (level - 1) * 2
        clock.tick(current_speed)
    
    pygame.quit()
    quit()

# Start the game
if __name__ == "__main__":
    gameLoop()
```

**📥 Download & Run:**
```bash
# Install pygame
pip install pygame

# Save as snake_game.py and run
python snake_game.py
```

🔗 [View on GitHub](https://github.com/achmatfadilah/snake-game) | ⭐ Star | 🍴 Fork

---

## 🎮 Game 2: Tic-Tac-Toe (HTML + JavaScript - Full Code)

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Tic Tac Toe - Achmatfadilah</title>
    <style>
        * {
            margin: 0;
            padding: 0;
            box-sizing: border-box;
            font-family: 'Segoe UI', Tahoma, Geneva, Verdana, sans-serif;
        }

        body {
            background: linear-gradient(135deg, #1a1a2e 0%, #16213e 100%);
            min-height: 100vh;
            display: flex;
            flex-direction: column;
            align-items: center;
            justify-content: center;
            color: white;
        }

        h1 {
            font-size: 3rem;
            margin-bottom: 20px;
            text-shadow: 2px 2px 4px rgba(0,0,0,0.5);
        }

        .status {
            font-size: 1.5rem;
            margin-bottom: 20px;
            padding: 10px 20px;
            background: rgba(255,255,255,0.1);
            border-radius: 10px;
        }

        .board {
            display: grid;
            grid-template-columns: repeat(3, 100px);
            grid-template-rows: repeat(3, 100px);
            gap: 5px;
            background: #333;
            padding: 5px;
            border-radius: 10px;
            box-shadow: 0 10px 30px rgba(0,0,0,0.5);
        }

        .cell {
            width: 100px;
            height: 100px;
            background: #1a1a2e;
            display: flex;
            align-items: center;
            justify-content: center;
            font-size: 3rem;
            font-weight: bold;
            cursor: pointer;
            transition: all 0.3s ease;
            border-radius: 5px;
        }

        .cell:hover {
            background: #16213e;
            transform: scale(1.05);
        }

        .cell.x {
            color: #00d4ff;
        }

        .cell.o {
            color: #ff6b6b;
        }

        .cell.winner {
            background: #00ff88;
            color: #000;
        }

        .btn-restart {
            margin-top: 30px;
            padding: 15px 40px;
            font-size: 1.2rem;
            background: linear-gradient(135deg, #667eea 0%, #764ba2 100%);
            color: white;
            border: none;
            border-radius: 25px;
            cursor: pointer;
            transition: transform 0.3s ease;
            box-shadow: 0 5px 15px rgba(102, 126, 234, 0.4);
        }

        .btn-restart:hover {
            transform: translateY(-3px);
            box-shadow: 0 8px 20px rgba(102, 126, 234, 0.6);
        }

        .score-board {
            display: flex;
            gap: 40px;
            margin-bottom: 20px;
            font-size: 1.2rem;
        }

        .score {
            padding: 10px 20px;
            background: rgba(255,255,255,0.1);
            border-radius: 10px;
        }

        .score span {
            font-weight: bold;
            font-size: 1.5rem;
        }

        .x-score { color: #00d4ff; }
        .o-score { color: #ff6b6b; }
        .draw-score { color: #ffd700; }
    </style>
</head>
<body>
    <h1>🎮 Tic Tac Toe 🎮</h1>
    <p style="margin-bottom: 15px;">Created by: Achmatfadilah (Prabu)</p>
    
    <div class="score-board">
        <div class="score x-score">X: <span id="xScore">0</span></div>
        <div class="score o-score">O: <span id="oScore">0</span></div>
        <div class="score draw-score">Draw: <span id="drawScore">0</span></div>
    </div>
    
    <div class="status" id="status">Player X's Turn</div>
    
    <div class="board" id="board">
        <div class="cell" data-index="0"></div>
        <div class="cell" data-index="1"></div>
        <div class="cell" data-index="2"></div>
        <div class="cell" data-index="3"></div>
        <div class="cell" data-index="4"></div>
        <div class="cell" data-index="5"></div>
        <div class="cell" data-index="6"></div>
        <div class="cell" data-index="7"></div>
        <div class="cell" data-index="8"></div>
    </div>
    
    <button class="btn-restart" onclick="restartGame()">🔄 Restart Game</button>

    <script>
        // Game State
        let board = ['', '', '', '', '', '', '', '', ''];
        let currentPlayer = 'X';
        let gameActive = true;
        let xWins = 0;
        let oWins = 0;
        let draws = 0;

        // Winning combinations
        const winningConditions = [
            [0, 1, 2], [3, 4, 5], [6, 7, 8],  // Rows
            [0, 3, 6], [1, 4, 7], [2, 5, 8],  // Columns
            [0, 4, 8], [2, 4, 6]               // Diagonals
        ];

        // DOM Elements
        const statusDisplay = document.getElementById('status');
        const cells = document.querySelectorAll('.cell');
        const xScoreEl = document.getElementById('xScore');
        const oScoreEl = document.getElementById('oScore');
        const drawScoreEl = document.getElementById('drawScore');

        // Initialize game
        cells.forEach(cell => {
            cell.addEventListener('click', handleCellClick);
        });

        function handleCellClick(clickedCellEvent) {
            const clickedCell = clickedCellEvent.target;
            const clickedCellIndex = parseInt(clickedCell.getAttribute('data-index'));

            // Check if cell is already filled or game is over
            if (board[clickedCellIndex] !== '' || !gameActive) {
                return;
            }

            // Update board
            board[clickedCellIndex] = currentPlayer;
            clickedCell.textContent = currentPlayer;
            clickedCell.classList.add(currentPlayer.toLowerCase());

            // Check for winner
            checkResult();
        }

        function checkResult() {
            let roundWon = false;
            let winnerCells = [];

            for (let i = 0; i < winningConditions.length; i++) {
                const [a, b, c] = winningConditions[i];
                if (board[a] && board[a] === board[b] && board[a] === board[c]) {
                    roundWon = true;
                    winnerCells = [a, b, c];
                    break;
                }
            }

            if (roundWon) {
                const winner = currentPlayer;
                statusDisplay.textContent = `🎉 Player ${winner} Wins!`;
                statusDisplay.style.background = winner === 'X' ? 'rgba(0, 212, 255, 0.3)' : 'rgba(255, 107, 107, 0.3)';
                
                // Highlight winning cells
                winnerCells.forEach(index => {
                    cells[index].classList.add('winner');
                });

                // Update score
                if (winner === 'X') {
                    xWins++;
                    xScoreEl.textContent = xWins;
                } else {
                    oWins++;
                    oScoreEl.textContent = oWins;
                }

                gameActive = false;
                return;
            }

            // Check for draw
            if (!board.includes('')) {
                statusDisplay.textContent = "🤝 It's a Draw!";
                statusDisplay.style.background = 'rgba(255, 215, 0, 0.3)';
                draws++;
                drawScoreEl.textContent = draws;
                gameActive = false;
                return;
            }

            // Switch player
            currentPlayer = currentPlayer === 'X' ? 'O' : 'X';
            statusDisplay.textContent = `Player ${currentPlayer}'s Turn`;
            statusDisplay.style.background = currentPlayer === 'X' ? 'rgba(0, 212, 255, 0.1)' : 'rgba(255, 107, 107, 0.1)';
        }

        function restartGame() {
            board = ['', '', '', '', '', '', '', '', ''];
            currentPlayer = 'X';
            gameActive = true;
            statusDisplay.textContent = "Player X's Turn";
            statusDisplay.style.background = 'rgba(255,255,255,0.1)';

            cells.forEach(cell => {
                cell.textContent = '';
                cell.classList.remove('x', 'o', 'winner');
            });
        }

        // Keyboard support
        document.addEventListener('keydown', (e) => {
            if (e.key === 'r' || e.key === 'R') {
                restartGame();
            }
        });
    </script>
</body>
</html>
```

**📥 Save & Run:**
```html
<!-- Save as index.html and open in browser -->
<!-- Or run with Python: python -m http.server 8000 -->
```

🔗 [View on GitHub](https://github.com/achmatfadilah/tic-tac-toe) | ⭐ Star | 🍴 Fork

---

## 🎳 Game 3: Pong Game (Python - Full Code)

```python
#!/usr/bin/env python3
"""
Pong Game
Created by: Achmatfadilah (Prabu)
Language: Python
Framework: Pygame

HOW TO RUN:
1. Install pygame: pip install pygame
2. Save this code as pong_game.py
3. Run: python pong_game.py

CONTROLS:
- Player 1 (Right): UP/DOWN arrows
- Player 2 (Left): W/S keys
- Q: Quit game
"""

import pygame
import sys

# Initialize Pygame
pygame.init()

# ============== CONSTANTS ==============
WIDTH, HEIGHT = 800, 600
TITLE = "🏓 Pong Game - Achmatfadilah"
FPS = 60

# Colors (RGB)
BLACK = (0, 0, 0)
WHITE = (255, 255, 255)
RED = (255, 50, 50)
BLUE = (50, 100, 255)
GREEN = (50, 255, 50)
YELLOW = (255, 255, 0)
GRAY = (100, 100, 100)

# Player Settings
PADDLE_WIDTH = 15
PADDLE_HEIGHT = 100
PADDLE_SPEED = 8

# Ball Settings
BALL_SIZE = 15
BALL_SPEED_X = 7
BALL_SPEED_Y = 7

# ============== SETUP ==============
screen = pygame.display.set_mode((WIDTH, HEIGHT))
pygame.display.set_caption(TITLE)
clock = pygame.time.Clock()
font = pygame.font.Font(None, 74)
small_font = pygame.font.Font(None, 36)

# ============== CLASSES ==============

class Paddle:
    def __init__(self, x, y, color):
        self.rect = pygame.Rect(x, y, PADDLE_WIDTH, PADDLE_HEIGHT)
        self.color = color
        self.speed = PADDLE_SPEED
        self.score = 0
    
    def move(self, up=True):
        if up:
            self.rect.y -= self.speed
        else:
            self.rect.y += self.speed
        
        # Keep paddle on screen
        if self.rect.top < 0:
            self.rect.top = 0
        if self.rect.bottom > HEIGHT:
            self.rect.bottom = HEIGHT
    
    def draw(self):
        pygame.draw.rect(screen, self.color, self.rect)
        # Add glow effect
        pygame.draw.rect(screen, GRAY, self.rect, 2)

class Ball:
    def __init__(self):
        self.rect = pygame.Rect(WIDTH//2 - BALL_SIZE//2, HEIGHT//2 - BALL_SIZE//2, BALL_SIZE, BALL_SIZE)
        self.speed_x = BALL_SPEED_X
        self.speed_y = BALL_SPEED_Y
        self.reset()
    
    def move(self):
        self.rect.x += self.speed_x
        self.rect.y += self.speed_y
        
        # Bounce off top and bottom
        if self.rect.top <= 0 or self.rect.bottom >= HEIGHT:
            self.speed_y *= -1
    
    def reset(self):
        self.rect.center = (WIDTH//2, HEIGHT//2)
        # Random direction
        import random
        self.speed_x = BALL_SPEED_X * random.choice([-1, 1])
        self.speed_y = BALL_SPEED_Y * random.choice([-1, 1])
    
    def draw(self):
        pygame.draw.ellipse(screen, WHITE, self.rect)

class Game:
    def __init__(self):
        self.player = Paddle(WIDTH - 30, HEIGHT//2 - PADDLE_HEIGHT//2, BLUE)
        self.opponent = Paddle(15, HEIGHT//2 - PADDLE_HEIGHT//2, RED)
        self.ball = Ball()
        self.winner = None
        self.game_over = False
    
    def update(self):
        if self.game_over:
            return
        
        # Move ball
        self.ball.move()
        
        # Ball collision with paddles
        if self.ball.rect.colliderect(self.player.rect):
            self.ball.speed_x *= -1
            self.ball.rect.right = self.player.rect.left
        
        if self.ball.rect.colliderect(self.opponent.rect):
            self.ball.speed_x *= -1
            self.ball.rect.left = self.opponent.rect.right
        
        # Score
        if self.ball.rect.left <= 0:
            self.player.score += 1
            self.ball.reset()
        
        if self.ball.rect.right >= WIDTH:
            self.opponent.score += 1
            self.ball.reset()
    
    def draw(self):
        # Background
        screen.fill(BLACK)
        
        # Draw center line
        pygame.draw.aaline(screen, GRAY, (WIDTH//2, 0), (WIDTH//2, HEIGHT))
        
        # Draw center circle
        pygame.draw.circle(screen, GRAY, (WIDTH//2, HEIGHT//2), 50, 2)
        
        # Draw paddles and ball
        self.player.draw()
        self.opponent.draw()
        self.ball.draw()
        
        # Draw scores
        player_text = font.render(str(self.player.score), True, BLUE)
        opponent_text = font.render(str(self.opponent.score), True, RED)
        
        screen.blit(player_text, (WIDTH//2 + 20, HEIGHT//2 - 35))
        screen.blit(opponent_text, (WIDTH//2 - 60, HEIGHT//2 - 35))
        
        # Draw game over
        if self.game_over:
            winner_text = f"{self.winner} Wins!"
            text = font.render(winner_text, True, GREEN)
            text_rect = text.get_rect(center=(WIDTH//2, HEIGHT//2 - 50))
            screen.blit(text, text_rect)
            
            restart_text = small_font.render("Press SPACE to restart", True, WHITE)
            restart_rect = restart_text.get_rect(center=(WIDTH//2, HEIGHT//2 + 20))
            screen.blit(restart_text, restart_rect)
    
    def handle_input(self):
        keys = pygame.key.get_pressed()
        
        # Player movement (Arrow keys)
        if keys[pygame.K_UP]:
            self.player.move(up=True)
        if keys[pygame.K_DOWN]:
            self.player.move(up=False)
        
        # Opponent movement (W/S keys)
        if keys[pygame.K_w]:
            self.opponent.move(up=True)
        if keys[pygame.K_s]:
            self.opponent.move(up=False)
        
        # Quit
        if keys[pygame.K_q]:
            pygame.quit()
            sys.exit()
        
        # Restart
        if self.game_over and keys[pygame.K_SPACE]:
            self.__init__()

def main():
    game = Game()
    
    running = True
    while running:
        # Event handling
        for event in pygame.event.get():
            if event.type == pygame.QUIT:
                running = False
            elif event.type == pygame.KEYDOWN:
                if event.key == pygame.K_ESCAPE:
                    running = False
        
        # Update and draw
        game.handle_input()
        game.update()
        game.draw()
        
        pygame.display.flip()
        clock.tick(FPS)
    
    pygame.quit()
    sys.exit()

if __name__ == "__main__":
    main()
```

**📥 Download & Run:**
```bash
pip install pygame
python pong_game.py
```

🔗 [View on GitHub](https://github.com/achmatfadilah/pong-game) | ⭐ Star | 🍴 Fork

---

## 🚀 Game 4: Endless Runner (JavaScript - Full Code)

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Endless Runner - Achmatfadilah</title>
    <style>
        * {
            margin: 0;
            padding: 0;
            box-sizing: border-box;
        }

        body {
            background: linear-gradient(to bottom, #87CEEB, #E0F7FA);
            min-height: 100vh;
            display: flex;
            flex-direction: column;
            align-items: center;
            justify-content: center;
            font-family: 'Arial', sans-serif;
            overflow: hidden;
        }

        h1 {
            color: #333;
            margin-bottom: 20px;
            text-shadow: 2px 2px 4px rgba(0,0,0,0.2);
        }

        #gameContainer {
            position: relative;
            border: 4px solid #333;
            border-radius: 10px;
            overflow: hidden;
            box-shadow: 0 10px 30px rgba(0,0,0,0.3);
        }

        #gameCanvas {
            display: block;
            background: linear-gradient(to bottom, #87CEEB 0%, #90EE90 70%, #228B22 100%);
        }

        #score {
            position: absolute;
            top: 10px;
            left: 10px;
            font-size: 24px;
            font-weight: bold;
            color: #333;
            background: rgba(255,255,255,0.8);
            padding: 5px 15px;
            border-radius: 20px;
        }

        #highScore {
            position: absolute;
            top: 10px;
            right: 10px;
            font-size: 20px;
            font-weight: bold;
            color: #333;
            background: rgba(255,255,255,0.8);
            padding: 5px 15px;
            border-radius: 20px;
        }

        #gameOver {
            position: absolute;
            top: 50%;
            left: 50%;
            transform: translate(-50%, -50%);
            text-align: center;
            background: rgba(0,0,0,0.8);
            color: white;
            padding: 30px 50px;
            border-radius: 20px;
            display: none;
        }

        #gameOver h2 {
            font-size: 40px;
            margin-bottom: 10px;
            color: #ff6b6b;
        }

        #gameOver p {
            font-size: 24px;
            margin-bottom: 20px;
        }

        #restartBtn {
            background: linear-gradient(135deg, #667eea 0%, #764ba2 100%);
            color: white;
            border: none;
            padding: 15px 30px;
            font-size: 18px;
            border-radius: 25px;
            cursor: pointer;
            transition: transform 0.3s;
        }

        #restartBtn:hover {
            transform: scale(1.1);
        }

        #instructions {
            margin-top: 20px;
            color: #666;
            font-size: 18px;
        }

        .key {
            background: #fff;
            padding: 5px 15px;
            border-radius: 5px;
            border: 2px solid #333;
            font-weight: bold;
        }
    </style>
</head>
<body>
    <h1>🏃 Endless Runner 🏃</h1>
    <p style="margin-bottom: 10px;">Created by: Achmatfadilah (Prabu)</p>
    
    <div id="gameContainer">
        <canvas id="gameCanvas" width="800" height="400"></canvas>
        <div id="score">Score: 0</div>
        <div id="highScore">Best: 0</div>
        
        <div id="gameOver">
            <h2>Game Over!</h2>
            <p>Your Score: <span id="finalScore">0</span></p>
            <button id="restartBtn" onclick="restartGame()">🔄 Play Again</button>
        </div>
    </div>
    
    <div id="instructions">
        Press <span class="key">SPACE</span> or <span class="key">UP ARROW</span> to Jump!
    </div>

    <script>
        // ============== GAME VARIABLES ==============
        const canvas = document.getElementById('gameCanvas');
        const ctx = canvas.getContext('2d');
        
        // Game state
        let gameRunning = false;
        let score = 0;
        let highScore = localStorage.getItem('runnerHighScore') || 0;
        let gameSpeed = 5;
        
        // Player (Dino)
        const dino = {
            x: 50,
            y: 300,
            width: 50,
            height: 50,
            dy: 0,
            jumpPower: -15,
            gravity: 0.8,
            grounded: false,
            color: '#4A4A4A'
        };
        
        // Ground
        const ground = {
            y: 350,
            height: 50
        };
        
        // Obstacles
        let obstacles = [];
        let obstacleTimer = 0;
        let minObstacleInterval = 60;
        let maxObstacleInterval = 120;
        
        // Clouds
        let clouds = [];
        
        // ============== INITIALIZE ==============
        document.getElementById('highScore').textContent = `Best: ${highScore}`;
        
        function init() {
            // Initialize clouds
            for (let i = 0; i < 5; i++) {
                clouds.push({
                    x: Math.random() * canvas.width,
                    y: Math.random() * 150 + 20,
                    width: Math.random() * 60 + 40,
                    speed: Math.random() * 0.5 + 0.2
                });
            }
            
            startGame();
        }
        
        function startGame() {
            gameRunning = true;
            score = 0;
            gameSpeed = 5;
            obstacles = [];
            obstacleTimer = 0;
            dino.y = ground.y - dino.height;
            dino.dy = 0;
            
            document.getElementById('gameOver').style.display = 'none';
            document.getElementById('score').textContent = `Score: ${score}`;
            
            gameLoop();
        }
        
        function restartGame() {
            startGame();
        }
        
        // ============== GAME LOOP ==============
        function gameLoop() {
            if (!gameRunning) return;
            
            update();
            draw();
            
            requestAnimationFrame(gameLoop);
        }
        
        // ============== UPDATE ==============
        function update() {
            // Update score
            score++;
            document.getElementById('score').textContent = `Score: ${Math.floor(score / 10)}`;
            
            // Increase game speed gradually
            if (score % 500 === 0) {
                gameSpeed += 0.5;
            }
            
            // Dino physics
            if (!dino.grounded) {
                dino.dy += dino.gravity;
                dino.y += dino.dy;
            }
            
            // Ground collision
            if (dino.y + dino.height >= ground.y) {
                dino.y = ground.y - dino.height;
                dino.dy = 0;
                dino.grounded = true;
            } else {
                dino.grounded = false;
            }
            
            // Spawn obstacles
            obstacleTimer++;
            if (obstacleTimer > Math.random() * (maxObstacleInterval - minObstacleInterval) + minObstacleInterval) {
                spawnObstacle();
                obstacleTimer = 0;
            }
            
            // Update obstacles
            for (let i = obstacles.length - 1; i >= 0; i--) {
                obstacles[i].x -= gameSpeed;
                
                // Remove off-screen obstacles
                if (obstacles[i].x + obstacles[i].width < 0) {
                    obstacles.splice(i, 1);
                    continue;
                }
                
                // Collision detection
                if (checkCollision(dino, obstacles[i])) {
                    gameOver();
                }
            }
            
            // Update clouds
            clouds.forEach(cloud => {
                cloud.x -= cloud.speed;
                if (cloud.x + cloud.width < 0) {
                    cloud.x = canvas.width;
                    cloud.y = Math.random() * 150 + 20;
                }
            });
        }
        
        // ============== DRAW ==============
        function draw() {
            // Clear canvas
            ctx.clearRect(0, 0, canvas.width, canvas.height);
            
            // Draw sky gradient
            const gradient = ctx.createLinearGradient(0, 0, 0, canvas.height);
            gradient.addColorStop(0, '#87CEEB');
            gradient.addColorStop(0.7, '#E0F7FA');
            gradient.addColorStop(1, '#90EE90');
            ctx.fillStyle = gradient;
            ctx.fillRect(0, 0, canvas.width, canvas.height);
            
            // Draw clouds
            ctx.fillStyle = 'rgba(255, 255, 255, 0.8)';
            clouds.forEach(cloud => {
                drawCloud(cloud.x, cloud.y, cloud.width);
            });
            
            // Draw ground
            ctx.fillStyle = '#228B22';
            ctx.fillRect(0, ground.y, canvas.width, ground.height);
            
            // Draw ground line
            ctx.strokeStyle = '#1a6b1a';
            ctx.lineWidth = 3;
            ctx.beginPath();
            ctx.moveTo(0, ground.y);
            ctx.lineTo(canvas.width, ground.y);
            ctx.stroke();
            
            // Draw dino
            drawDino(dino.x, dino.y, dino.width, dino.height);
            
            // Draw obstacles
            obstacles.forEach(obs => {
                drawObstacle(obs.x, obs.y, obs.width, obs.height, obs.type);
            });
        }
        
        // ============== DRAWING HELPERS ==============
        function drawDino(x, y, w, h) {
            ctx.fillStyle = dino.color;
            
            // Body
            ctx.fillRect(x + 5, y + 15, w - 10, h - 20);
            
            // Head
            ctx.fillRect(x + 20, y, 30, 20);
            
            // Eye
            ctx.fillStyle = 'white';
            ctx.fillRect(x + 35, y + 5, 8, 8);
            ctx.fillStyle = 'black';
            ctx.fillRect(x + 37, y + 7, 4, 4);
            
            // Legs
            ctx.fillStyle = dino.color;
            if (dino.grounded && Math.floor(Date.now() / 100) % 2 === 0) {
                ctx.fillRect(x + 10, y + h - 10, 8, 10);
                ctx.fillRect(x + 32, y + h - 10, 8, 10);
            } else {
                ctx.fillRect(x + 10, y + h - 15, 8, 15);
                ctx.fillRect(x + 32, y + h - 15, 8, 15);
            }
            
            // Tail
            ctx.fillRect(x, y + 20, 10, 8);
        }
        
        function drawCloud(x, y, w) {
            ctx.beginPath();
            ctx.arc(x, y, w/3, 0, Math.PI * 2);
            ctx.arc(x + w/3, y - w/6, w/4, 0, Math.PI * 2);
            ctx.arc(x + w*2/3, y, w/3, 0, Math.PI * 2);
            ctx.fill();
        }
        
        function drawObstacle(x, y, w, h, type) {
            if (type === 'cactus') {
                // Cactus
                ctx.fillStyle = '#228B22';
                ctx.fillRect(x + w/3, y, w/3, h);
                ctx.fillRect(x, y + h/3, w, h/3);
                ctx.fillRect(x, y + h/2, w/4, h/2);
                ctx.fillRect(x + w*3/4, y + h/2, w/4, h/2);
            } else {
                // Bird
                ctx.fillStyle = '#FF6B6B';
                ctx.fillRect(x, y + h/3, w, h/3);
                // Wings
                ctx.fillRect(x + w/4, y, w/2, h/3);
                ctx.fillRect(x + w/4, y + h*2/3, w/2, h/3);
            }
        }
        
        function spawnObstacle() {
            const type = Math.random() > 0.7 ? 'bird' : 'cactus';
            const height = type === 'bird' ? 40 : 50;
            
            obstacles.push({
                x: canvas.width,
                y: type === 'bird' ? ground.y - 80 - Math.random() * 50 : ground.y - height,
                width: type === 'bird' ? 50 : 30,
                height: height,
                type: type
            });
        }
        
        function checkCollision(rect1, rect2) {
            return rect1.x < rect2.x + rect2.width &&
                   rect1.x + rect1.width > rect2.x &&
                   rect1.y < rect2.y + rect2.height &&
                   rect1.y + rect1.height > rect2.y;
        }
        
        function gameOver() {
            gameRunning = false;
            
            // Update high score
            const finalScore = Math.floor(score / 10);
            if (finalScore > highScore) {
                highScore = finalScore;
                localStorage.setItem('runnerHighScore', highScore);
                document.getElementById('highScore').textContent = `Best: ${highScore}`;
            }
            
            document.getElementById('finalScore').textContent = finalScore;
            document.getElementById('gameOver').style.display = 'block';
        }
        
        // ============== INPUT HANDLING ==============
        document.addEventListener('keydown', (e) => {
            if (e.code === 'Space' || e.code === 'ArrowUp') {
                e.preventDefault();
                if (dino.grounded && gameRunning) {
                    dino.dy = dino.jumpPower;
                    dino.grounded = false;
                } else if (!gameRunning) {
                    restartGame();
                }
            }
        });
        
        // Touch support for mobile
        canvas.addEventListener('touchstart', (e) => {
            e.preventDefault();
            if (dino.grounded && gameRunning) {
                dino.dy = dino.jumpPower;
                dino.grounded = false;
            }
        });
        
        // Start the game
        init();
    </script>
</body>
</html>
```

**📥 Save & Run:**
```html
<!-- Save as runner.html and open in any browser -->
```

🔗 [View on GitHub](https://github.com/achmatfadilah/endless-runner) | ⭐ Star | 🍴 Fork

---

## 🃏 Game 5: Rock Paper Scissors (Python CLI - Full Code)

```python
#!/usr/bin/env python3
"""
Rock Paper Scissors Game
Created by: Achmatfadilah (Prabu)
Language: Python

HOW TO RUN:
1. Save as rps_game.py
2. Run: python rps_game.py

FEATURES:
- Player vs Computer
- Score tracking
- Multiple rounds
- Visual ASCII art
- Game statistics
"""

import random
import time
import os

# ============== CONSTANTS ==============
CHOICES = ['rock', 'paper', 'scissors']
EMOJI = {
    'rock': '🪨',
    'paper': '📄',
    'scissors': '✂️'
}

ASCII_ART = {
    'rock': '''
    _________
---'   ____)
      (_____)
      (_____)
      (____)
---.__(___)
''',
    'paper': '''
    _________
---'   _____)____
          ______)
          _______)
         _______)
---.__________)
''',
    'scissors': '''
    _________
---'   ____)____
          ______)
       __________)
      (____)
---.__(___)
'''
}

# ============== FUNCTIONS ==============

def clear_screen():
    """Clear the terminal screen"""
    os.system('cls' if os.name == 'nt' else 'clear')

def print_header():
    """Print game header"""
    print("\n" + "="*50)
    print("🪨 📄 ✂️ ROCK PAPER SCISSORS ✂️ 📄 🪨")
    print("="*50)
    print("Created by: Achmatfadilah (Prabu)")
    print("="*50 + "\n")

def print_choice_art(choice):
    """Print ASCII art for the choice"""
    print(ASCII_ART.get(choice, ''))

def get_player_choice():
    """Get and validate player's choice"""
    while True:
        print("\nYour options:")
        print("  🪨 [R]ock")
        print("  📄 [P]aper")
        print("  ✂️ [S]cissors")
        print("  🚪 [Q]uit")
        
        choice = input("\nEnter your choice: ").lower().strip()
        
        if choice in ['r', 'rock']:
            return 'rock'
        elif choice in ['p', 'paper']:
            return 'paper'
        elif choice in ['s', 'scissors']:
            return 'scissors'
        elif choice in ['q', 'quit', 'exit']:
            return 'quit'
        else:
            print("❌ Invalid choice! Please try again.")

def get_computer_choice():
    """Get random computer choice"""
    return random.choice(CHOICES)

def determine_winner(player, computer):
    """Determine the winner of the round"""
    if player == computer:
        return 'tie'
    elif (player == 'rock' and computer == 'scissors') or \
         (player == 'paper' and computer == 'rock') or \
         (player == 'scissors' and computer == 'paper'):
        return 'player'
    else:
        return 'computer'

def print_round_result(player, computer, winner):
    """Print the result of a round"""
    print("\n" + "-"*40)
    print("Your choice:")
    print_choice_art(player)
    print(f"{EMOJI[player]} You chose {player.upper()}")
    
    print("\nComputer chose:")
    print_choice_art(computer)
    print(f"{EMOJI[computer]} Computer chose {computer.upper()}")
    
    print("-"*40)
    
    if winner == 'player':
        print("🎉 YOU WIN THIS ROUND! 🎉")
    elif winner == 'computer':
        print("💻 Computer wins this round!")
    else:
        print("🤝 It's a TIE!")

def print_score(player_score, computer_score, ties):
    """Print current score"""
    print("\n" + "="*40)
    print("📊 SCORE BOARD")
    print("="*40)
    print(f"  🧑 You:     {player_score}")
    print(f"  💻 Computer: {computer_score}")
    print(f"  🤝 Ties:    {ties}")
    print("="*40)

def print_statistics(player_score, computer_score, ties, rounds):
    """Print final statistics"""
    total = rounds
    if total == 0:
        total = 1
    
    player_percent = (player_score / total) * 100
    computer_percent = (computer_score / total) * 100
    tie_percent = (ties / total) * 100
    
    print("\n" + "="*40)
    print("📈 FINAL STATISTICS")
    print("="*40)
    print(f"  Total Rounds: {rounds}")
    print(f"  🧑 Win Rate:  {player_percent:.1f}%")
    print(f"  💻 Lose Rate: {computer_percent:.1f}%")
    print(f"  🤝 Tie Rate:  {tie_percent:.1f}%")
    print("="*40)
    
    if player_score > computer_score:
        print("\n🏆 CONGRATULATIONS! YOU WON THE GAME! 🏆")
    elif player_score < computer_score:
        print("\n😢 Better luck next time!")
    else:
        print("\n🤝 It's a DRAW game!")

def play_again():
    """Ask if player wants to play again"""
    while True:
        choice = input("\nPlay again? (Y/N): ").lower().strip()
        if choice in ['y', 'yes']:
            return True
        elif choice in ['n', 'no']:
            return False
        else:
            print("Please enter Y or N")

def main():
    """Main game function"""
    player_score = 0
    computer_score = 0
    ties = 0
    rounds = 0
    
    while True:
        clear_screen()
        print_header()
        
        # Get player's choice
        player_choice = get_player_choice()
        
        if player_choice == 'quit':
            print("\n👋 Thanks for playing!")
            break
        
        # Get computer's choice
        print("\nComputer is thinking")
        for i in range(3):
            print(".", end=" ", flush=True)
            time.sleep(0.5)
        print()
        
        computer_choice = get_computer_choice()
        
        # Determine winner
        winner = determine_winner(player_choice, computer_choice)
        
        # Update scores
        if winner == 'player':
            player_score += 1
        elif winner == 'computer':
            computer_score += 1
        else:
            ties += 1
        rounds += 1
        
        # Print result
        print_round_result(player_choice, computer_choice, winner)
        print_score(player_score, computer_score, ties)
        
        # Ask to continue
        if not play_again():
            break
    
    # Print final statistics
    clear_screen()
    print_header()
    print_statistics(player_score, computer_score, ties, rounds)
    print("\n👋 Thanks for playing Rock Paper Scissors!")
    print("Created by: Achmatfadilah (Prabu)")

if __name__ == "__main__":
    try:
        main()
    except KeyboardInterrupt:
        print("\n\n👋 Game interrupted. Thanks for playing!")
```

**📥 Download & Run:**
```bash
python rps_game.py
```

🔗 [View on GitHub](https://github.com/achmatfadilah/rock-paper-scissors) | ⭐ Star | 🍴 Fork

---

## 🐍 Snake Animation

<p align="center">
  <img src="https://raw.githubusercontent.com/achmatfadilah/achmatfadilah/output/github-contribution-grid-snake.svg" alt="snake" />
</p>

---

## 📊 GitHub Stats

<p align="center">
  <img src="https://github-readme-stats.vercel.app/api?username=achmatfadilah&show_icons=true&theme=radical&hide_border=true&bg_color=0d1117&count_private=true" />
</p>

<p align="center">
  <img src="https://github-readme-stats.vercel.app/api/top-langs/?username=achmatfadilah&layout=donut&theme=radical&hide_border=true&bg_color=0d1117" />
</p>

---

## 📈 GitHub Activity

<img src="https://github-readme-activity-graph.vercel.app/graph?username=achmatfadilah&theme=react-dark&hide_border=true&bg_color=0d1117&color=58A6FF" />

---

## 🖥️ About Me

Hello! I'm **Achmatfadilah** (also known as **Prabu**), a passionate **Fullstack Web Developer** and **Game Developer** based in Indonesia 🇮🇩

I specialize in building modern web applications and creating fun, interactive games using Python, JavaScript, and various game development frameworks.

### 🎯 What I Do
- 🌐 Build responsive websites and web applications
- 🎮 Create browser-based games (HTML5, JavaScript)
- 🐍 Develop Python games (Pygame)
- 🔧 Backend development with Node.js, Python
- ☁️ Deploy applications to cloud platforms

### 📚 Skills

**Programming Languages:**
- Python 🐍
- JavaScript 📜
- TypeScript 📘
- HTML/CSS 🎨

**Frameworks:**
- React, Next.js ⚛️
- Node.js 🟢
- Django, FastAPI 🐍
- Pygame 🎮

**Databases:**
- PostgreSQL 🐘
- MongoDB 🍃
- Redis ⚡

**Tools:**
- Git, GitHub 📦
- Docker 🐳
- AWS, Vercel ☁️

### ⚡ Fun Facts
- ☕ Coffee lover (3 cups/day)
- 🌙 Night owl coder
- 🎮 Gaming enthusiast
- 💡 Open source contributor
- 📖 Always learning new things

### 🎯 Goals 2026
- Launch SaaS product
- Create 5+ indie games
- Contribute to 10+ open source projects
- Build developer community in Indonesia
- Get AWS Solutions Architect certified

---

## 🌟 My Repositories

<p align="center">
  <a href="https://github.com/achmatfadilah/snake-game">
    <img src="https://github-readme-stats.vercel.app/api/pin/?username=achmatfadilah&repo=snake-game&theme=radical&bg_color=0d1117&hide_border=true" />
  </a>
  <a href="https://github.com/achmatfadilah/tic-tac-toe">
    <img src="https://github-readme-stats.vercel.app/api/pin/?username=achmatfadilah&repo=tic-tac-toe&theme=radical&bg_color=0d1117&hide_border=true" />
  </a>
  <a href="https://github.com/achmatfadilah/pong-game">
    <img src="https://github-readme-stats.vercel.app/api/pin/?username=achmatfadilah&repo=pong-game&theme=radical&bg_color=0d1117&hide_border=true" />
  </a>
</p>

---

## 📬 Contact Me

<p align="center">
  <a href="mailto:prabudillah30@gmail.com">
    <img src="https://img.shields.io/badge/Email-prabudillah30%40gmail.com-D14836?style=for-the-badge&logo=gmail&logoColor=white" />
  </a>
  <a href="https://linkedin.com/in/achmatfadilah" target="_blank">
    <img src="https://img.shields.io/badge/LinkedIn-Connect-0077B5?style=for-the-badge&logo=linkedin&logoColor=white" />
  </a>
  <a href="https://instagram.com/achmat_dillah" target="_blank">
    <img src="https://img.shields.io/badge/Instagram-Follow-E4405F?style=for-the-badge&logo=instagram&logoColor=white" />
  </a>
  <a href="https://facebook.com/achmatfadilah" target="_blank">
    <img src="https://img.shields.io/badge/Facebook-Follow-1877F2?style=for-the-badge&logo=facebook&logoColor=white" />
  </a>
  <a href="https://github.com/achmatfadilah" target="_blank">
    <img src="https://img.shields.io/badge/GitHub-Follow-181717?style=for-the-badge&logo=github&logoColor=white" />
  </a>
</p>

---

## 💖 Support Me

<p align="center">
  <a href="https://www.buymeacoffee.com/achmatfadilah" target="_blank">
    <img src="https://cdn.buymeacoffee.com/buttons/v2/default-yellow.png" width="180" alt="Buy Me A Coffee" />
  </a>
</p>

---

## 🎉 Thank You!

<p align="center">
  <img src="https://capsule-render.vercel.app/api?type=waving&color=gradient&height=80&section=footer" width="100%" />
</p>

<p align="center">
  <sub>⭐ Thanks for visiting! Let's build amazing things together.</sub>
</p>

<p align="center">
  <sub><strong>Made with ❤️ by Achmatfadilah (Prabu)</strong></sub>
</p>
