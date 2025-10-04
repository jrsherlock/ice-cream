# Wells Blue Bunny Memory Match - Testing Checklist

## 🧪 Pre-Launch Testing Checklist

Use this checklist to verify all game features are working correctly.

---

## 1. Initial Load & Setup

### Page Load
- [ ] Page loads without errors
- [ ] No console errors in browser developer tools (F12)
- [ ] All CSS styles applied correctly
- [ ] Fonts loaded (Poppins)
- [ ] Background gradient visible

### Difficulty Selection Screen
- [ ] "Wells Blue Bunny Memory Match" title displays with bunny emoji
- [ ] Easy Mode button visible and styled correctly
- [ ] Hard Mode button visible and styled correctly
- [ ] High scores display (initially 0)
- [ ] Buttons have hover effects
- [ ] Buttons are clickable

---

## 2. Easy Mode (4x4) Testing

### Game Initialization
- [ ] Clicking "Easy Mode" starts the game
- [ ] Screen transitions smoothly to game board
- [ ] 4x4 grid displays (16 cards total)
- [ ] All cards show ice cream emoji on back
- [ ] Timer starts at 120 seconds
- [ ] Score starts at 0
- [ ] Timer counts down every second

### Card Interaction
- [ ] Cards flip when clicked (smooth animation)
- [ ] Card shows product image when flipped
- [ ] Cannot click same card twice
- [ ] Can flip second card after first
- [ ] Cards lock during match checking

### Matching - Success Case
- [ ] When two cards match:
  - [ ] Success modal appears immediately
  - [ ] Modal shows celebration emoji (🎉)
  - [ ] Modal shows larger product image
  - [ ] Modal shows product name (pink text)
  - [ ] Modal shows product description (italic)
  - [ ] **Timer pauses** (verify number stops changing)
  - [ ] "Continue Playing" button visible
- [ ] Clicking "Continue Playing" closes modal
- [ ] **Timer resumes** after closing modal
- [ ] Matched cards remain face-up
- [ ] Matched cards have pop animation
- [ ] Score increases by +50 points
- [ ] Cannot click matched cards again

### Matching - Failure Case
- [ ] When two cards don't match:
  - [ ] Score decreases by -2 points (or stays at 0)
  - [ ] Cards remain flipped briefly (1.2 seconds)
  - [ ] Cards flip back face-down
  - [ ] Can continue playing immediately after

### Timer Behavior
- [ ] Timer counts down continuously
- [ ] Timer pauses when success modal shown
- [ ] Timer resumes when modal closed
- [ ] Timer turns red when < 10 seconds
- [ ] Timer pulses when < 10 seconds
- [ ] Timer stops at 0

### Winning the Game
- [ ] When all 8 pairs matched:
  - [ ] End game modal appears
  - [ ] Title shows "You Win!" with emojis
  - [ ] Message shows number of matches
  - [ ] Message shows time remaining
  - [ ] Bonus points breakdown displayed
  - [ ] Final score calculated correctly:
    - [ ] Base: 8 × 50 = 400 points
    - [ ] Time bonus: seconds × 3
    - [ ] Speed bonus: +100 if >60 seconds left
    - [ ] Accuracy bonus: 100 - (mistakes × 10)
  - [ ] High score updated if beaten
  - [ ] "NEW HIGH SCORE" message if applicable
  - [ ] "Play Again" button visible

### Losing the Game (Time Out)
- [ ] When timer reaches 0:
  - [ ] End game modal appears
  - [ ] Title shows "Time's Up!"
  - [ ] Message shows pairs matched out of total
  - [ ] Final score shown (no bonuses)
  - [ ] "Play Again" button visible

### Play Again
- [ ] Clicking "Play Again" returns to difficulty screen
- [ ] High score updated on difficulty screen
- [ ] Can start new game

---

## 3. Hard Mode (6x6) Testing

### Game Initialization
- [ ] Clicking "Hard Mode" starts the game
- [ ] 6x6 grid displays (36 cards total)
- [ ] Timer starts at 240 seconds
- [ ] Score starts at 0

### Gameplay
- [ ] All card interactions work (same as Easy)
- [ ] All matching logic works (same as Easy)
- [ ] Timer pause/resume works (same as Easy)
- [ ] 18 pairs to match

### Winning
- [ ] Final score calculated correctly:
  - [ ] Base: 18 × 50 = 900 points
  - [ ] Time bonus: seconds × 3
  - [ ] Speed bonus: +100 if >120 seconds left
  - [ ] Accuracy bonus: 100 - (mistakes × 10)
- [ ] High score tracked separately from Easy mode

---

## 4. CSV Data Loading

### Product Data
- [ ] Open browser console (F12)
- [ ] Check for message: "Loaded X products from CSV"
- [ ] Verify X = 19 or more
- [ ] No CSV loading errors in console

### Product Display
- [ ] Product images load correctly
- [ ] Product names display correctly in modal
- [ ] Product descriptions display correctly in modal
- [ ] All 19 products can appear in game:
  1. [ ] Dill Pickle Delight
  2. [ ] Vegemite Dream
  3. [ ] Sriracha Swirl
  4. [ ] Fish Sauce Frosty
  5. [ ] Toothpaste Treat
  6. [ ] Grandma's Chicken Noodle Soup
  7. [ ] White Castle Whirl
  8. [ ] Mac n Cheese Moonpie
  9. [ ] Breakfast Pizza Popsicle
  10. [ ] Crab Rangoon Crunch
  11. [ ] Fried Butter On-A-Stick
  12. [ ] Bob Dog Delight
  13. [ ] Hot Beef Sundae
  14. [ ] Taco Salad Sundae
  15. [ ] 7-Layer Salad Sundae
  16. [ ] Ghost Pepper Fire
  17. [ ] Extreme Espresso
  18. [ ] Red White & Chew
  19. [ ] Baby Food Bomb Pop

