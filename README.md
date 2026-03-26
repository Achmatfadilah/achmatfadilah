# 👋 Hello, I'm Achmatfadilah (Prabu)

<h1 align="center">
  <a href="https://git.io/typing-svg">
    <img src="https://readme-typing-svg.herokuapp.com?font=Fira+Code&weight=700&size=40&duration=2000&pause=1000&color=58A6FF&center=true&vCenter=true&width=650&height=55&lines=Fullstack+Web+Developer;Game+Developer;Open+Source+Enthusiast;Coffee+Addicted+Coder" alt="Typing SVG" />
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
    <img src="https://img.shields.io/badge/gmail-%23D14836.svg?style=for-the-badge&logo=gmail&logoColor=white" />
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
</div>

---

## 🎮 SIMPLE GAMES I'VE BUILT 🎮

<p align="center">
  <img src="https://cultofthepartyparrot.com/parrots/hd/parrot.gif" width="50" />
  <img src="https://cultofthepartyparrot.com/parrots/hd/parrotpartyparrot.gif" width="50" />
  <img src="https://cultofthepartyparrot.com/parrots/hd/partyparrot.gif" width="50" />
</p>

---

### 🎯 Game 1: Snake Game (Python)

```python
import pygame
import time
import random

pygame.init()

# Colors
WHITE = (255, 255, 255)
YELLOW = (255, 255, 102)
BLACK = (0, 0, 0)
RED = (213, 50, 80)
GREEN = (0, 255, 0)
BLUE = (50, 153, 213)

# Display
dis_width = 600
dis_height = 400
dis = pygame.display.set_mode((dis_width, dis_height))
pygame.display.set_caption('Snake Game by Achmatfadilah')

clock = pygame.time.Clock()
snake_block = 10
snake_speed = 15

# Fonts
font_style = pygame.font.SysFont("bahnschrift", 25)
score_font = pygame.font.SysFont("comicsansms", 35)

def your_score(score):
    value = score_font.render("Score: " + str(score), True, YELLOW)
    dis.blit(value, [0, 0])

def our_snake(snake_block, snake_list):
    for x in snake_list:
        pygame.draw.rect(dis, GREEN, [x[0], x[1], snake_block, snake_block])

def message(msg, color):
    mesg = font_style.render(msg, True, color)
    dis.blit(mesg, [dis_width/6, dis_height/3])

def gameLoop():
    game_over = False
    game_close = False
    x1 = dis_width/2
    y1 = dis_height/2
    x1_change = 0
    y1_change = 0
    snake_List = []
    Length_of_snake = 1
    foodx = round(random.randrange(0, dis_width - snake_block) / 10.0) * 10.0
    foody = round(random.randrange(0, dis_height - snake_block) / 10.0) * 10.0

    while not game_over:
        while game_close == True:
            dis.fill(BLACK)
            message("You Lost! Press C-Play Again or Q-Quit", RED)
            your_score(Length_of_snake - 1)
            pygame.display.update()
            for event in pygame.event.get():
                if event.type == pygame.KEYDOWN:
                    if event.key == pygame.K_q:
                        game_over = True
                        game_close = False
                    if event.key == pygame.K_c:
                        gameLoop()

        for event in pygame.event.get():
            if event.type == pygame.QUIT:
                game_over = True
            if event.type == pygame.KEYDOWN:
                if event.key == pygame.K_LEFT:
                    x1_change = -snake_block
                    y1_change = 0
                elif event.key == pygame.K_RIGHT:
                    x1_change = snake_block
                    y1_change = 0
                elif event.key == pygame.K_UP:
                    y1_change = -snake_block
                    x1_change = 0
                elif event.key == pygame.K_DOWN:
                    y1_change = snake_block
                    x1_change = 0

        if x1 >= dis_width or x1 < 0 or y1 >= dis_height or y1 < 0:
            game_close = True
        x1 += x1_change
        y1 += y1_change
        dis.fill(BLACK)
        pygame.draw.rect(dis, BLUE, [foodx, foody, snake_block, snake_block])
        snake_Head = []
        snake_Head.append(x1)
        snake_Head.append(y1)
        snake_List.append(snake_Head)
        if len(snake_List) > Length_of_snake:
            del snake_List[0]
        
        our_snake(snake_block, snake_List)
        your_score(Length_of_snake - 1)
        pygame.display.update()
        
        if x1 == foodx and y1 == foody:
            foodx = round(random.randrange(0, dis_width - snake_block) / 10.0) * 10.0
            foody = round(random.randrange(0, dis_height - snake_block) / 10.0) * 10.0
            Length_of_snake += 1
        
        clock.tick(snake_speed)

    pygame.quit()
    quit()

gameLoop()
```

