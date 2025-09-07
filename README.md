# 🌲 Outdoor Survival V1

A **browser-based survival simulation** built with plain **HTML, CSS, and JavaScript**.  
This version (`V1`) is self-contained in a single `index.html` file with inline styles and scripts.

---

## 🗂 Project Structure

- `index.html` → Contains HTML, CSS, and JavaScript in a single file.  
- No external dependencies or assets — everything runs fully client-side.  

---

## 🧩 Core Components

### HTML
- **Stats Panel** – HP, Hunger, Thirst, and Stamina (progress bars).  
- **Resources Panel** – Food, Water, and Materials (Mats).  
- **Build Status** – Shelter, Fire Pit, Signal Fire & Help Sign.  
- **Rescue Chance** – dynamically updated based on fire.  
- **Actions Panel** – checkboxes for actions (foraging, eating, drinking, building, resting, etc.).  
- **Flavor Text** – feedback about current action/state.  

### CSS
- Responsive layout with simple styling.  
- Flexbox used for stat/resource rows.  
- Progress bars styled with colors for quick readability:  
  - HP → red  
  - Hunger → yellow  
  - Thirst → blue  
  - Stamina → green  
  - Fire → orange  
  - Build progress → brown  

### JavaScript
All game logic is inline in a `<script>` tag.  

**Game State Variables**  
- `hp`, `hunger`, `thirst`, `stamina` (player stats).  
- `food`, `water`, `mats` (resources).  
- `shelterBuilt`, `firePitBuilt`, `signalFireBuilt` (structures).  
- `rescueChance`, `rescueFireBonus`, `rescueUnlocked` (rescue system).  

**Actions Object**  
    let action = {
      forageFood: false,
      eatFood: false,
      gatherWater: false,
      drinkWater: false,
      gatherMats: false,
      rest: false,
      build: false
    };

Only **one action** can be active at a time.  

**Build System**  
- Sequential order:  
  1. Shelter → improves stamina recovery.  
  2. Fire Pit → improves effectiveness of food and water.  
  3. Signal Fire & Help Sign → unlocks rescue chance.  
- Each has a `mats` cost, `time` requirement, and `effect()` callback.  

**Rescue Mechanics**  
- Base chance unlocked at **1%** once Signal Fire is built.  
- Fire bonus increases rescue chance gradually while burning.  
- Roll happens once per second to check if rescue occurs.  

**Main Loop** (runs every 500ms)  
- Hunger & Thirst decrease gradually.  
- HP decreases if hunger or thirst reach zero.  
- HP regenerates slowly if conditions are good.  
- Stamina is consumed for gathering/building and restored by resting.  
- Resources (food, water, mats) are gathered/consumed based on actions.  
- Build progress advances if mats + stamina are available.  
- Fire timer decreases over time; stoking extends it.  
- Rescue chance recalculates each tick.  
- Game ends if HP hits 0 (death) or rescue roll succeeds.  

---

## 🕹️ Minimal Gameplay Notes

- Only one action can be toggled at a time.  
- Hunger & Thirst drain passively; neglecting them leads to HP loss.  
- Mats are needed both for **building** and **stoking fire**.  
- Shelter improves rest; Fire Pit improves food/water effects.  
- Victory: get rescued.  
- Defeat: die when HP reaches 0.  

---

## 🔧 Extending the Game

Some possible developer extensions:  
- Modularize into separate JS, CSS, and HTML files.  
- Adjust balance values (stat decay, build costs, rescue probabilities).  
- Improve UI (icons, animations, better feedback).  
- Add systems (weather, random events, crafting, animals).  
- Add persistence via `localStorage`.  

---

## 🚀 Running

No setup required. Just open `index.html` in any modern browser:

    open index.html   # or double-click

---

## 📜 License

MIT License – free to use, modify, and distribute.
