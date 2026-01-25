# Tank Warfare Simulation: A Study in 2D Projectile Physics and Interactive Systems

## Abstract

This project represents a technical exploration into the development of a real-time, multiplayer combat simulation using the p5.js library. The primary objective was to engineer a robust 2D rendering engine capable of handling user input, projectile physics, and collision detection within a continuous state loop. Beyond a simple entertainment application, this software serves as a demonstration of vector-based movement, array-based trajectory tracking, and state management in a JavaScript environment.

## Technical Architecture

The core of the application is built upon the p5.js framework, leveraging its `setup()` and `draw()` lifecycles to maintain a consistent frame rate for fluid animation. The architecture is modular, separating concerns between rendering logic (`draw`), state initialization (`setup`), and event handling (keyboard listeners).

### Key Components

*   **Game State Management**: The system utilizes a finite state machine (FSM) to transition between `Initialize`, `Running`, and `End` states. This ensures that resources are allocated efficiently and that the update loop only processes relevant logic for the current context.
*   **Rendering Engine**: Visual assets are preloaded to minimize runtime latency. The `draw` loop continuously clears and repaints the canvas, updating object positions based on delta time and velocity vectors.
*   **Input Handling**: Asynchronous event listeners track key states for both players simultaneously, allowing for seamless local multiplayer interaction without input blocking.

## Physics Engine and Trajectory Analysis

One of the most significant technical achievements of this project is the implementation of the ballistic trajectory system. Rather than relying on simple linear interpolation, the project implements a gravity-mimicking algorithm to simulate projectile motion.

### Trajectory Tracking with Dynamic Arrays
A custom implementation of 2D arrays (`btx` and `bty`) was utilized to store and compute the path of each projectile.
*   **Vector Calculation**: Each bullet possesses a velocity vector broken down into horizontal (`dx`) and vertical (`dy`) components.
*   **Gravity Simulation**: The vertical velocity component (`dy`) is iteratively modified by a constant acceleration factor, simulating the effect of gravity. This results in a parabolic arc which adds a layer of strategic depth to the gameplay.
*   **Path Persistence**: The system calculates the theoretical path of the projectile and stores these coordinates in arrays. This allows the rendering engine to not only draw the projectile at its current position but also theoretically predict or visualize the path if needed.

## Algorithmic Challenges and Solutions

### Challenge 1: Asynchronous Timing without Blocking
**Problem**: The standard JavaScript execution model is single-threaded. Introducing delays (e.g., for fire rate limiting) using blocking functions would freeze the entire rendering loop.
**Solution**: I implemented a delta-time checking mechanism using the `millis()` function. By capturing timestamps (`t`, `t3`) and comparing them against the current system time in each frame, the system achieves precise firing intervals (e.g., 60ms) without interrupting the game loop.

### Challenge 2: Trajectory Data Management
**Problem**: Managing the coordinate data for projectiles that change velocity over time required a data structure that could be dynamically updated.
**Solution**: I utilized the `push()` method to dynamically append coordinate data to the trajectory arrays. This approach allowed for flexible storage of path data, which is essential for the "Extra for Experts" requirement of complex data manipulation. The logic handles the continuous updating of these arrays to reflect the projectile's movement across the canvas.

## Installation and Execution

To deploy this simulation locally, ensure you have a modern web browser installed.

1.  **Clone the Repository**:
    ```bash
    git clone https://github.com/sarcaxtic12/Tank-Game.git
    ```
2.  **Navigate to Directory**:
    Open the directory containing the project files.
3.  **Launch**:
    Open `index.html` in your preferred browser. For optimal performance, it is recommended to use a local development server (e.g., Live Server in VS Code) to avoid cross-origin policies with local assets.

## Controls

The simulation supports two concurrent users on a single machine.

| Action | Player 1 | Player 2 |
| :--- | :--- | :--- |
| **Move Forward** | D | Left Arrow |
| **Move Backward** | A | Right Arrow |
| **Fire Projectile** | Shift | Enter |

## Future Development Trajectory

Current research suggests several avenues for optimization and feature expansion:
1.  **Terrain Complexity**: Implementing Perlin noise to generate non-flat terrain, requiring more complex collision detection algorithms.
2.  **Advanced Ballistics**: Incorporating wind resistance and variable projectile mass.
3.  **Data Persistence**: integrating local storage or a backend database to track long-term player statistics and ELO ratings.

---
*Authored by Hyder Shahzaib Ahmed*