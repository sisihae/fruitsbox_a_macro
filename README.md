# FruitsBox A Macro

This project provides an automation macro for the game FruitsBox A using Python. The macro leverages image recognition and clustering to interact with the game screen, automatically detecting game elements and performing in-game actions.

## 🍎 Overview

The macro uses screen capture and image processing techniques to:
- Detect fruit tiles and their grid positions from screen images.
- Cluster and organize the tile coordinates using KMeans clustering.
- Process the game logic that identifies positions where the sum is 10 and simulates mouse operations to automate game actions.

**NOTE**:  
This macro is dependent on Windows, as it uses packages like `pyautogui` (for mouse automation) and assumes image resources and certain screen layouts.  

---

## 🍎 Setup

1. Clone this repository:
    ```bash
    git clone https://github.com/sisihae/fruitsbox_a_macro.git
    cd fruitsbox_a_macro
    ```

2. Create and activate a virtual environment (optional but recommended):
    ```bash
    python -m venv .venv
    source .venv/bin/activate  # On Windows: .venv\Scripts\activate
    ```

3. Install dependencies:
    ```bash
    pip install pyautogui pandas scikit-learn keyboard numpy
    ```

4. Set up environment:
    - Make sure your display scaling is 100%, and the game window is visible and not obstructed when you run the macro.

---

## 🍎 How It Works

### 1. Image Detection

- **Detection**: The macro scans the screen to locate all instances of number images (`1.png` to `9.png`) that represent the fruit numbers.
- **DataFrame**: For each detection, the position and size are registered in a pandas DataFrame.

### 2. Clustering

- **Initial Clustering**: All tile positions are grouped by proximity through `KMeans` (170 clusters), filtering duplicates.
- **Column & Row Clustering**: The positions are clustered into 17 columns and 10 rows, representing the game's grid, and averaged for clean grid coordinates.

### 3. Game Logic (Finding 10-sum Blocks)

- The macro examines all possible block areas in the grid, repeatedly searching for contiguous rectangles whose tile sum equals 10.
- When a valid area is found, it is set to 0 (marked as cleared), and the same search repeats to handle cascading effects.

### 4. Mouse Automation

- For each detected "sum-10" area, the mouse is moved (with small corrections to ensure full coverage) and performs a click-drag to select/clear those areas in-game.
- The macro auto-repeats this detection and action loop to clear as many tiles as possible.

**Interruption**:  
You can stop the macro at any time by pressing the `q` key.

---

## 🍎 Usage

1. Open the FruitsBox A game and arrange window for visibility.
2. Run the notebook or script:
    - Use Jupyter Notebook and execute the cells sequentially, or convert and run as a script if you like.
3. The macro will automatically detect, process, and interact with the game.
4. Press `q` to stop the automation.

---

## 🍎 Notes

- Adjust the `confidence=` parameter or clustering numbers as needed if the grid size/game display changes.
- This macro could interact with your mouse and keyboard; make sure to use it when ready, as it may interfere with normal PC usage during operation.