---

## 5. Scoring System Verification

### Test Scenario 1: Perfect Easy Game
- [ ] Start Easy mode
- [ ] Match all 8 pairs without mistakes
- [ ] Finish with >60 seconds remaining
- [ ] Expected score: ~760-960 points
  - [ ] Base: 400
  - [ ] Time: 180-360
  - [ ] Speed: 100
  - [ ] Accuracy: 100

### Test Scenario 2: Game with Mistakes
- [ ] Start Easy mode
- [ ] Make 3 incorrect guesses
- [ ] Score should decrease by 6 points total
- [ ] Accuracy bonus reduced by 30 points

### Test Scenario 3: Slow Completion
- [ ] Start Easy mode
- [ ] Finish with <60 seconds remaining
- [ ] No speed demon bonus (+100)
- [ ] Lower time bonus

---

## 6. Timer Pause System (Critical Feature)

### Detailed Timer Pause Test
1. [ ] Start a game
2. [ ] Note the current time (e.g., 115 seconds)
3. [ ] Match a pair
4. [ ] **Verify timer stops counting** (number frozen)
5. [ ] Wait 5 seconds while modal is open
6. [ ] Close modal
7. [ ] **Verify timer resumes from same number** (e.g., still 115)
8. [ ] Verify timer continues counting down

### Multiple Pause Test
- [ ] Match 3 pairs in a row
- [ ] Verify timer pauses for each modal
- [ ] Verify timer resumes each time
- [ ] Verify total time is preserved

---

## 7. High Score Persistence

### LocalStorage Test
- [ ] Complete a game with score X
- [ ] Verify high score shows X on difficulty screen
- [ ] Close browser completely
- [ ] Reopen game
- [ ] Verify high score still shows X
- [ ] Beat high score with score Y
- [ ] Verify high score updates to Y

### Separate Difficulty Scores
- [ ] Set Easy mode high score
- [ ] Set Hard mode high score
- [ ] Verify both are tracked independently
- [ ] Verify correct score shows for each difficulty

---

## 8. Visual & Animation Testing

### Card Animations
- [ ] Card flip is smooth (0.6s)
- [ ] 3D flip effect works
- [ ] Matched cards have pop animation
- [ ] No animation glitches

### Modal Animations
- [ ] Modal fades in smoothly
- [ ] Modal scales up smoothly
- [ ] Modal fades out smoothly
- [ ] No jarring transitions

### Timer Visual Effects
- [ ] Timer is blue normally
- [ ] Timer turns red at <10 seconds
- [ ] Timer pulses at <10 seconds
- [ ] Pulse animation is smooth

### Card Back Effects
- [ ] Ice cream emoji visible
- [ ] Shimmer animation plays
- [ ] Gradient background visible
- [ ] Border styling correct

---

## 9. Responsive Design

### Desktop
- [ ] Game centered on screen
- [ ] All elements visible
- [ ] No horizontal scroll
- [ ] Buttons properly sized

### Tablet (if applicable)
- [ ] Layout adapts appropriately
- [ ] Cards remain clickable
- [ ] Text remains readable

### Mobile (if applicable)
- [ ] Game playable on mobile
- [ ] Cards tappable
- [ ] Modals display correctly
- [ ] Text readable

---

## 10. Browser Compatibility

Test in multiple browsers:

### Chrome
- [ ] All features work
- [ ] No console errors
- [ ] Animations smooth

### Firefox
- [ ] All features work
- [ ] No console errors
- [ ] Animations smooth

### Safari
- [ ] All features work
- [ ] No console errors
- [ ] Animations smooth

### Edge
- [ ] All features work
- [ ] No console errors
- [ ] Animations smooth

---

## 11. Edge Cases & Error Handling

### Rapid Clicking
- [ ] Cannot flip more than 2 cards at once
- [ ] Board locks during match check
- [ ] No duplicate flips

### Modal Interaction
- [ ] Can close modal by clicking overlay
- [ ] Can close modal by clicking button
- [ ] Cannot interact with cards while modal open

### CSV Loading Failure
- [ ] If CSV fails, fallback data loads
- [ ] Game still playable
- [ ] Console shows appropriate message

---

## 12. Performance

### Load Time
- [ ] Page loads in <2 seconds
- [ ] Images load progressively
- [ ] No lag on initial render

### Gameplay Performance
- [ ] Card flips are smooth (60fps)
- [ ] No lag when clicking cards
- [ ] Timer updates smoothly
- [ ] Score updates instantly

### Memory Usage
- [ ] No memory leaks (check dev tools)
- [ ] Can play multiple games without issues
- [ ] Browser doesn't slow down

---

## ✅ Final Verification

- [ ] All critical features working
- [ ] No console errors
- [ ] All requirements met
- [ ] Game is fun and engaging
- [ ] Ready for deployment

---

## 🐛 Bug Reporting Template

If you find any issues, document them as follows:

**Bug Description:**
[What went wrong?]

**Steps to Reproduce:**
1. [First step]
2. [Second step]
3. [etc.]

**Expected Behavior:**
[What should happen?]

**Actual Behavior:**
[What actually happened?]

**Browser/Device:**
[Chrome 120 on macOS, etc.]

**Screenshots:**
[If applicable]

---

## 📊 Test Results Summary

**Date Tested:** _______________

**Tester Name:** _______________

**Total Tests:** _____ / _____

**Pass Rate:** _____%

**Critical Issues:** _____

**Minor Issues:** _____

**Status:** ☐ Ready for Production  ☐ Needs Fixes

**Notes:**
_________________________________
_________________________________
_________________________________

