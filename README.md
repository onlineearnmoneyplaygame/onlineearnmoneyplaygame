 rt random

# Initialize pygame
pygame.init()

# Screen dimensions
WIDTH, HEIGHT = 800, 600
screen = pygame.display.set_mode((WIDTH, HEIGHT))
pygame.display.set_caption("Bird vs Ball")

# Colors
WHITE = (255, 255, 255)
RED = (255, 0, 0)
BLUE = (0, 0, 255)
BLACK = (0, 0, 0)

# Bird properties
bird_radius = 20
bird_x = 100
bird_y = HEIGHT // 2
bird_speed = 5
bird_jump = -15
bird_gravity = 1
bird_velocity = 0

# Ball properties
ball_radius = 30
ball_x = WIDTH
ball_y = random.randint(ball_radius, HEIGHT - ball_radius)
ball_speed = 7

# Score
score = 0
font = pygame.font.SysFont(None, 36)

# Game loop
clock = pygame.time.Clock()
running = True

while running:
    # Handle events
    for event in pygame.event.get():
        if event.type == pygame.QUIT:
            running = False
        if event.type == pygame.KEYDOWN:
            if event.key == pygame.K_SPACE:
                bird_velocity = bird_jump
    
    # Update bird
    bird_velocity += bird_gravity
    bird_y += bird_velocity
    
    # Keep bird on screen
    if bird_y < bird_radius:
        bird_y = bird_radius
        bird_velocity = 0
    if bird_y > HEIGHT - bird_radius:
        bird_y = HEIGHT - bird_radius
        bird_velocity = 0
    
    # Update ball
    ball_x -= ball_speed
    if ball_x < -ball_radius:
        ball_x = WIDTH + ball_radius
        ball_y = random.randint(ball_radius, HEIGHT - ball_radius)
        score += 1
        ball_speed += 0.5  # Increase difficulty
    
    # Check collision
    distance = ((bird_x - ball_x) ** 2 + (bird_y - ball_y) ** 2) ** 0.5
    if distance < bird_radius + ball_radius:
        running = False
    
    # Draw everything
    screen.fill(BLACK)
    pygame.draw.circle(screen, BLUE, (bird_x, int(bird_y)), bird_radius)
    pygame.draw.circle(screen, RED, (int(ball_x), int(ball_y)), ball_radius)
    
    # Draw score
    score_text = font.render(f"Score: {score}", True, WHITE)
    screen.blit(score_text, (10, 10))
    
    pygame.display.flip()
    clock.tick(60)

# Game over
game_over_text = font.render(f"Game Over! Final Score: {score}", True, WHITE)
screen.blit(game_over_text, (WIDTH//2 - 150, HEIGHT//2))
pygame.display.flip()
pygame.time.wait(3000)

pygame.quit()
sys.exit()
<!DOCTYPE html>
<html>
<head>
    <title>Bird vs Ball</title>
    <style>
        canvas {
            border: 1px solid black;
            display: block;
            margin: 0 auto;
            background-color: #000;
        }
        body {
            text-align: center;
            font-family: Arial, sans-serif;
        }
    </style>
</head>
<body>
    <h1>Bird vs Ball</h1>
    <p>Press SPACE to make the bird fly up</p>
    <canvas id="gameCanvas" width="800" height="600"></canvas>
    <p id="score">Score: 0</p>

    <script>
        const canvas = document.getElementById('gameCanvas');
        const ctx = canvas.getContext('2d');
        const scoreElement = document.getElementById('score');

        // Game variables
        let score = 0;
        let gameOver = false;

        // Bird properties
        const bird = {
            x: 100,
            y: canvas.height / 2,
            radius: 20,
            velocity: 0,
            gravity: 0.5,
            jump: -10,
            color: '#3498db'
        };

        // Ball properties
        const ball = {
            x: canvas.width,
            y: Math.random() * (canvas.height - 60) + 30,
            radius: 30,
            speed: 5,
            color: '#e74c3c'
        };

        // Handle keyboard input
        document.addEventListener('keydown', function(event) {
            if (event.code === 'Space') {
                bird.velocity = bird.jump;
            }
            if (gameOver && event.code === 'Space') {
                resetGame();
            }
        });

        function resetGame() {
            score = 0;
            gameOver = false;
            bird.y = canvas.height / 2;
            bird.velocity = 0;
            ball.x = canvas.width;
            ball.y = Math.random() * (canvas.height - 60) + 30;
            ball.speed = 5;
            scoreElement.textContent = `Score: ${score}`;
            requestAnimationFrame(gameLoop);
        }

        function gameLoop() {
            if (gameOver) return;

            // Clear canvas
            ctx.fillStyle = '#000';
            ctx.fillRect(0, 0, canvas.width, canvas.height);

            // Update bird
            bird.velocity += bird.gravity;
            bird.y += bird.velocity;

            // Keep bird on screen
            if (bird.y < bird.radius) {
                bird.y = bird.radius;
                bird.velocity = 0;
            }
            if (bird.y > canvas.height - bird.radius) {
                bird.y = canvas.height - bird.radius;
                bird.velocity = 0;
            }

            // Update ball
            ball.x -= ball.speed;
            if (ball.x < -ball.radius) {
                ball.x = canvas.width + ball.radius;
                ball.y = Math.random() * (canvas.height - 60) + 30;
                score++;
                ball.speed += 0.3;
                scoreElement.textContent = `Score: ${score}`;
            }

            // Check collision
            const dx = bird.x - ball.x;
            const dy = bird.y - ball.y;
            const distance = Math.sqrt(dx * dx + dy * dy);
            if (distance < bird.radius + ball.radius) {
                gameOver = true;
                ctx.fillStyle = '#fff';
                ctx.font = '36px Arial';
                ctx.fillText(`Game Over! Final Score: ${score}`, canvas.width/2 - 180, canvas.height/2);
                ctx.fillText('Press SPACE to play again', canvas.width/2 - 150, canvas.height/2 + 40);
                return;
            }

            // Draw bird
            ctx.beginPath();
            ctx.arc(bird.x, bird.y, bird.radius, 0, Math.PI * 2);
            ctx.fillStyle = bird.color;
            ctx.fill();
            ctx.closePath();

            // Draw ball
            ctx.beginPath();
            ctx.arc(ball.x, ball.y, ball.radius, 0, Math.PI * 2);
            ctx.fillStyle = ball.color;
            ctx.fill();
            ctx.closePath();

            requestAnimationFrame(gameLoop);
        }

        // Start the game
        resetGame();
    </script>
</body>
</html>- 👋 Hi, I’m @onlineearnmoneyplaygame
- 👀 I’m interested in ...
- 🌱 I’m currently learning ...
- 💞️ I’m looking to collaborate on ...
- 📫 How to reach me ...
- 😄 Pronouns: ...
- ⚡ Fun fact: ...

<!---
onlineearnmoneyplaygame/onlineearnmoneyplaygame is a ✨ special ✨ repository because its `README.md` (this file) appears on your GitHub profile.
You can click the Preview link to take a look at your changes.
--->
