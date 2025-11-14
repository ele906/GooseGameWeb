# 🪿 Goose Migration Simulation Game

A realistic web-based goose migration simulation game built with Flask and vanilla JavaScript. Guide your flock through the challenges of migration using **Monte Carlo simulation** for realistic survival probabilities and **geographic modeling** for climate-based gameplay!

## 🔗 Play on Browser!
https://ele906.github.io/GooseGameWeb/

## 🎮 Features

### Realistic Life Cycle
- **Eggs** 🥚: Hatch in 3 weeks (±0.5 weeks variation)
- **Goslings** 🐥: Mature into adults in 8 weeks (±1.5 weeks variation)
- **Adults** 🪿: Can breed and migrate

### Monte Carlo Simulation
- **Individual Genetic Variation**: Each goose has unique survival probabilities drawn from normal distributions
- **Stochastic Breeding**: Clutch sizes vary naturally (1-8 eggs, mean 4)
- **Probabilistic Survival**: Egg survival 85% ±10%, gosling survival 70% ±12%
- **Random Events**: Storms and environmental challenges strike probabilistically

### Geographic Modeling
- **Latitude/Longitude System**: Real coordinate-based world map
- **Climate Zones**: 7 distinct zones from Arctic to Antarctic
- **Migration Mechanics**: Directional travel (N/S/E/W) changes location and survival rates
- **Optimal Breeding Grounds**: Temperate zones (30-50°N) offer best survival

### Dynamic Systems
- **Weather System**: Sunny, cloudy, rain, and storm conditions
- **Seasonal Changes**: Spring, summer, fall, winter affect survival
- **Predator AI**: Foxes and eagles with stochastic pathfinding
- **Energy Management**: Migration costs energy, low energy reduces survival
- **Safe Zones**: Ponds and bushes provide protection

## 🧪 Simulation Mathematics

### Normal Distribution for Realism
The game uses the **Box-Muller transform** to generate normally distributed random numbers, creating realistic biological variation:

```javascript
// Each egg has individual survival probability
eggSurvival = N(μ=0.85, σ=0.10)  // Mean 85%, StdDev 10%

// Clutch size varies naturally
clutchSize = N(μ=4, σ=1.5)  // Mean 4 eggs, StdDev 1.5

// Incubation time has natural variation
incubationWeeks = N(μ=3, σ=0.5)  // Mean 3 weeks, StdDev 0.5
```

### Climate-Based Survival Modifiers

| Climate Zone | Latitude Range | Survival Modifier |
|-------------|----------------|-------------------|
| Arctic | 60°N - 90°N | 0.6x (60%) |
| Subarctic | 50°N - 60°N | 0.8x (80%) |
| **Temperate** | **30°N - 50°N** | **1.0x (100%)** ⭐ |
| Subtropical | 15°N - 30°N | 0.85x (85%) |
| Tropical | 15°S - 15°N | 0.7x (70%) |
| S. Temperate | 15°S - 50°S | 0.9x (90%) |
| Antarctic | 50°S - 90°S | 0.5x (50%) |

### Probability Calculations

**Breeding Success:**
```
P(breeding) = N(μ=0.80, σ=0.15)
Energy requirement: >50 units
Cooldown: 300 game ticks
```

**Predator Catch Probability:**
```
P(catch) = 0.02 per tick when near prey
Distance-based: P increases as distance decreases
Safe zones: P(catch) = 0 in ponds/bushes
```

**Migration Energy Loss:**
```
ΔEnergy = -0.1 × distance × (1 + weatherVariance)
weatherVariance ∈ [0, 0.3] stochastically
```

## 🚀 Getting Started

### Prerequisites
- Python 3.7+
- pip

### Installation

1. **Install dependencies:**
```bash
pip install -r requirements.txt
```

2. **Run the game:**
```bash
python app.py
```

3. **Open browser:**
```
http://localhost:5000
```

## 🎯 How to Play

### Basic Actions
- **🖱️ Click**: Select individual geese
- **💕 Mate Button**: Breed selected adult geese (requires energy >50)
- **🌳 Hide All**: Protect all geese in bushes
- **🦊 Add Predator**: Spawn a fox or eagle for challenge

### Migration Strategy
1. **Choose Direction**: Click North/South/East/West
2. **Monitor Climate**: Check your climate zone
3. **Aim for Temperate**: 30-50°N latitude is optimal
4. **Watch Energy**: Migration drains energy reserves

### Survival Tips
- 🥚 **Protect Eggs**: Hide mothers near bushes before breeding
- ⚡ **Manage Energy**: Low energy = lower survival rates
- 🌡️ **Follow Temperature**: Migrate to temperate zones
- 💧 **Use Ponds**: Safe zones during predator attacks
- 🎲 **Plan for Randomness**: Not all goslings survive - that's natural!

## 📁 Project Structure

```
GooseGameWeb/
├── app.py                  # Flask server
├── requirements.txt        # Python dependencies
├── README.md              # This file
├── templates/
│   └── index.html         # Main game page with full UI
├── static/
│   ├── js/
│   │   └── game.js        # Game logic & Monte Carlo simulation
│   ├── css/
│   │   └── style.css      # Responsive styling
│   └── images/
│       ├── egg.png        # 🥚 Egg sprite
│       ├── gosling.png    # 🐥 Gosling sprite
│       ├── goose_adult.jpg # 🪿 Adult goose sprite
│       ├── fox.png        # 🦊 Fox predator
│       ├── eagle.png      # 🦅 Eagle predator
│       └── bush.png       # 🌳 Hiding spot
```

