# Wells Blue Bunny Memory Game - Implementation Summary

## ✅ All Requirements Implemented

### 1. Difficulty Selection ✓
- **Easy Mode**: 4x4 grid (16 cards, 8 pairs) with 120-second timer
- **Hard Mode**: 6x6 grid (36 cards, 18 pairs) with 240-second timer
- Player selects difficulty before game starts
- High scores displayed for each difficulty level

### 2. Gameplay Mechanics ✓
- Standard memory game rules implemented
- Cards are face-down initially
- Smooth flip animation when clicked (0.6s CSS transition)
- Non-matching pairs flip back after 1.2-second delay
- Matched pairs remain face-up with "matched" class
- Cards cannot be clicked while locked or already flipped

### 3. Success Modal ✓
**When a player matches a pair:**
- Modal immediately displays with:
  - Larger product image (280x280px with border)
  - Product name from CSV (in pink with text shadow)
  - Tongue-in-cheek description from CSV (italic style)
  - Celebration emoji (🎉)
- **Timer pauses** when modal is shown (`timerPaused = true`)
- **Timer resumes** when modal is closed (`timerPaused = false`)
- Modal can be closed by:
  - Clicking "Continue Playing" button
  - Clicking anywhere on the modal overlay
- Smooth fade-in/scale animation

### 4. Timer System ✓
- Timer starts when game board is displayed (after difficulty selection)
- **Pauses when success modal is shown**
- **Resumes when modal is closed**
- Stops completely when all pairs are matched
- Visual feedback:
  - Normal state: Blue color
  - Low time (<10s): Red color with pulsing animation
- Updates every second via `setInterval`

### 5. Scoring System ✓
**Points Awarded:**
- **+50 points** per correct match
- **+3 points per second** remaining (time bonus)
- **+100 points** for finishing with >50% time remaining (speed bonus)
- **+100 points maximum** for accuracy (reduced by 10 per mistake)

**Point Penalties:**
- **-2 points** per incorrect guess (mismatched pair)
- Score cannot go below 0

**Score Display:**
- Current score shown prominently during gameplay (green, 1.4rem font)
- Final score shown in end game modal with breakdown
- High scores saved to localStorage per difficulty

## 🎨 Brand Aesthetic - Wells Blue Bunny

### Color Scheme
```css
--primary-blue: #0066CC      /* Wells Blue Bunny primary */
--light-blue: #4A9FE8        /* Lighter accent */
--bunny-pink: #FF69B4        /* Fun, playful pink */
--cream-white: #FFF8F0       /* Ice cream white */
--ice-cream-yellow: #FFD700  /* Golden yellow */
```

### Visual Design
- Gradient backgrounds (light blue to pink)
- Rounded corners (12-24px border radius)
- Box shadows for depth
- Poppins font (modern, friendly)
- Ice cream emoji (🍦) on card backs
- Bunny emoji (🐰) in headers
- Shimmer animation on card backs

## 📊 Asset Integration

### CSV Parsing
- Loads `Images/wells-descriptions.csv` via Fetch API
- Parses CSV to extract:
  - Product Name (column 0)
  - Description (column 1)
  - Filename (column 3)
- Handles filename conversion (.jpg → .png)
- Maps CSV filenames to actual image files
- Fallback data if CSV fails to load

### Image Mapping
Handles filename discrepancies:
- CSV uses `.jpg` extensions → converted to `.png`
- Special case: `BreakfastPizzaPopsicle` → `reakfastPizzaPopsicle` (typo in actual file)
- Sundae files: `HotBeefSundae` → `HotBeef_Sundae.png`
- All 19 product images properly mapped

### Available Products
1. Dill Pickle Delight
2. Vegemite Dream
3. Sriracha Swirl
4. Fish Sauce Frosty
5. Toothpaste Treat
6. Grandma's Chicken Noodle Soup
7. White Castle Whirl
8. Mac n Cheese Moonpie
9. Breakfast Pizza Popsicle
10. Crab Rangoon Crunch
11. Fried Butter On-A-Stick
12. Bob Dog Delight
13. Hot Beef Sundae
14. Taco Salad Sundae
15. 7-Layer Salad Sundae
16. Ghost Pepper Fire
17. Extreme Espresso
18. Red White & Chew
19. Baby Food Bomb Pop

## 🎯 Game Flow

```
Start Screen (Difficulty Selection)
    ↓
[Easy] or [Hard] selected
    ↓
Game Board Created
    ↓
Timer Starts
    ↓
Player flips cards
    ↓
Match Found? 
    ├─ YES → Show Modal (Timer Pauses)
    │         ↓
    │      Close Modal (Timer Resumes)
    │         ↓
    │      +50 points
    │         ↓
    │      All matched? → End Game (Win)
    │
    └─ NO → -2 points
              ↓
           Cards flip back
              ↓
           Continue playing
    ↓
Timer reaches 0? → End Game (Loss)
    ↓
Show Final Score & High Score
    ↓
Play Again → Return to Difficulty Selection
```

## 🔧 Technical Implementation

### Key Functions
- `loadCSV()`: Async function to fetch and parse product data
- `createBoard()`: Generates shuffled card grid
- `flipCard()`: Handles card click events
- `checkForMatch()`: Validates if two cards match
- `showMatchModal()`: Displays success modal and pauses timer
- `pauseTimer()` / `resumeTimer()`: Timer control
- `startTimer()`: Interval-based countdown with pause support
- `endGame()`: Calculates final score with bonuses
- `updateHighScores()`: LocalStorage persistence

### Shuffle Algorithm
Uses Fisher-Yates shuffle for true randomness:
```javascript
for (let i = shuffled.length - 1; i > 0; i--) {
    const j = Math.floor(Math.random() * (i + 1));
    [shuffled[i], shuffled[j]] = [shuffled[j], shuffled[i]];
}
```

### State Management
```javascript
let hasFlippedCard = false;    // First card flipped?
let lockBoard = false;          // Prevent clicks during check
let firstCard, secondCard;      // Card references
let score = 0;                  // Current score
let timeLeft = 0;               // Seconds remaining
let timerId;                    // setInterval reference
let matchesFound = 0;           // Pairs matched
let pairsToMatch = 0;           // Total pairs (8 or 18)
let currentDifficulty = '';     // 'easy' or 'hard'
let incorrectGuesses = 0;       // Mistake counter
let timerPaused = false;        // Timer pause state
```

## 🎮 User Experience Enhancements

1. **Visual Feedback**
   - Card flip animations (3D transform)
   - Pop animation on match
   - Shimmer effect on card backs
   - Pulsing timer when low
   - Celebration emoji in modal

2. **Accessibility**
   - High contrast colors
   - Large, readable fonts
   - Clear button states
   - Descriptive alt text on images

3. **Responsive Design**
   - Adapts to different screen sizes
   - Padding prevents edge clipping
   - Centered layout

4. **Performance**
   - Pure CSS animations (GPU accelerated)
   - Efficient event listeners
   - Minimal DOM manipulation
   - LocalStorage for persistence

## 📱 Browser Testing Recommendations

Test in:
- Chrome/Edge (Chromium)
- Firefox
- Safari (macOS/iOS)
- Mobile browsers (responsive design)

## 🚀 Deployment

Simply upload these files to a web server:
- `index.html` (main game file)
- `Images/` directory (all 19 PNG files + CSV)
- `README.md` (documentation)

No build process or dependencies required!

---

**Game is ready to play!** Open `index.html` in any modern browser.

