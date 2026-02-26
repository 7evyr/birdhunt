```python
import time
import random


# ----------------------------
# Utility / UI helpers
# ----------------------------
def clear_screen():
    # Simple, cross-platform-ish clear without importing os
    print("\n" * 50)


def slow_print(text, delay=0.015):
    for ch in text:
        print(ch, end="", flush=True)
        time.sleep(delay)
    print()


def bar(current, maximum, width=18, fill="█", empty="░"):
    current = max(0, min(current, maximum))
    filled = int((current / maximum) * width) if maximum else 0
    return fill * filled + empty * (width - filled)


def clamp_int(n: float) -> int:
    return int(n) if n > 0 else 0


def choice_menu(prompt, options):
    """
    options: list of (key, label)
    returns key
    """
    keys = {k.lower() for k, _ in options}
    while True:
        print(prompt)
        for k, label in options:
            print(f"  [{k}] {label}")
        ans = input("> ").strip().lower()
        if ans in keys:
            return ans
        print("Invalid choice. Try again.\n")


def prompt_action():
    while True:
        action = input("Your move (shoot/reload/scan): ").strip().lower()
        if action in ("shoot", "reload", "scan"):
            return action
        print("Invalid action. Type: shoot, reload, or scan.")


# ----------------------------
# Flavor generation
# ----------------------------
WEATHERS = [
    ("Clear sky", 0.72, 0.62),
    ("Light breeze", 0.70, 0.60),
    ("Overcast", 0.68, 0.58),
    ("Foggy", 0.64, 0.54),
    ("Drizzle", 0.66, 0.56),
    ("Windy", 0.62, 0.52),
]

LOCATIONS = [
    "pine ridge",
    "marsh edge",
    "open field",
    "lakeside trail",
    "old orchard",
    "rocky hillside",
]

BIRDS = [
    ("sparrow", 1),
    ("pigeon", 1),
    ("crow", 1),
    ("duck", 2),
    ("hawk", 3),
]

SOUNDS = ["CRACK!", "BANG!", "POP!", "THUMP!", "KRAK!"]


def spawn_bird(difficulty_key):
    # Weighted bird list changes slightly by difficulty
    if difficulty_key == "e":  # easy
        weights = [40, 30, 20, 8, 2]
    elif difficulty_key == "h":  # hard
        weights = [30, 25, 25, 15, 5]
    else:  # normal
        weights = [35, 28, 22, 12, 3]

    bird = random.choices(BIRDS, weights=weights, k=1)[0]  # (name, points)
    distance_m = random.randint(18, 85)
    angle = random.choice(["left", "right", "ahead"])
    speed = random.choice(["slow", "steady", "fast"])
    return bird[0], bird[1], distance_m, angle, speed


def get_difficulty_settings(key):
    # Returns: label, base_presence, base_hit, scan_bonus
    if key == "e":
        return "Easy", 0.74, 0.64, 0.12
    if key == "h":
        return "Hard", 0.60, 0.50, 0.10
    return "Normal", 0.68, 0.58, 0.11


# ----------------------------
# Home screen
# ----------------------------
def home_screen():
    clear_screen()
    slow_print("██████╗ ██╗██████╗ ██████╗     ██╗  ██╗██╗   ██╗███╗   ██╗████████╗", 0.002)
    slow_print("██╔══██╗██║██╔══██╗██╔══██╗    ██║  ██║██║   ██║████╗  ██║╚══██╔══╝", 0.002)
    slow_print("██████╔╝██║██████╔╝██║  ██║    ███████║██║   ██║██╔██╗ ██║   ██║   ", 0.002)
    slow_print("██╔══██╗██║██╔══██╗██║  ██║    ██╔══██║██║   ██║██║╚██╗██║   ██║   ", 0.002)
    slow_print("██████╔╝██║██║  ██║██████╔╝    ██║  ██║╚██████╔╝██║ ╚████║   ██║   ", 0.002)
    slow_print("╚═════╝ ╚═╝╚═╝  ╚═╝╚═════╝     ╚═╝  ╚═╝ ╚═════╝ ╚═╝  ╚═══╝   ╚═╝   ", 0.002)
    print()
    slow_print("First-Person Bird Hunter (Text Edition)", 0.01)
    print("Aim. Breathe. Fire. Reload. Survive the clock.\n")


def instructions():
    clear_screen()
    print("=== Instructions ===\n")
    print("Goal: Score as many points as possible before time runs out.")
    print()
    print("Commands:")
    print("  shoot  - Fire one bullet. If a bird is present, you might hit it.")
    print("  reload - Refill your magazine to full.")
    print("  scan   - Spend a moment scanning the sky to boost bird spotting briefly.")
    print()
    print("Scoring:")
    print("  Different birds give different points.")
    print("  Streaks increase your focus and improve your odds slightly.")
    print()
    input("\nPress Enter to return...")


# ----------------------------
# Game loop
# ----------------------------
def run_game(duration_seconds=60, max_bullets=16, difficulty_key="n"):
    label, base_presence, base_hit, scan_bonus = get_difficulty_settings(difficulty_key)
    weather_name, weather_presence, weather_hit = random.choice(WEATHERS)
    location = random.choice(LOCATIONS)

    # Final tuned chances
    presence_chance = min(0.90, max(0.20, (base_presence + (weather_presence - 0.68))))
    hit_chance = min(0.90, max(0.20, (base_hit + (weather_hit - 0.58))))

    score = 0
    bullets = max_bullets
    shots_fired = 0
    hits = 0
    streak = 0
    best_streak = 0

    scan_active_until = 0.0
    start_time = time.time()

    clear_screen()
    print("=== Mission Briefing ===")
    print(f"Difficulty: {label}")
    print(f"Location: {location}")
    print(f"Weather: {weather_name}")
    print(f"Time Limit: {duration_seconds}s")
    print(f"Magazine: {max_bullets} rounds (unlimited reloads)\n")
    input("Press Enter to begin...")

    clear_screen()
    slow_print("You raise your pistol. The world narrows to the treeline and open sky.\n", 0.01)

    while True:
        elapsed = time.time() - start_time
        time_left = duration_seconds - elapsed
        if time_left <= 0:
            print("\n=== TIME'S UP! ===")
            break

        focus_bonus = min(0.08, streak * 0.01)  # tiny bonus for streak
        scan_bonus_live = scan_bonus if time.time() < scan_active_until else 0.0

        # HUD
        print(
            f"\nTime: {clamp_int(time_left)}s  "
            f"Bullets: {bullets}/{max_bullets} [{bar(bullets, max_bullets)}]  "
            f"Score: {score}  "
            f"Streak: {streak}"
        )
        if scan_bonus_live > 0:
            print("Status: SCANNING BONUS ACTIVE")

        action = prompt_action()

        if action == "reload":
            if bullets == max_bullets:
                print("Your magazine is already full.")
            else:
                bullets = max_bullets
                print("You reload with a clean snap. Ready.")
            continue

        if action == "scan":
            # Scanning costs a bit of time, but boosts spotting briefly
            print("You scan the sky, tracking movement between branches...")
            scan_active_until = time.time() + 6.0
            time.sleep(0.6)
            continue

        # action == "shoot"
        if bullets <= 0:
            print("CLICK. Empty. Reload now!")
            streak = 0
            continue

        bullets -= 1
        shots_fired += 1

        bird_present = random.random() < min(0.95, presence_chance + scan_bonus_live + focus_bonus)
        sound = random.choice(SOUNDS)

        if not bird_present:
            print(f"{sound} Your shot fades into empty air. No target.")
            streak = 0
            continue

        bird_name, points, distance_m, angle, speed = spawn_bird(difficulty_key)
        print(f"{sound} A {bird_name} cuts {angle} at {distance_m}m, flying {speed}.")

        # Distance makes hits harder
        dist_penalty = max(0.0, (distance_m - 30) / 140)  # 0 at 30m, up to ~0.4 at long range
        final_hit_chance = max(0.10, min(0.90, hit_chance + focus_bonus - dist_penalty))

        if random.random() < final_hit_chance:
            score += points
            hits += 1
            streak += 1
            best_streak = max(best_streak, streak)

            if points >= 3:
                print(f"PERFECT SHOT. The {bird_name} drops hard. +{points} points!")
            elif points == 2:
                print(f"HIT. Clean takedown. +{points} points!")
            else:
                print(f"HIT. +{points} point!")

            # Small extra flavor on streaks
            if streak in (3, 5, 8, 12):
                print("Your breathing steadies. Focus locked in.")
        else:
            print("MISS. The bird veers away and disappears behind the trees.")
            streak = 0

        time.sleep(0.25)

    accuracy = (hits / shots_fired * 100) if shots_fired else 0.0
    clear_screen()
    print("=== After Action Report ===\n")
    print(f"Difficulty: {label}")
    print(f"Location: {location}")
    print(f"Weather: {weather_name}\n")
    print(f"Final Score: {score}")
    print(f"Shots Fired: {shots_fired}")
    print(f"Hits: {hits}")
    print(f"Accuracy: {accuracy:.1f}%")
    print(f"Best Streak: {best_streak}")
    print("\n===========================\n")
    input("Press Enter to return to Home...")


def main():
    while True:
        home_screen()
        sel = choice_menu(
            "Select an option:",
            [
                ("1", "Start Game"),
                ("2", "How To Play"),
                ("3", "Quit"),
            ],
        )

        if sel == "1":
            clear_screen()
            diff = choice_menu(
                "Choose difficulty:",
                [
                    ("e", "Easy (more birds, easier hits)"),
                    ("n", "Normal (balanced)"),
                    ("h", "Hard (fewer birds, harder hits)"),
                ],
            )
            run_game(duration_seconds=60, max_bullets=16, difficulty_key=diff)

        elif sel == "2":
            instructions()

        else:
            clear_screen()
            print("Good hunt.")
            break


if __name__ == "__main__":
    main()
```
