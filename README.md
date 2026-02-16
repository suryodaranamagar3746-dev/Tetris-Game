# Pygame Tetris

A robust, object-oriented implementation of the classic Tetris game built with Python and the **Pygame** library. This project features high-fidelity mechanics, a modular code architecture, and a dynamic leveling system.

---

## 🚀 Features

* **Authentic Gameplay**: Precise collision detection, tetromino rotation, and line-clearing logic.
* **Dynamic Difficulty**: Automatic level progression that increases the fall speed as you clear more lines.
* **Advanced UI**: 
    * **Main Game Grid**: Classic 10x20 layout with smooth rendering.
    * **Preview Window**: Real-time rendering of the next three upcoming shapes.
    * **Scoreboard**: Tracks current score, total lines cleared, and current level.
* **Responsive Input**: Custom timer system for fluid movement and rotation without "sticky" keys.

---

## 🏗️ Internal Architecture

The project is divided into several modules to ensure a clean separation of concerns:

### 1. Game Core (`game.py`)
* **Field Data**: Uses a 2D matrix (`field_data`) to track static blocks and manage the game state.
* **Tetromino Logic**: Manages individual block positions. It utilizes vector math to handle 90-degree rotations around a dynamic pivot point.
* **Collision System**: Implements specialized checks for boundaries (walls/floor) and internal collisions with existing blocks.

### 2. UI & Component Management (`main.py`)
* The `Main` class acts as the central hub, coordinating the `Game`, `Score`, and `Preview` components.
* **State Coordination**: It manages the "Next Shape" queue to ensure the preview window and game engine stay synchronized.

### 3. Timing & Performance (`timer.py`)
* Uses a custom `Timer` class based on `pygame.time.get_ticks()`. This manages game events (gravity, movement delays) independently of the frame rate for a consistent feel across different hardware.

### 4. Configuration (`setting.py`)
* A centralized file for all game constants, including HEX colors, grid dimensions, and coordinate data for all seven tetromino shapes.

---

## 🕹️ Controls & Input Handling

The game uses a sophisticated input system to balance precision and speed. Controls are processed through `pygame.key.get_pressed()` combined with internal timers to prevent accidental double-inputs.

| Key | Action | Internal Logic |
| :--- | :--- | :--- |
| **Left Arrow / A** | Move Left | Triggers `MOVE_WAIT_TIME` timer to allow for single-step or rapid-scroll movement. |
| **Right Arrow / D** | Move Right | Checks horizontal collision against `field_data` before updating position. |
| **Up Arrow / W** | Rotate Shape | Uses `Vector2.rotate(90)` around the pivot; includes a "wall-kick" check to prevent rotating out of bounds. |
| **Down Arrow / S** | Soft Drop | Overrides the standard gravity timer with `down_speed_faster` for rapid descent. |
| **Escape / Close** | Exit Game | Safely terminates the Pygame instance and system process. |

---

## 🎮 Getting Started

### Prerequisites
* Python 3.x
* Pygame library

### Installation
1.  **Clone the repository:**
    ```bash
    git clone [https://github.com/yourusername/pygame-tetris.git](https://github.com/yourusername/pygame-tetris.git)
    cd pygame-tetris
    ```
2.  **Install dependencies:**
    ```bash
    pip install pygame
    ```

### Running the Game
```bash
python main.py