🔗 [View Full Code](https://github.com/achmatfadilah/snake-game) | ⭐ Star this project

---

### 🎮 Game 2: Tic-Tac-Toe (JavaScript)

```javascript
const board = ['', '', '', '', '', '', '', '', ''];
let currentPlayer = 'X';
let gameActive = true;

const winningConditions = [
    [0, 1, 2], [3, 4, 5], [6, 7, 8], // Rows
    [0, 3, 6], [1, 4, 7], [2, 5, 8], // Columns
    [0, 4, 8], [2, 4, 6]             // Diagonals
];

function handleCellClick(clickedCellEvent) {
    const clickedCell = clickedCellEvent.target;
    const clickedCellIndex = parseInt(clickedCell.getAttribute('data-cell-index'));

    if (board[clickedCellIndex] !== '' || !gameActive) {
        return;
    }

    board[clickedCellIndex] = currentPlayer;
    clickedCell.innerHTML = currentPlayer;
    checkResult();
}

function checkResult() {
    let roundWon = false;
    for (let i = 0; i < winningConditions.length; i++) {
        const [a, b, c] = winningConditions[i];
        if (board[a] && board[a] === board[b] && board[a] === board[c]) {
            roundWon = true;
            break;
        }
    }

    if (roundWon) {
        alert(`Player ${currentPlayer} wins!`);
        gameActive = false;
        return;
    }

    if (!board.includes('')) {
        alert('Draw!');
        gameActive = false;
        return;
    }

    currentPlayer = currentPlayer === 'X' ? 'O' : 'X';
}

document.querySelectorAll('.cell').forEach(cell => 
    cell.addEventListener('click', handleCellClick));
```

🔗 [View Full Code](https://github.com/achmatfadilah/tic-tac-toe) | ⭐ Star this project

---

### 🏀 Game 3: Pong Game (Python)

```python
import pygame
import sys

# Initialize
pygame.init()

# Colors
BLACK = (0, 0, 0)
WHITE = (255, 255, 255)

# Screen
WIDTH, HEIGHT = 800, 600
screen = pygame.display.set_mode((WIDTH, HEIGHT))
pygame.display.set_caption("Pong Game by Achmatfadilah")

# Paddles
player = pygame.Rect(WIDTH-20, HEIGHT//2-50, 10, 100)
opponent = pygame.Rect(10, HEIGHT//2-50, 10, 100)
ball = pygame.Rect(WIDTH//2-10, HEIGHT//2-10, 20, 20)

ball_speed_x = 7
ball_speed_y = 7
player_speed = 0
opponent_speed = 0

# Game Loop
while True:
    for event in pygame.event.get():
        if event.type == pygame.QUIT:
            pygame.quit()
            sys.exit()
        
        if event.type == pygame.KEYDOWN:
            if event.key == pygame.K_UP:
                player_speed = -6
            if event.key == pygame.K_DOWN:
                player_speed = 6
        
        if event.type == pygame.KEYUP:
            if event.key in [pygame.K_UP, pygame.K_DOWN]:
                player_speed = 0

    # Ball Movement
    ball.x += ball_speed_x
    ball.y += ball_speed_y

    if ball.top <= 0 or ball.bottom >= HEIGHT:
        ball_speed_y *= -1
    
    if ball.left <= 0 or ball.right >= WIDTH:
        ball_speed_x *= -1

    # Paddle Movement
    player.y += player_speed
    
    # Collision
    if ball.colliderect(player) or ball.colliderect(opponent):
        ball_speed_x *= -1

    screen.fill(BLACK)
    pygame.draw.rect(screen, WHITE, player)
    pygame.draw.rect(screen, WHITE, opponent)
    pygame.draw.ellipse(screen, WHITE, ball)
    pygame.draw.aaline(screen, WHITE, (WIDTH//2, 0), (WIDTH//2, HEIGHT))
    
    pygame.display.update()
```

🔗 [View Full Code](https://github.com/achmatfadilah/pong-game) | ⭐ Star this project

---

### 🏃 Game 4: Endless Runner (JavaScript)

```javascript
const canvas = document.getElementById('gameCanvas');
const ctx = canvas.getContext('2d');

let dino = { x: 50, y: 150, width: 40, height: 40, dy: 0, jumpPower: -15 };
let obstacles = [];
let score = 0;
let gameSpeed = 5;
let isGameOver = false;

function draw() {
    ctx.clearRect(0, 0, canvas.width, canvas.height);
    
    // Draw Dino
    ctx.fillStyle = '#555';
    ctx.fillRect(dino.x, dino.y, dino.width, dino.height);
    
    // Draw Ground
    ctx.fillStyle = '#333';
    ctx.fillRect(0, 190, canvas.width, 10);
    
    // Draw Obstacles
    ctx.fillStyle = '#ff5722';
    obstacles.forEach(obs => {
        ctx.fillRect(obs.x, obs.y, obs.width, obs.height);
    });
    
    // Draw Score
    ctx.fillStyle = '#333';
    ctx.font = '20px Arial';
    ctx.fillText('Score: ' + score, 10, 30);
}

function update() {
    if (isGameOver) return;
    
    // Jump physics
    dino.dy += 0.8;
    dino.y += dino.dy;
    
    if (dino.y > 150) {
        dino.y = 150;
        dino.dy = 0;
    }
    
    // Move obstacles
    obstacles.forEach((obs, index) => {
        obs.x -= gameSpeed;
        if (obs.x < -obs.width) {
            obstacles.splice(index, 1);
            score++;
        }
    });
    
    // Collision detection
    obstacles.forEach(obs => {
        if (dino.x < obs.x + obs.width &&
            dino.x + dino.width > obs.x &&
            dino.y < obs.y + obs.height &&
            dino.y + dino.height > obs.y) {
            isGameOver = true;
            alert('Game Over! Score: ' + score);
        }
    });
    
    // Spawn obstacles
    if (Math.random() < 0.02) {
        obstacles.push({
            x: canvas.width,
            y: 160,
            width: 20,
            height: 30
        });
    }
    
    draw();
    requestAnimationFrame(update);
}

function jump() {
    if (dino.y === 150) {
        dino.dy = dino.jumpPower;
    }
}

document.addEventListener('keydown', jump);
update();
```

🔗 [View Full Code](https://github.com/achmatfadilah/endless-runner) | ⭐ Star this project

---

### 🃏 Game 5: Rock Paper Scissors (Python)

```python
import random

def play_game():
    choices = ['rock', 'paper', 'scissors']
    user_score = 0
    com_score = 0
    
    print("🪨📄✂️ ROCK PAPER SCISSORS 🪨📄✂️")
    print("By: Achmatfadilah")
    
    while True:
        user_choice = input("\nEnter rock/paper/scissors (or 'quit'): ").lower()
        
        if user_choice == 'quit':
            print(f"\nFinal Score - You: {user_score}, Computer: {com_score}")
            break
        
        if user_choice not in choices:
            print("Invalid choice! Try again.")
            continue
        
        com_choice = random.choice(choices)
        
        print(f"\nYou chose: {user_choice}")
        print(f"Computer chose: {com_choice}")
        
        if user_choice == com_choice:
            print("🤝 It's a tie!")
        elif (user_choice == 'rock' and com_choice == 'scissors') or \
             (user_choice == 'paper' and com_choice == 'rock') or \
             (user_choice == 'scissors' and com_choice == 'paper'):
            print("🎉 You win!")
            user_score += 1
        else:
            print("💻 Computer wins!")
            com_score += 1
        
        print(f"Score - You: {user_score}, Computer: {com_score}")

if __name__ == "__main__":
    play_game()
```

🔗 [View Full Code](https://github.com/achmatfadilah/rock-paper-scissors) | ⭐ Star this project

---

## 🎮 My Game Projects

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

## 🐍 Snake Animation

<p align="center">
  <img src="https://raw.githubusercontent.com/achmatfadilah/achmatfadilah/output/github-contribution-grid-snake.svg" alt="snake" />
</p>

---

## 🖥️ About Me

Hello! I'm **Achmatfadilah** (also known as **Prabu**), a passionate **Fullstack Web Developer** and **Game Developer** based in Indonesia 🇮🇩

I create modern web applications and fun simple games using Python, JavaScript, and other technologies.

### 🎯 What I Do
- 🌐 Build responsive websites
- 🎮 Create browser-based games
- 🔧 Backend development
- ☁️ Deploy applications

### ⚡ Fun Facts
- ☕ Coffee lover
- 🎮 Gaming enthusiast
- 💡 Love coding simple games
- 🌙 Night owl coder

---

## 🛠️ Tech Stack

<p>
  <img src="https://skillicons.dev/icons?i=python,javascript,typescript,react,nodejs,fastapi&theme=dark" />
</p>

---

## 📊 GitHub Stats

<p align="center">
  <img src="https://github-readme-stats.vercel.app/api?username=achmatfadilah&show_icons=true&theme=radical&hide_border=true&bg_color=0d1117" />
</p>

---

## 📬 Contact

- 📧 Email: prabudillah30@gmail.com
- 📱 Instagram: @achmat_dillah
- 📘 Facebook: achmatfadilah

---

## 🙏 Thank You!

<p align="center">
  <img src="https://capsule-render.vercel.app/api?type=waving&color=gradient&height=80&section=footer" width="100%" />
</p>

<p align="center">
  <sub>⭐ Made with ❤️ by Achmatfadilah (Prabu)</sub>
</p>

