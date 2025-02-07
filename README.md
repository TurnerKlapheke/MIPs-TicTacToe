# MIPs-TicTacToe

[![MARS](https://img.shields.io/badge/Environment-MARS_4.5_Simulator-2B2D42.svg?style=flat)](http://courses.missouristate.edu/kenvollmar/mars/)
[![ASM](https://img.shields.io/badge/Language-MIPS_Assembly-004088.svg?style=flat)](https://en.wikipedia.org/wiki/MIPS_architecture)
[![Education](https://img.shields.io/badge/Education-NCSSM-107895.svg?style=flat)](https://www.ncssm.edu)

## Project Overview

**MIPS Tic-Tac-Toe** is a low-level assembly implementation featuring:
- Human vs Computer gameplay
- Memory-mapped I/O graphics
- QWERTY-style input mapping (q,w,e,a,s,d,z,x,c)
- Win condition detection
- Basic collision checking
- Game reset functionality

Developed using the MARS (MIPS Assembler and Runtime Simulator) 4.5 environment, this project demonstrates fundamental concepts of computer architecture through practical implementation.

### Game Implementation
- **Board Representation**:
  - 16x16 grid memory structure
  - Predefined X/O sprites
  - Dynamic board redrawing
- **Input System**:
  - Keyboard polling via 0xFFFF0008
  - QWERTY-to-grid mapping
  - Move validation system
- **Game Logic**:
  - Turn-based gameplay
  - 8-way win condition checking
  - Draw detection
- **Basic AI**:
  - Random valid move selection
  - Immediate response timing

## Technical Implementation

### Memory Architecture
- **Board Storage**: 
  - 1024-byte grid at 0x10010000
  - 4-byte word alignment
  - Preloaded grid template
- **Sprite Data**:
  - 16-word X (red) and O (blue) patterns
  - Direct memory-to-display blitting

### Critical Routines
1. **Input Handler** (`input:`)
   - Keyboard interrupt polling
   - Positional mapping (q=0, w=1, ..., c=8)
   - Move validation through memory checks

2. **Render System** (`write_x/o:`)
   - Nested loop structure (i/j)
   - Bitwise address calculation
   - Sprite pattern application

3. **Win Check** (`win_check:`)
   - Positional truth evaluation
   - 8 combinatorial checks
   - Draw detection at 9 moves

4. **AI Logic** (`enemy:`)
   - PRNG via syscall 42
   - Random valid move selection
   - Input simulation

## Development Context

Created during my senior year at the [North Carolina School of Science and Mathematics](https://www.ncssm.edu) over a 3 week period as part of a J-Term Collaboration between myself and a peer **Max Wolffe** using pair programming methodology.

**Development Period**: January 2023

## Collaboration

Developed in equal partnership with **Max Wolffe** (NCSU College of Engineering '28). Our collaborative workflow featured:
- **Version Control**: Manual change tracking via shared documentation
- **Pair Programming**: Split focus between AI logic and UI components
- **Testing Protocol**: Cross-verification of subsystem integrations

**Contributors**:
- Turner Klapheke
- Max Wolffe

## Installation & Execution

1. [Download MARS 4.5 Simulator](http://courses.missouristate.edu/kenvollmar/mars/download.htm)
2. Clone repository:
   ```bash
   git clone https://github.com/TurnerKlapheke/mips-tictactoe.git
3. Launch MARS and open tictactoe.asm
4. Assemble (Ctrl+R) and Run (F5)

### Controls
* q w e
* a s d
* z x c
* y/n for replays

### Limitations
* No difficulty levels
* basic random ai
* fixed grid layout
* no score tracking

## Code Structure

```plaintext
.data 0x10010000
board:   # 16x16 grid buffer
grid:    # Template with permanent lines
X/o:     # Player/AI sprites
q-c:     # Position mappings (68, 88,...748)

.text 0x00400000
main:         # Game loop controller
setup:        # Grid initialization
refresh:      # Display redraw
write_x/o:    # Sprite rendering
input:        # Player input handling
enemy:        # AI move selection
win_check:    # Victory/draw detection
replay:       # Reset functionality
