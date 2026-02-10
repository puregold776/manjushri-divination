# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## Project Overview

This is a **Manjushri Divination** (文殊占卜) web application - a Tibetan Buddhist dice divination system based on the teachings of Mipham Rinpoche (全知麥彭仁波切). The application is a single-file HTML application with embedded CSS and JavaScript, requiring no build process or dependencies.

## Technical Architecture

### Single-File Structure
The entire application is contained in `index.html` (~1737 lines):
- **Lines 1-598**: HTML head with embedded CSS styling
- **Lines 600-692**: HTML body structure
- **Lines 694-1735**: Embedded JavaScript with hexagram data and logic

### Core Components

**Hexagram Data System** (`hexagrams` object, lines ~696-1400):
- Contains all 36 possible divination outcomes (6×6 combinations)
- Each hexagram represents a combination of two dice faces using Tibetan characters: ཨ, ར, པ, ཙ, ན, དྷཱིཿ
- Structure: `'ཨ-ཨ': { name, fortune, direction, verse, meaning, readings, practices }`
- Fortunes are categorized: 上上吉, 上吉, 吉, 中平, 凶, 大凶

**Dice Rolling Logic** (`rollDice()` function, lines ~1400-1450):
- Simulates 3D dice rotation using CSS transforms
- Generates random results for yellow dice (佛父/Buddha Father) and white dice (佛母/Buddha Mother)
- Maps dice faces to Tibetan syllables and looks up corresponding hexagram

**Results Display** (`displayResult()` function, lines ~1450-1530):
- Dynamically creates collapsible sections for different reading categories
- Categories include: 家庭和生命, 謀略與籌劃, 財運, 怨敵, 行旅之人, 疾病, 修法, 丟失物, 來客及成事, etc.

**Sharing Features** (lines ~1538-1730):
- Social media sharing for Facebook, LINE, WeChat
- Image generation using HTML5 Canvas API for Instagram sharing
- Web Share API integration for modern browsers

## Development

### Running the Application
Simply open `index.html` in a web browser. No build process, server, or dependencies required.

### Testing Changes
Refresh the browser after making edits to `index.html`.

### Important Constraints
- **Cultural Sensitivity**: This is a religious/spiritual application. Any modifications should respect the Tibetan Buddhist tradition and the accuracy of the divination system.
- **Language**: The application is in Traditional Chinese (繁體中文) with Tibetan script. Maintain this language consistency.
- **Hexagram Data**: The 36 hexagrams and their interpretations are based on traditional teachings. Do not modify the content of hexagram readings unless explicitly requested by the user.

## Code Organization

### CSS Styling System
- Uses CSS custom properties (variables) for color theming: `--maroon`, `--gold`, `--white`, etc.
- Responsive design with breakpoints at 768px and 480px
- 3D dice animation using CSS `transform-style: preserve-3d`

### JavaScript Architecture
- Pure vanilla JavaScript, no frameworks or libraries
- Global variables: `isRolling` (state), `currentResult` (current hexagram)
- Main functions:
  - `rollDice()`: Handles dice animation and result generation
  - `displayResult(result)`: Renders hexagram interpretation
  - `toggleReading(element)`: Expands/collapses reading sections
  - `shareFacebook/Line/WeChat/Image/Web()`: Social sharing functions

### Dice Face Mapping
```javascript
faces = {
  1: 'ཨ', 2: 'དྷཱིཿ', 3: 'ར',
  4: 'ཙ', 5: 'ན', 6: 'པ'
}
```

## Key Features

1. **3D Dice Animation**: CSS transform-based 3D cube with six faces showing Tibetan syllables
2. **36 Hexagram System**: Complete divination outcomes based on dice combinations
3. **Collapsible Readings**: Each hexagram has 8-10 reading categories that expand on click
4. **Fortune Classification**: Six levels of fortune (上上吉 to 大凶) with color-coded badges
5. **Multi-Platform Sharing**: Facebook, LINE, WeChat, and image download for Instagram
6. **Responsive Design**: Mobile-friendly layout with breakpoints

## Hexagram Structure Example

Each hexagram entry contains:
- `name`: Chinese name of the hexagram (e.g., "無垢晴空")
- `fortune`: Fortune level (上上吉/上吉/吉/中平/凶/大凶)
- `direction`: Directional indication (下下/下東/上吉/etc.)
- `verse`: Poetic verse describing the hexagram
- `meaning`: Symbolic interpretation
- `readings`: Object with 8-10 life aspect interpretations
- `practices`: Recommended spiritual practices

## Common Modifications

When modifying this application:

1. **Adding new hexagrams**: Update the `hexagrams` object with the same structure
2. **Styling changes**: Modify CSS variables in `:root` or specific CSS rules
3. **UI translations**: Search for Chinese text strings and update carefully
4. **Animation timing**: Adjust `transition` properties in CSS or timing values in `rollDice()`
5. **Sharing features**: Modify share functions (lines ~1538-1718)

## Cultural Context

The application implements **Manjushri Divination** (ཨ་ར་པ་ཙ་ན་དྷཱིཿ), a traditional Tibetan Buddhist divination method:
- Two dice represent Buddha Father (yellow) and Buddha Mother (white)
- Six faces correspond to the six syllables of Manjushri's mantra
- 36 possible combinations provide guidance on life questions
- Based on teachings translated by Khenpo Sodargye (索達吉堪布)

Users are instructed to visualize Manjushri, recite the mantra 3-7 times, focus on their question, then cast the dice.
