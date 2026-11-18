# Card Match (Unity memory game)

A card-matching memory game. All cards are shown briefly at the start of each level, then flipped face down. Find every pair before the timer runs out. Each level sets its own number of pairs and time limit, consecutive matches build a combo multiplier, and your best score and highest level are saved between sessions.

**Unity 2021.3.31f1** · C#

## What the code shows

- **Data-driven levels.** `LevelData` (a ScriptableObject) sets the number of pairs and the time limit for each level, and `LevelManager` serves them in order, so the difficulty curve is tuned without touching code.
- **Card library and fair shuffling.** `CardLibrary` (a ScriptableObject) picks random pairs and shuffles them with a **Fisher–Yates** shuffle.
- **Auto-sizing board.** `BoardGenerator` works out a near-square grid from the card count and scales the cards to fit the screen, so any number of pairs lays out correctly.
- **Event-driven flow.** Each `CardView` raises `OnSelected`. `GameManager` handles the selection, locks input while two cards are being checked so you can't click a third, and passes the result to the score, audio and UI managers.
- **Card states.** Face down, face up and matched states stop invalid clicks. A coroutine animates the flip by scaling the card on the X axis.
- **Scoring.** Combo-based: each consecutive match is worth more, and a mismatch resets the combo. Moves are also tracked.
- **Saves.** `SaveSystem` stores career stats as JSON in `PlayerPrefs`.

## Project structure

```
Assets/Development/
├── Scripts/
│   ├── Animation/  CardFlipAnimation
│   ├── Board/      BoardGenerator
│   ├── Card/       CardData, CardLibrary, CardView
│   ├── Core/       GameTimer, MatchResolver, SaveSystem, SaveData
│   ├── Data/       LevelData
│   └── Managers/   GameManager, LevelManager, ScoreManager, UIManager, AudioManager
└── Scenes/GamePlay.unity
```

## How to run

1. Open the project in **Unity 2021.3.31f1** (2021.3 LTS or newer).
2. Open `Assets/Development/Scenes/GamePlay.unity` and press Play.
3. Click cards to flip them and find matching pairs.
