# Wells Blue Bunny Memory Match - Game Architecture

## System Overview

```
┌─────────────────────────────────────────────────────────────┐
│                    Wells Memory Match Game                   │
│                     (Single HTML File)                       │
└─────────────────────────────────────────────────────────────┘
                              │
                ┌─────────────┼─────────────┐
                │             │             │
           ┌────▼────┐   ┌────▼────┐   ┌───▼────┐
           │   HTML  │   │   CSS   │   │   JS   │
           │Structure│   │ Styling │   │ Logic  │
           └─────────┘   └─────────┘   └────────┘
                              │
                    ┌─────────┴─────────┐
                    │                   │
              ┌─────▼──────┐     ┌─────▼──────┐
              │   Images/  │     │    CSV     │
              │  (19 PNGs) │     │    Data    │
              └────────────┘     └────────────┘
```

## Component Architecture

### 1. Screen Management
```
┌──────────────────────────────────────────────────────┐
│                   Screen System                       │
├──────────────────────────────────────────────────────┤
│                                                       │
│  ┌─────────────────┐         ┌──────────────────┐  │
│  │ Difficulty      │  ────▶  │  Game Board      │  │
│  │ Selection       │         │  Screen          │  │
│  │ Screen          │         │                  │  │
│  │                 │         │  - Timer         │  │
│  │ - Easy (4x4)    │         │  - Score         │  │
│  │ - Hard (6x6)    │         │  - Card Grid     │  │
│  │ - High Scores   │         │                  │  │
│  └─────────────────┘         └──────────────────┘  │
│         │                             │             │
│         │                             │             │
│         └──────────┬──────────────────┘             │
│                    │                                │
│                    ▼                                │
│         ┌──────────────────────┐                   │
│         │   End Game Modal     │                   │
│         │                      │                   │
│         │  - Final Score       │                   │
│         │  - High Score Check  │                   │
│         │  - Play Again        │                   │
│         └──────────────────────┘                   │
└──────────────────────────────────────────────────────┘
```

### 2. Modal System
```
┌──────────────────────────────────────────────────────┐
│                   Modal Overlays                      │
├──────────────────────────────────────────────────────┤
│                                                       │
│  ┌─────────────────────────────────────────────┐    │
│  │         Match Success Modal                  │    │
│  │  ┌────────────────────────────────────────┐ │    │
│  │  │  🎉 Celebration Emoji                  │ │    │
│  │  │  ┌──────────────────────────────────┐  │ │    │
│  │  │  │   Product Image (280x280)        │  │ │    │
│  │  │  └──────────────────────────────────┘  │ │    │
│  │  │  Product Name (Pink, Bold)             │ │    │
│  │  │  "Tongue-in-cheek description..."      │ │    │
│  │  │  [Continue Playing Button]             │ │    │
│  │  └────────────────────────────────────────┘ │    │
│  │                                              │    │
│  │  Actions:                                    │    │
│  │  - Pause Timer ⏸️                            │    │
│  │  - Display Product Info                     │    │
│  │  - Resume Timer on Close ▶️                 │    │
│  └─────────────────────────────────────────────┘    │
│                                                       │
│  ┌─────────────────────────────────────────────┐    │
│  │         End Game Modal                       │    │
│  │  ┌────────────────────────────────────────┐ │    │
│  │  │  Title: "You Win!" or "Time's Up!"     │ │    │
│  │  │  Message with stats                     │ │    │
│  │  │  Final Score: XXX points                │ │    │
│  │  │  High Score indicator                   │ │    │
│  │  │  [Play Again Button]                    │ │    │
│  │  └────────────────────────────────────────┘ │    │
│  └─────────────────────────────────────────────┘    │
└──────────────────────────────────────────────────────┘
```

