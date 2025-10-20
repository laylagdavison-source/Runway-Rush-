# Runway Rush

**Runway Rush** is a fast-paced collectible endless-runner style game made with **MakeCode Arcade**.  
The player controls a fashion-forward character dodging through a scrolling runway, collecting stylish items like dresses, lipstick, and heels — all while racing against time!

---

## Gameplay Overview

When the game starts, a **countdown (3…2…1)** appears before the action begins.  
The background scrolls continuously to create a runway effect while collectible items spawn randomly for the player to grab.

Each time the player collects an item, their **score increases by +1**, and a satisfying **“ding” sound** plays.

Your goal?  
Collect as many fashion items as possible before the runway ends!

---

## Features

- **Starting Countdown** – The game flashes “3”, “2”, “1” before gameplay begins.  
- **Smooth Scrolling Background** – Two background images loop endlessly to simulate a moving runway.  
- **Collectible System** – Randomized fashion items (dress, lipstick, shirt, glasses, heels, bow, shorts) appear periodically.  
- **Score Tracker** – Player’s score updates in real time.  
- **Sound Effects** – Positive audio feedback when items are collected.  
- **Simple Controls** – Move the character **up and down** to collect items and avoid missing them.

---

## Controls

| Action | Key | Description |
|--------|-----|-------------|
| Move Up | ⬆️ | Move player up the runway |
| Move Down | ⬇️ | Move player down the runway |

---

## How It Works

1. **Sprite Setup:**  
   - The player sprite represents the character.  
   - Fashion items are stored in a list of collectables.  
   - Background sprites scroll at a constant speed.

2. **Game Loop:**  
   - Two background sprites alternate to create a continuous scrolling effect.  
   - A timed update spawns random collectible sprites from the list.  
   - The last two spawned items are tracked to avoid repetition.

3. **Collision Logic:**  
   - When the player overlaps with a collectible, the item resets off-screen, velocity stops, and the score increases.

4. **Visual & Audio Feedback:**  
   - The game displays dynamic text for countdowns and plays sound effects on item collection.

---

## Key Code Sections

- **Countdown Start:**
  ```python
  mySprite.say_text("3")
  pause(1000)
  mySprite.say_text("2")
  pause(1000)
  mySprite.say_text("1")
  pause(1000)
  mySprite.say_text("")
  ```
- **Collectible Collision:**
  ```python
  def on_on_overlap(player2, collectable):
      collectable.set_position(scene.screen_width() + 16, 0)
      collectable.set_velocity(0, 0)
      info.change_score_by(1)
      music.ba_ding.play()
  
  sprites.on_overlap(SpriteKind.player, SpriteKind.Collectable, on_on_overlap)
  ```
- **Random Spawning:**
  ```python
  def on_update_interval():
      global n, collectable_sprite
      n = randint(0, len(collectables) - 1)
      while last_two_sprites.index_of(n) >= 0:
          n = randint(0, len(collectables) - 1)
      last_two_sprites[1] = last_two_sprites[0]
      last_two_sprites[0] = n
      collectable_sprite = collectables[n]
      collectable_sprite.set_position(scene.screen_width() + 16,
          randint(16, scene.screen_height() - 16))
      collectable_sprite.vx = bgSprite1.vx
  
  game.on_update_interval(1500, on_update_interval)
  ```

## How to run the game
- Go to https://arcade.makecode.com/
- Click *New Project* and select Python mode

## Assets
- **Custom background**: scrolling runway
- **Player sprite**: custom fashion character
- **Collectibles**: dress, lipstick, shirt, glasses, heels, bow, shorts

## Future Improvements
- Add obstacles (e.g., paparazzi or flashing cameras)
- Introduce levels or timed challenges
- Add combo bonuses for collecting themed sets
- Include power-ups or speed boosts

## Created By
Layla Davison :)
