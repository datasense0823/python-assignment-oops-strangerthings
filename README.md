# Stranger Things: OOP Battleground Assignment (Python)

## 🌌 Background: The World of Stranger Things

In the quiet town of **Hawkins**, Indiana, strange portals have opened to the **Upside Down**, a terrifying alternate dimension. This rift has unleashed powerful and terrifying entities—**Demogorgon**, **Mind Flayer**, and **Vecna**—into the real world.

A group of young heroes—**Eleven**, **Dustin**, **Lucas**, **Max**, and others—have taken it upon themselves to protect Hawkins. With their unique powers and teamwork, they must fight to close the rift and defeat these supernatural enemies once and for all.

---

## 📚 Case Study: The Digital Battleground of Hawkins

You are tasked with creating a **Python simulation** of this supernatural battle using the **4 Pillars of Object-Oriented Programming**:
- **Encapsulation**
- **Inheritance**
- **Polymorphism**
- **Abstraction**

You will model heroes and enemies as classes, simulate battle interactions, and use OOP design patterns to ensure reusability, modularity, and clarity.

---

## 🎯 Assignment Objectives

Build a battle simulation between heroes and enemies with:

- Clear OOP design using **abstract base classes**, **method overriding**, and **private state**
- Multiple character types with specialized powers
- A centralized battle manager controlling turn-by-turn logic
- Console-based battle logs with dynamic storytelling

---

## ⚔️ Battle System Design

### 🎮 Game Setup

- **Each character (Hero or Enemy)** is an instance of a class that inherits from an abstract base class `Character`.
- Heroes and enemies are stored in two lists: `heroes[]` and `enemies[]`.
- The `BattleManager` class handles:
  - Turn-based logic
  - Health updates
  - Action narration
  - Declaring the winner

---

### 🔁 Turn-by-Turn Mechanics

- Each **turn** consists of:
  1. A **Hero's move**: attack a random or chosen enemy
  2. An **Enemy's move**: retaliate on a random living hero
- After each turn:
  - Damage is applied using `take_damage()`
  - Dead characters are removed from battle
- Battle continues until:
  - One side is completely wiped out

---

### 🧪 Sample Battle Flow

```text
🎮 The Battle Begins: Hawkins vs The Upside Down

👩‍🔬 Eleven uses Telekinesis on Demogorgon!
💥 Demogorgon takes 40 damage. (HP left: 60)

👹 Demogorgon slashes Max with claws!
💥 Max takes 25 damage. (HP left: 75)

🧢 Dustin throws Sonic Boom Gadget at Vecna!
💥 Vecna takes 35 damage. (HP left: 65)

🧠 Vecna attacks Eleven with psychic blast!
💥 Eleven takes 30 damage. (HP left: 70)

...

❌ Mind Flayer has been defeated!
🏆 HEROES WIN! Hawkins is safe... for now.
```


# Class Design Breakdown

## 1. Abstraction

```python
from abc import ABC, abstractmethod

class Character(ABC):
    def __init__(self, name, health, power):
        self._name = name
        self._health = health
        self._power = power

    @abstractmethod
    def attack(self, opponent): pass

    def take_damage(self, amount):
        self._health -= amount

    def is_alive(self):
        return self._health > 0

```

## 2. 🧬 Inheritance & 3. 🔁 Polymorphism

```python

class Hero(Character):
    def attack(self, opponent):
        print(f"{self._name} attacks {opponent._name} with hero power!")
        opponent.take_damage(self._power)

class Eleven(Hero):
    def attack(self, opponent):
        print(f"👩‍🔬 {self._name} uses Telekinesis on {opponent._name}!")
        opponent.take_damage(self._power + 10)

class Vecna(Character):
    def attack(self, opponent):
        print(f"🧠 {self._name} unleashes a psychic blast at {opponent._name}!")
        opponent.take_damage(self._power + 5)

```

## BattleExample

```python

import random

class BattleManager:
    def __init__(self, heroes, enemies):
        self.heroes = heroes
        self.enemies = enemies

    def run_battle(self):
        print("🎮 The Battle Begins: Hawkins vs The Upside Down\n")
        turn = 1
        while self.heroes and self.enemies:
            print(f"--- Turn {turn} ---")
            for hero in self.heroes:
                if self.enemies:
                    target = random.choice(self.enemies)
                    hero.attack(target)
                    if not target.is_alive():
                        print(f"❌ {target._name} has been defeated!")
                        self.enemies.remove(target)
            for enemy in self.enemies:
                if self.heroes:
                    target = random.choice(self.heroes)
                    enemy.attack(target)
                    if not target.is_alive():
                        print(f"❌ {target._name} has been knocked out!")
                        self.heroes.remove(target)
            print()
            turn += 1
        if self.heroes:
            print("🏆 HEROES WIN! Hawkins is safe... for now.")
        else:
            print("💀 ENEMIES WIN! The Upside Down has taken over.")

```

# Deliverables Checklist

| Task                      | Description                                     | Done |
| ------------------------- | ----------------------------------------------- | ---- |
| `Character` Abstract Base | Includes health, name, power, attack method     | \[ ] |
| Hero Subclasses           | At least 3: Eleven, Dustin, Max                 | \[ ] |
| Enemy Subclasses          | At least 3: Demogorgon, Mind Flayer, Vecna      | \[ ] |
| Encapsulated Properties   | All internal variables private                  | \[ ] |
| Polymorphic `attack()`    | Different logic for each character              | \[ ] |
| `BattleManager` Class     | Handles turn system and prints logs             | \[ ] |
| `main.py`                 | Initializes all objects and runs the simulation | \[ ] |


# Project Structure

stranger_things_battle/
│
├── characters/
│   ├── base.py           # Character (abstract class)
│   ├── heroes.py         # Eleven, Dustin, Lucas, etc.
│   └── enemies.py        # Demogorgon, Vecna, etc.
│
├── battle_manager.py     # Main battle logic
├── main.py               # Entry point
└── README.md             # You are here


# Bonus Challenges

1. Add elemental powers (fire, lightning, psychic)

2. Allow characters to “heal” on their turn

3. Introduce levels or experience points

4. Log results to a file

# Summary

This assignment gives you a fun, creative way to learn core OOP concepts. You’ll learn to think in terms of objects, behaviors, and interactions, just like real-world systems.

OOP isn’t just about classes. It’s about designing programs like stories—with characters, purpose, and rules.

**Good luck, and remember:**

**Friends don’t lie. But code might. So debug. 😄**
