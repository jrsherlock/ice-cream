# Quick Start Guide - Wells Blue Bunny Memory Match

## 🚀 Running the Game

### Option 1: Direct File Open (Simplest)
1. Navigate to the project folder
2. Double-click `index.html`
3. Game opens in your default browser
4. Start playing!

**Note:** Some browsers may block CSV loading from `file://` protocol. If images don't load, use Option 2.

### Option 2: Local Web Server (Recommended)
```bash
# Navigate to project directory
cd /path/to/Wells-memory

# Start a simple web server (Python 3)
python3 -m http.server 8000

# Or with Python 2
python -m SimpleHTTPServer 8000

# Or with Node.js (if you have http-server installed)
npx http-server -p 8000
```

Then open your browser to: **http://localhost:8000**

## 🎮 How to Play

### Step 1: Choose Your Difficulty
- **🍦 Easy Mode (4x4)**: Perfect for beginners, 2 minutes
- **🔥 Hard Mode (6x6)**: Challenge yourself, 4 minutes

### Step 2: Match the Pairs
1. Click any card to flip it over
2. Click another card to find its match
3. If they match:
   - 🎉 Success modal appears
   - Read the funny product description
   - Click "Continue Playing" or anywhere on the modal
   - Earn +50 points!
4. If they don't match:
   - Cards flip back after 1.2 seconds
   - Lose -2 points
   - Try to remember where they were!

### Step 3: Beat the Clock
- Match all pairs before time runs out
- Timer pauses when you're reading product descriptions
- Finish fast for bonus points!

### Step 4: Maximize Your Score
- **Speed**: Finish quickly for time bonus (+3 pts/second)
- **Accuracy**: Avoid mistakes for accuracy bonus (up to +100)
- **Efficiency**: Finish with >50% time left for speed demon bonus (+100)

## 🏆 Scoring Breakdown

| Action | Points |
|--------|--------|
| Correct Match | +50 |
| Incorrect Guess | -2 |
| Time Bonus (Win) | +3 per second remaining |
| Speed Demon Bonus | +100 (if >50% time left) |
| Accuracy Bonus | +100 max (minus 10 per mistake) |

### Example Winning Score (Easy Mode):
- 8 matches × 50 = **400 points**
- 60 seconds left × 3 = **+180 points**
- Speed bonus = **+100 points**
- No mistakes = **+100 points**
- **Total: 780 points!**

## 🎯 Pro Tips

1. **Focus on Memory**: Try to remember card positions even when they flip back
2. **Work Systematically**: Start from one corner and work your way across
3. **Speed vs Accuracy**: Balance quick matching with careful selection
4. **Use the Modal Time**: While reading descriptions, plan your next moves
5. **Practice**: Play Easy mode first to learn the products

## 🐛 Troubleshooting

### Images Not Loading?
- **Solution 1**: Use a local web server (see Option 2 above)
- **Solution 2**: Check that all files are in the correct locations:
  ```
  Wells-memory/
  ├── index.html
  └── Images/
      ├── wells-descriptions.csv
      ├── DillPickleDelight_Flavor.png
      ├── VegemiteDream_Flavor.png
      └── ... (all 19 PNG files)
  ```

### CSV Not Loading?
- Open browser console (F12) and check for errors
- Verify `Images/wells-descriptions.csv` exists
- Make sure you're using a web server (not file://)

### Game Not Starting?
- Ensure JavaScript is enabled in your browser
- Try a different browser (Chrome, Firefox, Safari, Edge)
- Clear browser cache and reload

### Cards Not Flipping?
- Check browser console for JavaScript errors
- Ensure you're clicking on the card area
- Wait for previous animation to complete

## 📱 Mobile Play

The game works on mobile devices:
- Tap cards instead of clicking
- Landscape orientation recommended for Hard mode
- May need to zoom out on smaller screens

## 🎨 Customization Ideas

Want to modify the game? Here are some easy tweaks:

### Change Timer Duration
In `index.html`, find the `initGame` function:
```javascript
if (difficulty === 'easy') {
    timeLeft = 120; // Change this number (seconds)
} else {
    timeLeft = 240; // Change this number (seconds)
}
```

### Adjust Scoring
Find the scoring constants:
```javascript
score += 50;  // Match bonus
score -= 2;   // Incorrect penalty
bonusPoints = timeLeft * 3;  // Time bonus multiplier
```

### Change Colors
In the CSS `:root` section:
```css
--primary-blue: #0066CC;
--bunny-pink: #FF69B4;
/* etc. */
```

## 📊 High Scores

High scores are saved in your browser's localStorage:
- Separate scores for Easy and Hard modes
- Persist across browser sessions
- Specific to each browser/device

To reset high scores:
1. Open browser console (F12)
2. Type: `localStorage.clear()`
3. Refresh the page

## 🎉 Have Fun!

Enjoy discovering all the wild and wacky Wells Blue Bunny ice cream flavors:
- Dill Pickle Delight 🥒
- Grandma's Chicken Noodle Soup 🍜
- Ghost Pepper Fire 🌶️
- And 16 more crazy creations!

**Good luck and happy matching!** 🐰🍦