### 3. Card System
```
┌──────────────────────────────────────────────────────┐
│                   Card Component                      │
├──────────────────────────────────────────────────────┤
│                                                       │
│  Card Structure (3D Flip):                           │
│                                                       │
│  ┌─────────────────┐         ┌─────────────────┐   │
│  │   Card Back     │  flip   │   Card Front    │   │
│  │                 │  ────▶  │                 │   │
│  │      🍦         │         │  [Product Img]  │   │
│  │   (Shimmer)     │         │                 │   │
│  │                 │         │                 │   │
│  └─────────────────┘         └─────────────────┘   │
│   (Face Down)                 (Face Up)             │
│                                                       │
│  States:                                             │
│  - default      : Face down, clickable               │
│  - is-flipped   : Face up, showing image             │
│  - matched      : Permanently face up, pop animation │
│                                                       │
│  Data Attributes:                                    │
│  - data-name        : Product name (for matching)    │
│  - data-description : Product description            │
│  - data-imageUrl    : Path to product image          │
└──────────────────────────────────────────────────────┘
```

### 4. Game State Machine
```
┌──────────────────────────────────────────────────────┐
│                  Game State Flow                      │
├──────────────────────────────────────────────────────┤
│                                                       │
│  START                                               │
│    │                                                 │
│    ▼                                                 │
│  [Difficulty Selection]                              │
│    │                                                 │
│    ▼                                                 │
│  Initialize Game                                     │
│    ├─ Set pairsToMatch (8 or 18)                    │
│    ├─ Set timeLeft (120 or 240)                     │
│    ├─ Reset score = 0                               │
│    ├─ Reset incorrectGuesses = 0                    │
│    └─ Create shuffled board                         │
│    │                                                 │
│    ▼                                                 │
│  Start Timer ⏱️                                      │
│    │                                                 │
│    ▼                                                 │
│  ┌─────────────────────────────────────┐            │
│  │      PLAYING STATE                  │            │
│  │  ┌───────────────────────────────┐  │            │
│  │  │  Wait for card click          │  │            │
│  │  └───────────┬───────────────────┘  │            │
│  │              │                       │            │
│  │              ▼                       │            │
│  │  ┌───────────────────────────────┐  │            │
│  │  │  First card flipped           │  │            │
│  │  │  hasFlippedCard = true        │  │            │
│  │  └───────────┬───────────────────┘  │            │
│  │              │                       │            │
│  │              ▼                       │            │
│  │  ┌───────────────────────────────┐  │            │
│  │  │  Second card flipped          │  │            │
│  │  │  lockBoard = true             │  │            │
│  │  └───────────┬───────────────────┘  │            │
│  │              │                       │            │
│  │              ▼                       │            │
│  │  ┌───────────────────────────────┐  │            │
│  │  │  Check for match              │  │            │
│  │  └───┬───────────────────┬───────┘  │            │
│  │      │                   │           │            │
│  │   MATCH              NO MATCH        │            │
│  │      │                   │           │            │
│  │      ▼                   ▼           │            │
│  │  ┌────────┐      ┌──────────────┐   │            │
│  │  │ Pause  │      │ -2 points    │   │            │
│  │  │ Timer  │      │ Flip back    │   │            │
│  │  └───┬────┘      └──────┬───────┘   │            │
│  │      │                   │           │            │
│  │      ▼                   │           │            │
│  │  ┌────────┐              │           │            │
│  │  │ Show   │              │           │            │
│  │  │ Modal  │              │           │            │
│  │  └───┬────┘              │           │            │
│  │      │                   │           │            │
│  │      ▼                   │           │            │
│  │  ┌────────┐              │           │            │
│  │  │ Resume │              │           │            │
│  │  │ Timer  │              │           │            │
│  │  └───┬────┘              │           │            │
│  │      │                   │           │            │
│  │      ▼                   ▼           │            │
│  │  ┌────────────────────────────────┐ │            │
│  │  │ +50 points                     │ │            │
│  │  │ matchesFound++                 │ │            │
│  │  │ Reset board state              │ │            │
│  │  └────────┬───────────────────────┘ │            │
│  │           │                          │            │
│  │           ▼                          │            │
│  │  ┌────────────────────┐              │            │
│  │  │ All pairs matched? │              │            │
│  │  └───┬────────────┬───┘              │            │
│  │      │            │                  │            │
│  │     YES          NO                  │            │
│  │      │            │                  │            │
│  │      │            └──────────────────┤            │
│  │      │                               │            │
│  └──────┼───────────────────────────────┘            │
│         │                                            │
│         ▼                                            │
│  ┌─────────────────┐                                │
│  │  Calculate      │                                │
│  │  Final Score    │                                │
│  │  - Base points  │                                │
│  │  - Time bonus   │                                │
│  │  - Speed bonus  │                                │
│  │  - Accuracy     │                                │
│  └────────┬────────┘                                │
│           │                                          │
│           ▼                                          │
│  ┌─────────────────┐                                │
│  │  Check High     │                                │
│  │  Score          │                                │
│  └────────┬────────┘                                │
│           │                                          │
│           ▼                                          │
│  ┌─────────────────┐                                │
│  │  Show End Game  │                                │
│  │  Modal          │                                │
│  └────────┬────────┘                                │
│           │                                          │
│           ▼                                          │
│  [Play Again?] ──────▶ [Difficulty Selection]       │
│                                                       │
└──────────────────────────────────────────────────────┘
```