## 🔧 Simulation Parameters

Want to modify the simulation? Edit these constants in `game.js`:

```javascript
const SIMULATION_PARAMS = {
    // Survival probabilities
    EGG_SURVIVAL_MEAN: 0.85,
    EGG_SURVIVAL_STDDEV: 0.10,
    GOSLING_SURVIVAL_MEAN: 0.70,
    GOSLING_SURVIVAL_STDDEV: 0.12,
    
    // Breeding
    BREEDING_SUCCESS_MEAN: 0.80,
    BREEDING_SUCCESS_STDDEV: 0.15,
    CLUTCH_SIZE_MEAN: 4,
    CLUTCH_SIZE_STDDEV: 1.5,
    
    // Migration
    MIGRATION_DISTANCE: 150,  // km per move
    MIGRATION_ENERGY_LOSS: 0.1,
    
    // Safety
    SAFE_PERIOD_SECONDS: 10,  // Grace period at start
    
    // Climate
    OPTIMAL_LATITUDE_MIN: 35,
    OPTIMAL_LATITUDE_MAX: 55,
    LATITUDE_SURVIVAL_PENALTY: 0.3
};
```

## 🎲 Stochastic Features Explained

### 1. **Individual Variation**
Every goose is unique! When born, each gets:
- Individual egg survival probability from N(0.85, 0.10)
- Individual gosling survival probability from N(0.70, 0.12)
- Unique incubation/maturation times

### 2. **Geographic Realism**
- Start at 45°N, 75°W (Eastern North America)
- Each migration moves ~150km
- Climate zones affect survival multipliers
- Latitude affects breeding success

### 3. **Predator AI**
- Foxes: Ground-based, moderate speed
- Eagles: Aerial, faster speed
- Stochastic targeting: Choose random geese
- Distance-based catch probability

### 4. **Weather Randomness**
- 50% sunny, 30% cloudy, 15% rain, 5% storm
- Storms reduce health by 2 per tick
- Weather affects migration energy loss

### 5. **Breeding Variance**
- Success rate: 80% ±15% (individual variation)
- Clutch size: 1-8 eggs (normally distributed)
- Energy cost: -15 per breeding attempt
- Cooldown: 300 ticks between attempts

## 📊 Understanding the Statistics

### Why Monte Carlo?
Traditional games use fixed mechanics. This game uses **probabilistic modeling**:
- ✅ More realistic biological behavior
- ✅ No two playthroughs are the same
- ✅ Teaches statistical thinking
- ✅ Mirrors real ecology research

### Expected Outcomes
From 2 adult geese over 100 days:
- **Expected eggs**: 8-12 (varies by breeding success)
- **Expected hatchlings**: 6-10 (85% survival)
- **Expected adults**: 4-7 (70% survival from gosling)
- **Expected deaths**: 3-6 (predators, energy, climate)

Your results will vary due to randomness - that's the point! 🎲

## 🏆 Win Conditions

**Survival Challenge:**
- Keep your flock alive for 365 days
- Reach 20+ geese
- Maintain 100% survival rate in optimal climate

**Migration Challenge:**
- Start at 45°N
- Migrate to Arctic (>60°N) and back
- Return with >50% of original flock

**Breeding Challenge:**
- Start with 2 geese
- Reach 50+ geese
- Maintain genetic diversity (track lineages)

## 🐛 Known Features

- Safe period (10 seconds) at game start
- Geese auto-move with realistic wandering
- Weather changes every ~30 ticks
- Seasons change every 90 days
- Predators spawn randomly (5% chance per tick)
- Eggs spread ±60 pixels from mother

## 🎓 Educational Value

This game demonstrates:
- **Statistics**: Normal distributions, probability theory
- **Biology**: Life cycles, survival rates, breeding patterns
- **Geography**: Climate zones, migration patterns, latitude effects
- **Ecology**: Predator-prey dynamics, carrying capacity
- **Computer Science**: Monte Carlo methods, game loops, state machines

Perfect for:
- Statistics students learning probability distributions
- Biology classes studying population dynamics
- Geography lessons on climate and migration
- Anyone interested in simulation and modeling!

## 📝 Technical Details

### Technologies
- **Backend**: Flask (Python)
- **Frontend**: Vanilla JavaScript (ES6+)
- **Canvas**: HTML5 Canvas API for rendering
- **Math**: Box-Muller transform for normal distributions

### Performance
- 60 FPS target
- Handles 100+ geese smoothly
- Efficient collision detection
- Optimized image rendering

### Browser Support
- Chrome/Edge: ✅ Full support
- Firefox: ✅ Full support
- Safari: ✅ Full support
- Mobile: ✅ Responsive design

## 🤝 Contributing

Want to improve the simulation?
- Add new predator types with different AI
- Implement seasonal migration patterns
- Add weather effects (wind, temperature)
- Create more complex climate models
- Add disease/illness mechanics
- Implement food scarcity

## 📚 References

This simulation is inspired by:
- Real Canada Goose (*Branta canadensis*) migration patterns
- Population ecology models
- Monte Carlo methods in biology
- Geographic Information Systems (GIS)

## 📜 License

Educational project demonstrating Monte Carlo simulation in game development.
Free to use for learning and teaching!

## 🙏 Acknowledgments

- Built with Flask and vanilla JavaScript
- Images: Various sources
- Inspired by real goose migration ecology
- Educational tool for probability and statistics

---

**Start your migration journey!** 🪿✨

*Guide your flock through the seasons, avoid predators, and reach the optimal breeding grounds. Every decision matters in this stochastic world!*
