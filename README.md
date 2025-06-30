# Self-Driving Car Simulation

A JavaScript-based neural network simulation that trains virtual cars to drive autonomously using genetic algorithms and collision avoidance sensors.

## Overview

This project implements a self-driving car simulation using vanilla JavaScript and HTML5 Canvas. The simulation features:

- **Neural Network-Controlled Cars**: AI cars learn to navigate through traffic using a custom neural network
- **Genetic Algorithm**: Cars evolve over generations to improve driving performance
- **Real-time Visualization**: Live neural network visualization showing decision-making process
- **Traffic System**: Dynamic traffic with collision detection
- **Sensor System**: Ray-casting sensors for environment perception

## Demo

Open `index.html` in your browser to start the simulation. The interface includes:
- **Left Canvas**: Car simulation with road, traffic, and AI cars
- **Right Canvas**: Real-time neural network visualization
- **Control Buttons**: Save and discard the best performing neural network

## Architecture

### Core Components

#### 1. **Neural Network (`network.js`)**
- Multi-layer perceptron with configurable architecture
- Feed-forward propagation for decision making
- Genetic mutation for evolutionary learning
- Default architecture: 5 inputs → 6 hidden → 4 outputs

#### 2. **Car System (`car.js`)**
- Physics-based movement with acceleration, friction, and steering
- Collision detection using polygon intersection
- Three control types: AI, manual (KEYS), and dummy traffic
- Integrated sensor system for environment perception

#### 3. **Sensor System (`sensor.js`)**
- 5 ray-casting sensors with 150-pixel range
- 90-degree spread for comprehensive environment scanning
- Detects road borders and traffic obstacles
- Provides normalized distance data to neural network

#### 4. **Road System (`road.js`)**
- 3-lane highway with infinite length
- Dynamic lane center calculation
- Border collision detection
- Visual lane markings

#### 5. **Traffic Management (`main.js`)**
- Spawns 200 AI cars for evolutionary training
- Predefined traffic patterns with dummy cars
- Best performer selection based on distance traveled
- Local storage for brain persistence

#### 6. **Visualization (`visualizer.js`)**
- Real-time neural network graph rendering
- Color-coded weights and biases
- Directional output labels (forward, left, right, reverse)
- Dynamic connection strength visualization

### Neural Network Details

**Input Layer (5 neurons)**: Sensor readings
- Each sensor provides distance to nearest obstacle (0-1 normalized)

**Hidden Layer (6 neurons)**: Feature processing
- Fully connected to input layer
- Uses threshold activation function

**Output Layer (4 neurons)**: Control commands
- Forward acceleration
- Left steering
- Right steering  
- Reverse acceleration

## Genetic Algorithm

The simulation uses a genetic algorithm approach:

1. **Population**: 200 cars with random neural networks
2. **Fitness**: Distance traveled without crashing
3. **Selection**: Best performing car's brain is saved
4. **Mutation**: 15% mutation rate for genetic diversity
5. **Evolution**: New generation inherits and mutates from the best performer

## Features

### AI Learning
- **Autonomous Navigation**: Cars learn to stay in lanes and avoid obstacles
- **Traffic Awareness**: Responds to dynamic traffic patterns
- **Collision Avoidance**: Uses sensor data to prevent crashes
- **Performance Optimization**: Evolutionary improvement over generations

### Visual Elements
- **Car Rendering**: Polygon-based car graphics with damage states
- **Sensor Visualization**: Yellow rays showing active sensing
- **Neural Network Display**: Live weight and bias visualization
- **Traffic Differentiation**: Color-coded cars (blue AI, green traffic, red damaged)

### Controls
- **Save**: Stores the best neural network in localStorage
- **Discard**: Clears saved neural network data
- **Manual Override**: Arrow keys for manual car control (when enabled)

## Getting Started

### Prerequisites
- Modern web browser with HTML5 Canvas support
- No additional dependencies required

### Installation
1. Clone or download the repository
2. Open `index.html` in your web browser
3. The simulation starts automatically

### Usage
1. **Watch the AI Learn**: Cars will initially drive randomly but improve over time
2. **Save Progress**: Click "Save" when you see good performance to preserve the neural network
3. **Reset Learning**: Click "Discard" to start fresh with random networks
4. **Monitor Progress**: Watch the neural network visualization to see decision patterns

## 📁 File Structure

```
self-driving-car-sim/
├── index.html          # Main HTML file and entry point
├── style.css           # Styling for canvas and UI elements
├── main.js             # Main simulation loop and traffic management
├── car.js              # Car physics, rendering, and AI integration
├── network.js          # Neural network implementation
├── sensor.js           # Ray-casting sensor system
├── road.js             # Road rendering and lane management
├── controls.js         # Input handling (keyboard/AI)
├── visualizer.js       # Neural network visualization
├── utils.js            # Helper functions (lerp, intersections, etc.)
└── README.md           # This file
```

## 🔧 Customization

### Neural Network Architecture
Modify the network structure in `car.js`:
```javascript
this.brain = new NeuralNetwork([this.sensor.rayCount, 6, 4]);
//                              [inputs, hidden, outputs]
```

### Population Size
Adjust the number of AI cars in `main.js`:
```javascript
const N = 200; // Number of cars in population
```

### Sensor Configuration
Customize sensor behavior in `sensor.js`:
```javascript
this.rayCount = 5;           // Number of sensors
this.rayLength = 150;        // Sensor range
this.raySpread = Math.PI / 2; // Sensor spread angle
```

### Traffic Patterns
Modify traffic in `main.js` by adjusting the `traffic` array.

## Learning Outcomes

This project was built following the lecture series by Dr. Radu Mariescu-Istodor
This project demonstrates:
- **Neural Network Fundamentals**: Forward propagation, weights, biases
- **Genetic Algorithms**: Selection, mutation, evolution
- **Computer Vision**: Ray-casting, collision detection
- **Game Physics**: Movement, acceleration, friction
- **Data Visualization**: Real-time graph rendering
- **JavaScript Canvas**: 2D graphics and animation

## Future Enhancements

Potential improvements:
- **Advanced Neural Networks**: LSTM or CNN architectures
- **Reinforcement Learning**: Q-learning implementation
- **Complex Scenarios**: Intersections, traffic lights, weather
- **Performance Metrics**: Speed, efficiency, safety scoring
- **3D Visualization**: WebGL-based 3D environment
- **Multiplayer Mode**: Competitive AI training