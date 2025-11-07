# 🦆 Goose Migration Game - Web Version

A fun browser-based game simulating goose lifecycle, breeding, and survival against predators!

## 🎮 Features

- **Full Lifecycle System**: Eggs → Goslings → Adult Geese
- **Smart Predator AI**: Foxes and eagles hunt your flock
- **Breeding Mechanics**: Males + females automatically produce eggs
- **Interactive Hiding**: Click geese to make them hide in bushes
- **Environmental Features**: Ponds and bushes provide safety
- **Real-time Scoring**: Earn points as goslings mature

## 🚀 Quick Start

### Prerequisites
- Python 3.7+ (check with `python --version`)
- That's it!

### Installation & Running

```bash
# 1. Navigate to project folder
cd GooseGameWeb

# 2. Install dependencies
pip install -r requirements.txt

# 3. Run the game!
python app.py

# 4. Open your browser to:
#    http://localhost:5000
```

That's it! The game should be running in your browser! 🎉

## 🎯 How to Play

1. **Goal**: Keep your goose flock alive as long as possible
2. **Click geese** to make them hide in bushes (safe for 3 seconds)
3. **Watch them breed** - eggs appear automatically
4. **Avoid predators** - foxes and eagles will hunt your flock
5. **Earn points** - 10 points each time a gosling matures

## 📁 Project Structure

```
GooseGameWeb/
├── app.py                  # Flask server
├── requirements.txt        # Python dependencies
├── templates/
│   └── index.html         # Main game page
└── static/
    ├── css/
    │   └── style.css      # Styling
    └── js/
        └── game.js        # Game engine (all the logic!)
```

## 🛠️ Tech Stack

**Backend:**
- Python 3
- Flask (lightweight web framework)

**Frontend:**
- HTML5 Canvas for rendering
- Vanilla JavaScript (no frameworks!)
- CSS3 for styling

## 🎨 Game Architecture

### Classes (in JavaScript)

1. **Goose** - Manages goose state, movement, and rendering
   - States: EGG, GOSLING, ADULT
   - Movement AI: Goslings follow parents, adults wander
   
2. **Predator** - AI-controlled hunters
   - Types: FOX, EAGLE
   - Hunting behavior: Chase nearby visible geese
   
3. **Pond** - Safe water areas
   
4. **Bush** - Hiding spots for geese
   
5. **Game** - Main game controller
   - Game loop at 60 FPS
   - Collision detection
   - Breeding system
   - Score tracking

## 💡 Code Highlights

### Object-Oriented JavaScript
```javascript
class Goose {
    constructor(state, weeksLeft, x, y, gender = 'female', parent = null) {
        this.state = state;
        // ... properties
    }
    
    move(width, height) {
        // Movement logic with parent following
    }
    
    draw(ctx) {
        // Canvas rendering for different states
    }
}
```

### AI Pathfinding
```javascript
findNearestGoose(geese) {
    let nearest = null;
    let minDist = Infinity;
    for (const goose of geese) {
        if (goose.state !== GooseState.EGG && !goose.hiding) {
            const dist = this.distance(goose);
            if (dist < minDist) {
                minDist = dist;
                nearest = goose;
            }
        }
    }
    return nearest;
}
```

### Game Loop
```javascript
function gameLoop() {
    game.update();  // Update game state
    game.draw();    // Render to canvas
    requestAnimationFrame(gameLoop);  // 60 FPS
}
```

## 🎓 Skills Demonstrated

✅ **Python/Flask** - Web server setup and routing  
✅ **JavaScript** - OOP, game loops, algorithms  
✅ **HTML5 Canvas** - 2D graphics rendering  
✅ **CSS** - Modern styling with gradients and animations  
✅ **Game Development** - State machines, AI, collision detection  
✅ **Clean Code** - Well-organized, commented, modular  

## 🔧 Customization Ideas

Want to expand the game? Try adding:

- [ ] Sound effects with Web Audio API
- [ ] Different difficulty levels
- [ ] More predator types
- [ ] Weather effects (wind, rain)
- [ ] Backend high score system with database
- [ ] Multiplayer with WebSockets
- [ ] Mobile touch controls
- [ ] Save/load game state

## 🐛 Troubleshooting

**Port already in use?**
```bash
# Change port in app.py:
app.run(debug=True, port=5001)  # Use different port
```

**Flask not found?**
```bash
pip install Flask
```

**Python not found?**
- Download from [python.org](https://python.org)
- Make sure to check "Add Python to PATH" during installation

## 📝 License

MIT License - Free to use and modify!

## 🚀 Deploying (Optional)

Want to share your game online?

### Option 1: GitHub Pages (Static Only)
- Remove Flask, serve static files directly
- Push to GitHub with GitHub Actions

### Option 2: Heroku (Free tier)
```bash
# Add Procfile:
web: python app.py

# Deploy:
heroku create
git push heroku main
```

### Option 3: Replit
- Upload project to [replit.com](https://replit.com)
- Click "Run" - automatically detects Flask!

## 🎉 That's It!

Enjoy the game! Feel free to customize and expand it. This is a great portfolio project showing full-stack web development skills.

---

Made with 🪿 and ❤️