### 5. Timer System
```
┌──────────────────────────────────────────────────────┐
│                   Timer Controller                    │
├──────────────────────────────────────────────────────┤
│                                                       │
│  setInterval (1000ms)                                │
│       │                                              │
│       ▼                                              │
│  ┌─────────────────┐                                │
│  │ timerPaused?    │                                │
│  └────┬────────┬───┘                                │
│       │        │                                     │
│      YES      NO                                     │
│       │        │                                     │
│       │        ▼                                     │
│       │   ┌─────────────────┐                       │
│       │   │ timeLeft--      │                       │
│       │   │ Update Display  │                       │
│       │   └────┬────────────┘                       │
│       │        │                                     │
│       │        ▼                                     │
│       │   ┌─────────────────┐                       │
│       │   │ timeLeft < 10?  │                       │
│       │   └────┬────────┬───┘                       │
│       │        │        │                            │
│       │       YES      NO                            │
│       │        │        │                            │
│       │        ▼        │                            │
│       │   ┌─────────┐  │                            │
│       │   │ Turn    │  │                            │
│       │   │ Red &   │  │                            │
│       │   │ Pulse   │  │                            │
│       │   └─────────┘  │                            │
│       │                │                             │
│       │        ┌───────┘                            │
│       │        │                                     │
│       │        ▼                                     │
│       │   ┌─────────────────┐                       │
│       │   │ timeLeft <= 0?  │                       │
│       │   └────┬────────┬───┘                       │
│       │        │        │                            │
│       │       YES      NO                            │
│       │        │        │                            │
│       │        ▼        │                            │
│       │   ┌─────────┐  │                            │
│       │   │ End     │  │                            │
│       │   │ Game    │  │                            │
│       │   │ (Loss)  │  │                            │
│       │   └─────────┘  │                            │
│       │                │                             │
│       └────────────────┴─────────▶ Continue         │
│                                                       │
│  Pause Triggers:                                     │
│  - Match modal shown                                 │
│                                                       │
│  Resume Triggers:                                    │
│  - Match modal closed                                │
└──────────────────────────────────────────────────────┘
```

### 6. Scoring System
```
┌──────────────────────────────────────────────────────┐
│                  Score Calculator                     │
├──────────────────────────────────────────────────────┤
│                                                       │
│  Base Score:                                         │
│  ┌────────────────────────────────────────────┐     │
│  │  Each Match:        +50 points             │     │
│  │  Each Miss:         -2 points              │     │
│  │  (Minimum: 0)                              │     │
│  └────────────────────────────────────────────┘     │
│                                                       │
│  Win Bonuses:                                        │
│  ┌────────────────────────────────────────────┐     │
│  │  Time Bonus:                               │     │
│  │    timeLeft × 3 points                     │     │
│  │                                             │     │
│  │  Speed Demon Bonus:                        │     │
│  │    IF timeLeft > 50% of total              │     │
│  │    THEN +100 points                        │     │
│  │                                             │     │
│  │  Accuracy Bonus:                           │     │
│  │    100 - (incorrectGuesses × 10)           │     │
│  │    (Minimum: 0, Maximum: 100)              │     │
│  └────────────────────────────────────────────┘     │
│                                                       │
│  Example (Easy Mode, Perfect Game):                  │
│  ┌────────────────────────────────────────────┐     │
│  │  8 matches × 50        = 400 points        │     │
│  │  120 seconds × 3       = 360 points        │     │
│  │  Speed bonus           = 100 points        │     │
│  │  Accuracy (0 misses)   = 100 points        │     │
│  │  ─────────────────────────────────         │     │
│  │  TOTAL                 = 960 points        │     │
│  └────────────────────────────────────────────┘     │
└──────────────────────────────────────────────────────┘
```

