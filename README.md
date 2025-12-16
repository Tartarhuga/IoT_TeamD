# IoT_TeamA
This is the github repository for the IOT project

# M.A.B.I.T.E  
**Mental Ability Benchmarking and Intelligence Testing Environment**

## 1. Project Context

M.A.B.I.T.E (Mental Ability Benchmarking and Intelligence Testing Environment) is an embedded systems project developed in an academic context.  
The objective of this project is to design an interactive cognitive assessment platform using an ESP32 microcontroller.

The system evaluates and trains different mental abilities such as:
- Short-term memory
- Reaction speed
- Time perception

The project combines hardware interaction, real-time user input, visual feedback, and audio signals, all simulated using the **Wokwi** environment.

---

## 2. System Architecture

### 2.1 Hardware Components

- ESP32-C3 DevKit microcontroller
- SSD1306 OLED display (128×64, I2C)
- 4 LEDs (Red, Green, Blue, Yellow)
- 4 colored push buttons (matching LEDs)
- 1 gray push button (menu validation)
- 1 potentiometer (menu navigation)
- 1 piezo buzzer

### 2.2 User Interface

- **Potentiometer**: navigates through the menu options  
- **Gray button**: validates the selected option  
- **Colored buttons**: used for gameplay interactions  
- **OLED display**: provides visual feedback and game information  
- **LEDs and buzzer**: provide real-time visual and audio cues  

---

## 3. Software Structure

The software is written in **C++ using the Arduino framework** and is organized into the following main modules:

- Menu management
- OLED display handling
- Individual mini-games
- Score management
- Global cognitive challenge

The program uses a state-based approach, switching between menu navigation and gameplay modes.

---

## 4. Menu Navigation Logic

The menu contains five options:


    LED GAME (Simon Says)

    10 Second Timer

    Reflex Challenge

    Global Cognitive Challenge

    Score Board

Menu selection is controlled by mapping the potentiometer’s analog value to a discrete menu index.  
The gray button confirms the selection.

---

## 5. Simon Says Game (Memory Challenge)  
### *Implemented by the author*

### 5.1 Educational Objective

The Simon Says game is designed to evaluate and improve:
- Sequential memory
- Attention
- Sensorimotor coordination

The difficulty increases progressively by extending the sequence length after each successful round.

---

### 5.2 Functional Description

1. The system generates a random sequence of colors.
2. Each color is displayed using a LED and an associated tone.
3. The player must reproduce the sequence using the corresponding buttons.
4. The game continues as long as the sequence is correctly reproduced.
5. An error ends the game and displays the final score.

---

### 5.3 Simon Says – Functional Flow Diagram

┌───────────────┐
│ Start Simon │
└───────┬───────┘
│
▼
┌─────────────────────┐
│ Initialize score │
│ Clear sequence │
└───────┬─────────────┘
│
▼
┌─────────────────────┐
│ Add random LED │
│ to sequence │
└───────┬─────────────┘
│
▼
┌─────────────────────┐
│ Play LED + sound │
│ sequence │
└───────┬─────────────┘
│
▼
┌─────────────────────┐
│ Player inputs │
│ sequence │
└───────┬─────────────┘
│
┌─────┴─────┐
│ Correct ? │
└─────┬─────┘
│Yes
▼
┌─────────────────────┐
│ Increase score │
│ Level-up sound │
└───────┬─────────────┘
│
└───► Loop to add next LED
     No
     ▼
┌─────────────────────┐
│ Game Over │
│ Display score │
└─────────────────────┘

---

### 5.4 Key Functions Explanation

#### `runSimonGame()`
Main control loop of the Simon Says game:
- Initializes variables and random seed
- Manages game progression
- Displays scores
- Handles game over conditions
- Updates best score

#### `lightLedAndPlayTone(byte ledIndex)`
Activates a LED and plays a corresponding tone using the buzzer to reinforce memorization through multisensory feedback.

#### `playSequence()`
Plays the full stored sequence by iterating through the LED array.

#### `readButtons()`
Continuously checks the state of the four colored buttons and returns the index of the pressed button.

#### `checkUserSequence()`
Compares user input to the expected sequence and detects errors.

#### `playLevelUpSound()`
Plays a short success melody when the player completes a level.

---

## 6. Other Mini-Games Overview

### 6.1 10-Second Timer Challenge
Tests the player’s internal time estimation by asking them to press a button exactly after 10 seconds.

### 6.2 Reflex Challenge
Measures reaction speed by lighting up a random LED and timing the player’s response.

---

## 7. Global Cognitive Challenge

This mode sequentially executes:
1. Simon Says
2. 10-Second Timer
3. Reflex Challenge

A global score is calculated using the results of all three games, providing an overall cognitive performance indicator.

---

## 8. Score Management

Best scores are stored temporarily in RAM:
- Best Simon score
- Best timer deviation (ms)
- Best reflex average (ms)
- Best global score

Scores reset when the system is powered off.

---

## 9. Simulation Environment

The entire system is simulated using **Wokwi**, allowing:
- Hardware validation
- Rapid testing
- Debugging without physical components

---

## 10. Conclusion

M.A.B.I.T.E demonstrates how embedded systems can be used to create interactive cognitive evaluation tools.  
The Simon Says game highlights the integration of hardware control, user interaction, and algorithmic logic in a real-time system.

---

## Author

Developed as part of an academic embedded systems project.  
Simon Says game implementation by **FranklinTheTeamLead**.
