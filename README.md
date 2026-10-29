# 🏛️ Hispania Casino

### Five HTML5 Casino-Style Games · Phaser 4 · JavaScript

**Hispania Casino** is a multilingual collection of five classic
casino-style games, developed with Phaser 4, JavaScript and Vite.

---

## 🎬 Gameplay Demo

<video src="https://www.jorgesegovia.es/games/mini-fruit-slot/casinoCTornado.mp4" controls="controls" width="100%">
  Tu navegador no soporta el reproductor de vídeo HTML5.
</video>

> 📺 **[Ver o descargar vídeo completo de demostración en alta definición (MP4)](https://www.jorgesegovia.es/games/mini-fruit-slot/casinoCTornado.mp4)**

---


# 🏛️ Hispania Casino

### Five HTML5 Casino-Style Games · Phaser 4 · JavaScript

**Hispania Casino** is a multilingual collection of five classic
casino-style games, developed with Phaser 4, JavaScript and Vite.

Set within a Hispano-Roman-inspired visual theme, the project brings
together fruit slots, European roulette, dice, blackjack and a
wheel of fortune.

All games share a virtual-credit wallet and can be played directly
in a web browser.

**Free to play · Virtual credits only · No real-money gambling**

---

## The Five Games

| Game | Description |
|---|---|
| 🍒 Frutas de Hispania | Three-reel fruit slot machine with nine symbols and three paylines |
| 🎯 European Roulette | 37-number European wheel with inside and outside bets |
| ⚄ Roman Dice | Craps-inspired dice game with Pass Line, Don't Pass and Field |
| ♠ Roman Blackjack | Six-deck blackjack with doubling, splitting and dealer S17 |
| 🎡 Wheel of Fortune | 24-sector prize wheel with multipliers up to ×10 |

Players can switch between the five games using the casino navigation
controls.

The virtual-credit balance is shared across the games. Game-specific
states, such as an unresolved dice point or an active blackjack hand,
can also be preserved when switching scenes.

No payment system, deposits, withdrawals or real-money prizes
are implemented.

---

## Main Features

- Five playable HTML5 minigames
- Hispano-Roman-inspired graphical presentation
- Shared virtual-credit wallet
- Starting balance of 1,000 virtual credits
- Free-credit recharge
- Six interface languages
- Phaser 4 rendering
- WebGL and Canvas compatibility
- Procedurally generated graphical elements
- Synthesized sound effects using the Web Audio API
- Mouse and keyboard controls
- Responsive touchscreen controls
- Dedicated HTML controls for mobile devices
- Support for portrait and landscape layouts
- Mathematical engines separated from graphical scenes
- Exact payout and probability verification
- Automated browser testing with Playwright
- Production builds using Vite
- Relative asset paths for HTML5 portal integration
- Operation in iframe environments with blocked localStorage

The project is both a playable browser-game collection and a
technical demonstration of JavaScript game development,
mathematical modeling, responsive interfaces and automated QA.

---

## Technology Stack

| Component | Technology |
|---|---|
| Game framework | Phaser 4.2.1 |
| Programming language | JavaScript ES modules |
| Build system | Vite 8 |
| Browser testing | Playwright |
| Graphical rendering | WebGL and Canvas |
| Procedural artwork | Phaser Graphics and Canvas 2D |
| Audio | Web Audio API |
| Virtual-credit persistence | localStorage with fallback |
| Game mathematics | Independent JavaScript modules |
| Mobile interface | HTML, CSS and JavaScript |
| Automated mathematical auditing | Node.js |

The mathematical engines do not require Phaser or a graphical browser
environment. This allows payouts, probabilities and edge cases
to be tested independently of the interface.

---

## Getting Started

### Requirements

- Node.js 20.19+ or 22.12+
- npm
- A modern browser

### Install dependencies

    npm ci

### Start development server

    npm run dev

### Build for production

    npm run build

The production files are generated in:

    dist/

### Preview production build

    npm run preview

### Standalone server

    npm run start

### Run automated tests

    npm test

### Run mathematical audit

    npm run sim

The mathematical audit checks all five games without launching
the graphical interface.

---

## Casino Navigation and Shared Credits

The project uses Phaser scenes for its five games.

Game initialization and navigation are implemented in:

    src/main.js

The shared wallet is implemented in:

    src/CasinoWallet.js

Navigation allows players to move between games while retaining
their virtual-credit balance.

The system is designed to tolerate browser environments where
localStorage is unavailable, including restricted third-party iframes.

Automated tests verify balance consistency when returning between
games, paying prizes and restoring free credits.

---

## Game 1 — Frutas de Hispania

Frutas de Hispania is a three-reel slot machine.

### Configuration

| Feature | Value |
|---|---:|
| Reels | 3 |
| Visible rows | 3 |
| Horizontal paylines | 3 |
| Symbols | 9 |
| Stops per reel | 100 |
| Initial credits | 1,000 |
| Selectable bets | 10, 25, 50, 100 |

Each reel has 100 possible stop positions.

The three reels are selected independently.

A horizontal line awards:

- Three identical symbols: symbol-specific prize
- Exactly two identical symbols: consolation prize
- Otherwise: no prize

Matching pairs can occur in any two positions on a payline.

### Symbol Payouts

All multipliers are expressed relative to the selected wager.

| Symbol | Weight | Three matches | Two matches |
|---|---:|---:|---:|
| 🍒 Cherry | 24 | ×3 | ×0.4 |
| 🍋 Lemon | 18 | ×5 | ×0.4 |
| 🍊 Orange | 15 | ×7 | ×0.4 |
| 🍇 Grapes | 12 | ×12 | ×0.4 |
| 🍉 Watermelon | 10 | ×18 | ×0.4 |
| 🍓 Strawberry | 8 | ×25 | ×0.4 |
| ⭐ Star | 6 | ×40 | ×0.4 |
| 7 Seven | 5 | ×80 | ×0.4 |
| 💎 Diamond | 2 | ×200 | ×0.4 |

The reel strip uses deterministic weighted distribution to
spread symbols across the 100 positions and avoid long
consecutive groups.

### Verified Exact Mathematics

All 1,000,000 possible combinations have been enumerated using
the actual game evaluation engine.

| Metric | Exact Result |
|---|---:|
| Possible combinations | 1,000,000 |
| Return to player (RTP) | 94.1547% |
| Winning-spin frequency | 76.4920% |
| Winning combinations | 764,920 |
| Maximum combined multiplier | ×223 |

A winning spin means that at least one payline pays something.
It does not necessarily mean that the player earns a net profit.

The exact RTP is also verified analytically from the symbol
weights and payout table.

The separate seeded Monte Carlo audit evaluates 200,000 spins.
Its results may differ from the exact theoretical RTP because
the sample is finite.

Mathematical implementation:

    src/config.js

Graphical implementation:

    src/SlotScene.js
    src/CasinoScenes.js

Exhaustive testing:

    tests/slot-math-exact.spec.js

---

## Game 2 — European Roulette

The European roulette engine uses a wheel with 37 outcomes:

    0–36

It includes:

- 18 red numbers
- 18 black numbers
- One green zero
- The traditional European wheel order

The mathematical engine supports 13 bet types:

| Bet | Gross Winning Multiplier |
|---|---:|
| Straight | ×36 |
| Split | ×18 |
| Street | ×12 |
| Corner | ×9 |
| Six Line | ×6 |
| Dozen | ×3 |
| Column | ×3 |
| Red / Black | ×2 |
| Even / Odd | ×2 |
| Low / High | ×2 |

These are the supported mathematical bet types; available
interface controls may present a subset of them.

### Exact Mathematics

| Metric | Result |
|---|---:|
| Wheel outcomes | 37 |
| RTP | 97.2973% |
| House edge | 2.7027% |

The mathematical audit checks 154 legal bet configurations
against all 37 outcomes, for 5,698 settlement checks.

The results are checked exhaustively rather than estimated
by random simulation.

The engine also validates bet coverage, rejects invalid
input and prevents unsafe integer payouts.

Files:

    src/rouletteMath.js
    src/RouletteScene.js
    tests/roulette.spec.js

---

## Game 3 — Roman Dice

Roman Dice implements a craps-inspired game using two
six-sided dice.

Available betting options:

- Pass Line
- Don't Pass
- Field

A point can be established and carried forward through
subsequent rolls until resolved.

A Don't Pass bet pushes when the come-out roll is 12.

The Field bet pays:

- 2 or 12: gross ×3
- 3, 4, 9, 10 or 11: gross ×2
- All other totals: zero

### Exact Mathematics

| Bet | RTP | House Edge |
|---|---:|---:|
| Pass Line | 98.5859% | 1.4141% |
| Don't Pass | 98.6364% | 1.3636% |
| Field | 94.4444% | 5.5556% |

The audit verifies the 36 possible dice combinations,
come-out results, point resolution and combined payouts.

The mathematical engine also computes exact probabilities
for the bets that require several rolls.

Files:

    src/crapsMath.js
    src/CrapsScene.js
    tests/craps.spec.js
    tests/craps-ui.spec.js

---

## Game 4 — Roman Blackjack

Roman Blackjack uses standard playing cards.

### Rules

| Rule | Implementation |
|---|---|
| Number of decks | 6 |
| Cards in shoe | 312 |
| Dealer soft 17 | Stand (S17) |
| Natural blackjack | Pays 3:2 |
| Normal win | Pays 1:1 |
| Push | Original wager returned |
| Doubling | Supported |
| Splitting | Supported |
| Maximum split hands | 2 |
| Double after split | Supported |
| Split aces | One additional card per hand |
| Blackjack after split | Not treated as natural |
| Insurance | Not implemented |
| Surrender | Not implemented |

The game evaluates soft and hard hands, dealer behavior,
blackjack naturals, normal wins, pushes, busts and split hands.

The mathematical audit includes deterministic settlement checks.
Additional Playwright tests examine hand evaluation, split rules,
doubling and browser-interface behavior.

### RTP

No single RTP is claimed for blackjack.

Its expected return depends on the player's decisions, the
specific house rules and the strategy being followed.

Computing a meaningful blackjack RTP would require specifying
and evaluating a complete playing strategy.

Files:

    src/blackjackMath.js
    src/BlackjackScene.js
    tests/blackjack.spec.js
    tests/blackjack-ui.spec.js

---

## Game 5 — Wheel of Fortune

The Wheel of Fortune uses 24 equiprobable sectors.

### Prize Distribution

| Multiplier | Number of Sectors |
|---|---:|
| ×0 | 12 |
| ×0.5 | 5 |
| ×1 | 3 |
| ×2 | 2 |
| ×3 | 1 |
| ×10 | 1 |
| **Total** | **24** |

### Exact Mathematics

| Metric | Result |
|---|---:|
| Number of sectors | 24 |
| RTP | 93.7500% |
| House edge | 6.2500% |
| Maximum multiplier | ×10 |

The result is selected before the animation starts.

The mathematical engine then computes the rotation required
to place the selected sector under the pointer.

Automated checks verify:

- Prize distribution
- Exact RTP
- All 96 bet-and-sector payout combinations tested
- Jackpot settlement
- Sector selection
- Pointer alignment
- Rotation calculations
- Invalid-input protection

Files:

    src/wheelMath.js
    src/WheelScene.js
    tests/wheel.spec.js
    tests/wheel-ui.spec.js

---

## Random Number Generation

The roulette, dice, blackjack and wheel mathematical engines
use cryptographically generated random values with rejection
sampling where appropriate.

This avoids modulo bias when converting random integers
into the required outcome range.

The slot audit uses a separate, seeded pseudorandom generator
to produce repeatable simulation results.

The seeded audit generator is not a replacement for the
random-number generation used by the playable games.

This software has not been certified for regulated gambling.

---

## Localization

Hispania Casino includes six interface languages:

| Code | Language |
|---|---|
| ES | Spanish |
| EN | English |
| FR | French |
| DE | German |
| PT | Portuguese |
| JA | Japanese |

The interface allows changing languages during gameplay.

Language settings are stored when localStorage permissions
allow it.

The Phaser interface, casino navigation and additional
mobile HTML controls use localized labels.

Manual verification on real devices is still recommended,
particularly for long labels and Japanese font rendering.

---

## Mobile and Touchscreen Support

The internal Phaser resolution is:

    800 × 620

The game uses:

    Phaser.Scale.FIT
    Phaser.Scale.CENTER_BOTH

Additional HTML controls improve accessibility when the
Phaser canvas is scaled down for narrow mobile screens.

The original slot-machine touch dock is installed by:

    src/main.js

The shared touch controls for roulette, dice, blackjack
and the wheel are implemented in:

    src/TableTouchControls.js

Mobile features include:

- Bet-selection controls
- Game-specific actions
- Spin and roll buttons
- Navigation between games
- Selected-bet feedback
- Disabled controls during animations
- Credit and game-state synchronization
- Language and interface controls
- Portrait and landscape adaptations

### Verified Viewports

| Viewport | Orientation |
|---|---|
| 390 × 844 | Portrait |
| 320 × 568 | Compact portrait |
| 844 × 390 | Landscape |

Playwright verifies that the relevant controls remain
accessible and that the mobile panel does not obscure
the playable canvas in the tested configurations.

Real-device testing remains advisable for browser chrome,
display cutouts, unusual aspect ratios and touch responsiveness.

---

## Automated Quality Assurance

The project uses Playwright to test:

- Game initialization
- Production builds
- Canvas and WebGL rendering
- iframe deployment
- Relative asset loading
- Browser storage restrictions
- Shared-wallet integrity
- Betting and payout behavior
- Blackjack hands and dealer rules
- Roulette probabilities and settlements
- Dice-point preservation
- Wheel payouts and pointer alignment
- Touchscreen controls
- Responsive layouts
- Free-credit recharge
- Invalid mathematical inputs
- Exhaustive slot combinations
- Browser JavaScript exceptions

### Latest Verified Results

**52 of 52 selected Playwright tests passed.**

The latest complete run finished in approximately 61.65 seconds
using four workers.

The successful run included tests against the updated
Hispania Casino HTML entry page.

Relevant test files include:

    tests/iframe.spec.js
    tests/load.spec.js
    tests/slot-math-exact.spec.js
    tests/roulette.spec.js
    tests/craps.spec.js
    tests/blackjack.spec.js
    tests/blackjack-ui.spec.js
    tests/wheel.spec.js
    tests/wheel-ui.spec.js
    tests/casino.spec.js
    tests/craps-ui.spec.js
    tests/wallet.spec.js
    tests/mobile-dock.spec.js
    tests/table-touch.spec.js

The Playwright configuration selects the active regression
suite. Additional legacy and diagnostic test files remain in
the repository but are not necessarily included in that suite.

### Run Browser Tests

    npm test

### Run Mathematical Audit

    npm run sim

The audit runs:

1. A seeded 200,000-spin slot simulation.
2. Exhaustive roulette settlement verification.
3. Exact dice probabilities and settlement checks.
4. Deterministic blackjack rule and payout checks.
5. Wheel sector, payout and alignment checks.

Latest mathematical audit result:

    Five mathematical engines checked.
    Zero errors detected.
    Result: OK

Automated tests do not replace manual evaluation of gameplay,
art direction, audio quality or usability on physical devices.

---

## Production Build and Performance

Generate the production package:

    npm run build

The resulting application is written into:

    dist/

### Latest Verified Build

| Metric | Result |
|---|---:|
| Build status | Successful |
| Vite compilation | 631 ms |
| JavaScript bundle | 1,514.53 kB |
| JavaScript gzip | 399.91 kB |
| HTML gzip | 3.07 kB |
| CSS gzip | 1.06 kB |
| Active JavaScript bundles | 1 |
| Obsolete bundles | 0 |

The bundle-size warning reported by Vite is non-fatal.

Code splitting may be considered in the future, but changes
should be evaluated against actual loading times and scene
transition performance.

### Local Browser Loading Measurements

Median values from the latest successful Playwright run:

| Measurement | Canvas | WebGL |
|---|---:|---:|
| Canvas created | 118.2 ms | 138.2 ms |
| Loading screen removed | 965.7 ms | 991.9 ms |
| Interaction confirmed | 1052.1 ms | 1113.5 ms |

These measurements were taken on localhost.

They are not representative of download times over real
mobile networks, and interaction measurements include
Playwright automation and polling overhead.

No formal performance threshold has yet been established.

---

## HTML5 Portal Compatibility

Vite is configured with:

    base: './'

This generates relative production asset paths and allows
the game to run from a subdirectory instead of requiring
deployment at the domain root.

Automated tests have verified:

- Loading through an external iframe
- JavaScript and CSS resource requests
- Touchscreen play inside an iframe
- A real slot spin inside a portal-like environment
- Operation with localStorage blocked
- Canvas and WebGL production loading

The output directory can be packaged for deployment on
a compatible HTML5 game-hosting platform.

Passing automated compatibility tests does not guarantee
acceptance by a particular portal.

Before submission, verify that the game complies with the
platform's content, advertising, branding and technical
requirements.

---

## Project Structure

    index.html
    package.json
    package-lock.json
    playwright.config.js
    vite.config.js
    README.md

    src/
      main.js
      style.css
      sound.js
      config.js
      SlotScene.js
      CasinoScenes.js
      CasinoWallet.js
      RouletteScene.js
      rouletteMath.js
      CrapsScene.js
      crapsMath.js
      BlackjackScene.js
      blackjackMath.js
      WheelScene.js
      wheelMath.js
      TableTouchControls.js

    tests/
      blackjack-ui.spec.js
      blackjack.spec.js
      casino.spec.js
      craps-ui.spec.js
      craps.spec.js
      iframe.spec.js
      load.spec.js
      mobile-dock.spec.js
      mobile.spec.js
      roulette-touch-diagnostic.spec.js
      roulette.spec.js
      slot-math-exact.spec.js
      slot.spec.js
      table-touch.spec.js
      wallet.spec.js
      wheel-ui.spec.js
      wheel.spec.js

    tools/
      probe.mjs
      rtp-check.mjs
      serve.mjs

### Main Architecture

**src/main.js**

Initializes Phaser, registers the scenes, installs the
casino navigation and touchscreen interfaces.

**src/CasinoWallet.js**

Manages the shared virtual-credit wallet.

**src/CasinoScenes.js**

Integrates the original slot and roulette scenes with
the multi-game casino structure.

**src/config.js**

Defines slot symbols, weights, prize multipliers and
result evaluation.

**src/*Math.js**

Independent mathematical engines for roulette, dice,
blackjack and the wheel.

**src/TableTouchControls.js**

Provides shared touchscreen controls for the four
table and wheel games.

**tools/rtp-check.mjs**

Runs the joint mathematical audit.

**vite.config.js**

Configures relative asset paths and production cleanup.

**playwright.config.js**

Defines the active regression projects and test dependencies.

---

## Limitations and Future Work

Hispania Casino is a free, virtual-credit-only game collection.

It is not a regulated gambling product.

The project does not implement real-money wagering,
cash prizes, payment processing or withdrawals.

Potential future improvements include:

- Additional visual polish and animation effects
- More detailed gameplay tutorials
- Further localization review
- Accessibility improvements
- Manual testing on physical iOS and Android devices
- Additional browser compatibility tests
- Screenshot-based visual regression testing
- Improved performance measurements on real networks
- Production bundle analysis
- More polished game selection and onboarding
- Platform-specific advertising integration where permitted
- A documented release and deployment process

---

## Resumen en Español

**Hispania Casino** es una colección de cinco minijuegos HTML5
desarrollados con Phaser 4 y JavaScript.

Incluye:

- 🍒 Tragaperras Frutas de Hispania
- 🎯 Ruleta europea
- ⚄ Dados romanos
- ♠ Blackjack romano
- 🎡 Rueda de la Fortuna

Los cinco comparten un monedero de créditos virtuales.

El proyecto ofrece seis idiomas, controles móviles, gráficos
procedimentales, sonidos sintetizados y compatibilidad con
Canvas y WebGL.

### Matemáticas verificadas

| Juego | RTP |
|---|---:|
| Tragaperras | 94,1547 % exacto |
| Ruleta europea | 97,2973 % |
| Dados — Pass Line | 98,5859 % |
| Dados — Don't Pass | 98,6364 % |
| Dados — Field | 94,4444 % |
| Blackjack | Depende de la estrategia |
| Rueda de la Fortuna | 93,7500 % |

### Calidad técnica

- 52 pruebas Playwright superadas
- Un millón de combinaciones de tragaperras verificadas
- Auditoría matemática de los cinco motores
- Control de créditos entre escenas
- Pruebas móviles en tres resoluciones
- Compatibilidad probada con iframes
- Compilación de producción correcta
- Sin errores detectados en la última batería

**Solo utiliza créditos virtuales. No admite dinero real.**

---

## Author 

Coque Tornado

Portfolio:  

https://github.com/coquetornado

---

Developed as a technical portfolio project demonstrating
browser-game engineering, JavaScript architecture,
probability mathematics, responsive interfaces and
automated quality assurance.
