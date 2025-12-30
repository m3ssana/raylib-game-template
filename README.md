# raylib game template

A base structure for developing games with [raylib](https://www.raylib.com) in C.

## New to C Programming? Start Here!

Don't worry if you've never programmed in C before. This template is a great way to learn! Here's everything you need to know.

### What You'll Need

1. **A code editor** - [VS Code](https://code.visualstudio.com/) is free and beginner-friendly
2. **A C compiler** - This turns your code into a runnable program
3. **CMake** - A tool that helps build your project

### Step 1: Install the Tools

#### Windows
1. Download and install [Visual Studio 2022 Community](https://visualstudio.microsoft.com/) (free)
   - During installation, select "Desktop development with C++"
   - This includes the compiler and CMake
2. Alternatively, install [w64devkit](https://github.com/skeeto/w64devkit/releases) for a lighter setup

#### macOS
1. Open Terminal and run:
   ```bash
   xcode-select --install
   brew install cmake
   ```

#### Linux (Ubuntu/Debian)
```bash
sudo apt update
sudo apt install build-essential cmake git
sudo apt install libasound2-dev libx11-dev libxrandr-dev libxi-dev libgl1-mesa-dev libglu1-mesa-dev libxcursor-dev libxinerama-dev libwayland-dev libxkbcommon-dev
```

### Step 2: Build and Run

Open a terminal/command prompt in the project folder and run:

```bash
# Configure the project (downloads raylib automatically)
cmake -S . -B build

# Build the game
cmake --build build

# Run the game (from the src folder so resources load correctly)
cd src
```

Then run the executable:
- **Windows:** `..\build\raylib-game-template\Debug\raylib-game-template.exe`
- **macOS/Linux:** `../build/raylib-game-template/raylib-game-template`

You should see a window with the raylib logo that transitions to a title screen!

### Step 3: Understanding the Code Structure

```
src/
├── raylib_game.c      # Main file - game loop lives here
├── screens.h          # Shared definitions for all screens
├── screen_logo.c      # Logo/splash screen
├── screen_title.c     # Title/menu screen
├── screen_gameplay.c  # YOUR GAME CODE GOES HERE!
├── screen_options.c   # Options/settings screen
├── screen_ending.c    # Game over/ending screen
└── resources/         # Images, sounds, fonts
```

**The game flows like this:** Logo → Title → Gameplay → Ending → Title (loop)

### Step 4: Make Your First Change

Let's modify the gameplay screen! Open `src/screen_gameplay.c` and find the `DrawGameplayScreen` function:

```c
void DrawGameplayScreen(void)
{
    // Change the background color
    DrawRectangle(0, 0, GetScreenWidth(), GetScreenHeight(), PURPLE);

    // Draw some text
    DrawText("MY FIRST GAME!", 20, 20, 40, WHITE);

    // Draw a moving circle (add these lines)
    static float x = 400;  // static means it remembers its value
    static float y = 225;

    // Move with arrow keys
    if (IsKeyDown(KEY_RIGHT)) x += 5;
    if (IsKeyDown(KEY_LEFT)) x -= 5;
    if (IsKeyDown(KEY_DOWN)) y += 5;
    if (IsKeyDown(KEY_UP)) y -= 5;

    DrawCircle(x, y, 30, YELLOW);
}
```

Rebuild and run to see your changes!

### Step 5: Learn C as You Go

Here are the C basics you'll use most:

```c
// Variables - store data
int score = 0;              // Whole numbers
float speed = 5.5f;         // Decimal numbers (f means float)
bool isAlive = true;        // true or false

// If statements - make decisions
if (score > 100) {
    // do something
}

// Loops - repeat actions
for (int i = 0; i < 10; i++) {
    // runs 10 times
}

// Functions - reusable code blocks
void MyFunction(int parameter) {
    // code here
}
```

### Useful raylib Functions for Beginners

```c
// Drawing
DrawRectangle(x, y, width, height, color);
DrawCircle(x, y, radius, color);
DrawText("Hello", x, y, fontSize, color);

// Input
IsKeyPressed(KEY_SPACE);    // True once when pressed
IsKeyDown(KEY_SPACE);       // True while held down
GetMousePosition();         // Returns Vector2 with x, y

// Collision detection
CheckCollisionRecs(rect1, rect2);      // Rectangle vs rectangle
CheckCollisionCircles(c1, r1, c2, r2); // Circle vs circle

// Sound (fxCoin is already loaded for you!)
PlaySound(fxCoin);

// Random numbers
GetRandomValue(min, max);
```

### Common Beginner Mistakes

1. **Forgetting semicolons** - Every statement ends with `;`
2. **Using `=` instead of `==`** - Use `=` to assign, `==` to compare
3. **Not rebuilding** - After changing code, run `cmake --build build` again
4. **Resources not loading** - Make sure to run from the `src` folder

### Where to Learn More

- [raylib cheatsheet](https://www.raylib.com/cheatsheet/cheatsheet.html) - All functions at a glance
- [raylib examples](https://www.raylib.com/examples.html) - 100+ code examples
- [Learn C](https://www.learn-c.org/) - Interactive C tutorial

---

## Getting Started (Experienced Developers)

### CMake

```bash
cmake -S . -B build
cmake --build build
```

Run from `src` directory for proper resource loading. Debug build: `-DCMAKE_BUILD_TYPE=Debug`

CMake automatically fetches raylib 5.5. Use local raylib: `-DFETCHCONTENT_SOURCE_DIR_RAYLIB=<path>`

### Visual Studio

1. Place `raylib-game-template` alongside a `raylib` folder
2. Open `projects/VS2022/raylib-game-template.sln`
3. Set `raylib_game` as startup project
4. Click "Local Windows Debugger" to run

### Linux Dependencies

See [Working on GNU Linux](https://github.com/raysan5/raylib/wiki/Working-on-GNU-Linux)

---

## $(Game Title)

![$(Game Title)](screenshots/screenshot000.png "$(Game Title)")

### Description

$(Your Game Description)

### Features

 - $(Game Feature 01)
 - $(Game Feature 02)
 - $(Game Feature 03)

### Controls

Keyboard:
 - $(Game Control 01)
 - $(Game Control 02)
 - $(Game Control 03)

### Screenshots

_TODO: Show your game to the world, animated GIFs recommended!_

### Developers

 - $(Developer 01) - $(Role/Tasks Developed)

### Links

 - YouTube Gameplay: $(YouTube Link)
 - itch.io Release: $(itch.io Game Page)

### License

This game sources are licensed under an unmodified zlib/libpng license, which is an OSI-certified, BSD-like license that allows static linking with closed source software. Check [LICENSE](LICENSE) for further details.

*Copyright (c) 2014-2025 Ramon Santamaria ([@raysan5](https://github.com/raysan5))*
