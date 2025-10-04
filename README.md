# Wells Blue Bunny Memory Match Game 🐰🍦

A custom memory card-matching game featuring Wells Enterprises' Blue Bunny ice cream products with tongue-in-cheek descriptions.

## 🎮 Game Features

### Difficulty Levels
- **Easy Mode (4x4)**: 16 cards total, 8 matched pairs, 2 minutes to complete
- **Hard Mode (6x6)**: 36 cards total, 18 matched pairs, 4 minutes to complete

### Gameplay Mechanics
- Standard memory game rules: flip two cards at a time to find matching pairs
- Cards flip with smooth animations when clicked
- Non-matching pairs flip back face-down after a brief delay
- Matched pairs remain face-up and are highlighted

### Success Modal System
When you successfully match a pair:
- A modal popup immediately displays with:
  - A larger view of the matched product image
  - The product name
  - The tongue-in-cheek product description
- **Timer pauses** while the modal is displayed
- Click "Continue Playing" button or anywhere on the modal to close it
- Timer resumes when modal is closed

### Scoring System

#### Points Earned:
- **+50 points** for each correct match
- **Time Bonus**: +3 points per second remaining when you win
- **Speed Demon Bonus**: +100 points if you finish with more than 50% time remaining
- **Accuracy Bonus**: Up to +100 points based on how few mistakes you make

#### Point Penalties:
- **-2 points** for each incorrect guess (mismatched pair)

### Timer System
- Timer starts when the game board is first displayed (after difficulty selection)
- **Timer pauses** when a success modal is shown
- **Timer resumes** when the modal is closed
- Timer stops completely when all pairs have been matched
- Timer turns red and pulses when less than 10 seconds remain

### High Score Tracking
- Separate high scores for Easy and Hard modes
- High scores are saved locally in your browser
- New high score achievements are celebrated in the end game screen

## 🎨 Design Features

### Wells Blue Bunny Branding
- Custom color scheme matching Blue Bunny brand colors:
  - Primary Blue (#0066CC)
  - Light Blue (#4A9FE8)
  - Bunny Pink (#FF69B4)
  - Cream White (#FFF8F0)
  - Ice Cream Yellow (#FFD700)
- Gradient backgrounds for a premium feel
- Ice cream cone emoji (🍦) on card backs
- Bunny emoji (🐰) in headers

### Visual Effects
- Smooth card flip animations
- Shimmer effect on card backs
- Pop animation when cards are matched
- Pulsing timer when time is running low
- Celebration animation in success modal
- Gradient buttons with hover effects

## 📦 Assets

### Product Images
19 unique ice cream product images located in `/Images` directory:
- Flavors (Dill Pickle Delight, Vegemite Dream, Sriracha Swirl, etc.)
- Novelty Treats (White Castle Whirl, Mac n Cheese Moonpie, etc.)
- Sundae Series (Hot Beef Sundae, Taco Salad Sundae, etc.)
- Bomb Pops (Ghost Pepper Fire, Extreme Espresso, etc.)

### Product Data
CSV file (`Images/wells-descriptions.csv`) containing:
- Product names
- Tongue-in-cheek descriptions
- Product types
- Image filenames

## 🚀 How to Play

1. **Open `index.html`** in a web browser
2. **Select difficulty**: Choose Easy (4x4) or Hard (6x6) mode
3. **Match pairs**: Click cards to flip them and find matching pairs
4. **Read descriptions**: When you match a pair, enjoy the humorous product description
5. **Beat the clock**: Complete all matches before time runs out
6. **Maximize your score**: Match quickly and accurately for bonus points!

## 🛠️ Technical Details

### Technologies Used
- Pure HTML5, CSS3, and JavaScript (no external dependencies)
- CSS Grid for responsive card layout
- CSS Animations and Transitions
- LocalStorage for high score persistence
- Fetch API for CSV data loading

### Browser Compatibility
- Modern browsers (Chrome, Firefox, Safari, Edge)
- Requires JavaScript enabled
- Responsive design adapts to different screen sizes

## 📝 Game Rules Summary

1. Click any card to flip it over
2. Click a second card to try to find a match
3. If cards match:
   - Success modal appears with product details
   - Timer pauses
   - You earn +50 points
   - Cards stay flipped
4. If cards don't match:
   - You lose -2 points
   - Cards flip back after 1.2 seconds
5. Match all pairs before time runs out to win!

## 🏆 Scoring Strategy

To achieve the highest score:
- **Work quickly** to maximize time bonus (3 points/second)
- **Be accurate** to avoid -2 point penalties
- **Finish fast** to earn the +100 speed demon bonus
- **Remember card positions** to reduce incorrect guesses

### Maximum Possible Scores:
- **Easy Mode**: Base (400) + Time Bonus (360) + Speed Bonus (100) + Accuracy Bonus (100) = **960 points**
- **Hard Mode**: Base (900) + Time Bonus (720) + Speed Bonus (100) + Accuracy Bonus (100) = **1,820 points**

## 🎯 Future Enhancement Ideas

- Sound effects for card flips and matches
- Multiplayer mode
- Additional difficulty levels
- Leaderboard system
- Mobile touch optimization
- Accessibility improvements (keyboard navigation, screen reader support)
- Animation preferences for reduced motion

## 📄 License

Created for Wells Enterprises - Blue Bunny Ice Cream

---

**Enjoy the game and discover all the wild and wacky ice cream flavors!** 🍦🎉

