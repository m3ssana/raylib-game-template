# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## Build Commands

### CMake (Recommended)
```bash
# Configure
cmake -S . -B build

# Configure with debug symbols
cmake -S . -B build -DCMAKE_BUILD_TYPE=Debug

# Build
cmake --build build

# Run (from src directory for proper resource loading)
cd src && ../build/raylib-game-template/raylib-game-template
```

### Web Build (Emscripten)
```bash
cmake -S . -B build -DPLATFORM=Web
cmake --build build
```

### Makefile (Alternative)
```bash
cd src
make                    # Desktop build
make PLATFORM=PLATFORM_WEB    # Web build
make BUILD_MODE=DEBUG         # Debug build
make clean              # Clean build artifacts
```

## Architecture

### Screen-Based State Machine
The game uses a screen-based architecture with fade transitions. Each screen (Logo, Title, Options, Gameplay, Ending) implements four functions:
- `Init[Screen]Screen()` - Initialize screen state
- `Update[Screen]Screen()` - Update logic each frame
- `Draw[Screen]Screen()` - Render screen
- `Unload[Screen]Screen()` - Cleanup resources
- `Finish[Screen]Screen()` - Return non-zero to trigger screen transition

Screen flow: LOGO → TITLE → (OPTIONS | GAMEPLAY) → ENDING → TITLE

### Key Files
- `src/raylib_game.c` - Main entry, game loop, screen transitions, global resources
- `src/screens.h` - GameScreen enum, shared globals (`font`, `music`, `fxCoin`, `currentScreen`)
- `src/screen_*.c` - Individual screen implementations

### Global Resources
Loaded in main, available to all screens via `screens.h`:
- `Font font` - Global font
- `Music music` - Background music
- `Sound fxCoin` - Sound effect
- `GameScreen currentScreen` - Current active screen

### Resources
Place assets in `src/resources/`. CMake copies them to build output automatically.

## C Coding Conventions

Follow raylib style from CONVENTIONS.md:
- Variables/params: `lowerCase`
- Functions: `TitleCase` (e.g., `InitWindow()`)
- Defines/Macros/Enums: `ALL_CAPS`
- Structs/Enums types: `TitleCase`
- 4 spaces indentation, no tabs
- Braces on separate lines (Allman style)
- Always initialize variables
- Float literals: `10.0f`
- Conditions in parentheses: `if ((value > 1) && (value < 50) && isActive)`

### File Naming
- Directories: `snake_case`
- Files: `snake_case` (e.g., `screen_gameplay.c`, `main_theme.ogg`)