### 7. Data Flow
```
┌──────────────────────────────────────────────────────┐
│                    Data Pipeline                      │
├──────────────────────────────────────────────────────┤
│                                                       │
│  CSV File (wells-descriptions.csv)                   │
│       │                                              │
│       ▼                                              │
│  Fetch API                                           │
│       │                                              │
│       ▼                                              │
│  Parse CSV                                           │
│  ┌─────────────────────────────────────┐            │
│  │ Split by newline                    │            │
│  │ Skip header row                     │            │
│  │ Split each line by comma            │            │
│  │ Extract: name, description, filename│            │
│  └────────────┬────────────────────────┘            │
│               │                                      │
│               ▼                                      │
│  Map Filenames                                       │
│  ┌─────────────────────────────────────┐            │
│  │ .jpg → .png conversion              │            │
│  │ Handle special cases                │            │
│  │ (e.g., HotBeefSundae → HotBeef_)   │            │
│  └────────────┬────────────────────────┘            │
│               │                                      │
│               ▼                                      │
│  Create Product Objects                              │
│  ┌─────────────────────────────────────┐            │
│  │ {                                   │            │
│  │   name: "Product Name",             │            │
│  │   description: "Description...",    │            │
│  │   filename: "file.png",             │            │
│  │   imageUrl: "Images/file.png"       │            │
│  │ }                                   │            │
│  └────────────┬────────────────────────┘            │
│               │                                      │
│               ▼                                      │
│  allProducts[] Array (19 items)                      │
│       │                                              │
│       ▼                                              │
│  Game Selection                                      │
│  ┌─────────────────────────────────────┐            │
│  │ Shuffle array                       │            │
│  │ Select first N products             │            │
│  │ (8 for easy, 18 for hard)           │            │
│  └────────────┬────────────────────────┘            │
│               │                                      │
│               ▼                                      │
│  Duplicate for Pairs                                 │
│  ┌─────────────────────────────────────┐            │
│  │ [...products, ...products]          │            │
│  └────────────┬────────────────────────┘            │
│               │                                      │
│               ▼                                      │
│  Shuffle Again                                       │
│       │                                              │
│       ▼                                              │
│  Create Card Elements                                │
│  ┌─────────────────────────────────────┐            │
│  │ For each product:                   │            │
│  │   Create <div class="card">         │            │
│  │   Set data attributes               │            │
│  │   Add front/back faces              │            │
│  │   Attach click listener             │            │
│  └────────────┬────────────────────────┘            │
│               │                                      │
│               ▼                                      │
│  Render to Game Board                                │
└──────────────────────────────────────────────────────┘
```

## Technology Stack

- **HTML5**: Structure and semantic markup
- **CSS3**: Styling, animations, gradients, transforms
- **JavaScript (ES6+)**: Game logic, async/await, arrow functions
- **LocalStorage API**: High score persistence
- **Fetch API**: CSV data loading
- **CSS Grid**: Card layout system
- **CSS Transforms**: 3D card flip animations

## Performance Optimizations

1. **CSS Animations**: GPU-accelerated transforms
2. **Event Delegation**: Minimal event listeners
3. **Efficient Shuffling**: Fisher-Yates algorithm
4. **Lazy Loading**: Images loaded as needed
5. **LocalStorage**: Client-side persistence (no server calls)

## Browser Compatibility

- Chrome 90+
- Firefox 88+
- Safari 14+
- Edge 90+
- Mobile browsers (iOS Safari, Chrome Mobile)

