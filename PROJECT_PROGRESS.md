Project Overview
Sudoku Fun (סודוקו כיף) is a responsive mobile-first web application built as a single-file solution using HTML5, Tailwind CSS, JavaScript (ES6+), Web Audio API, and HTML5 LocalStorage. The application features multiple grid sizes, distinct game modes, seeded daily challenges, and persistent state management.

Core Architecture & Technical Stack
Frontend: HTML5, Tailwind CSS (with custom Neumorphic shadow utilities), Vanilla ES6 JavaScript, canvas-confetti integration.

Audio System: Custom Web Audio API synthesizer for native mobile touch feedback and sound effects (click, error, fanfare) without external audio asset dependencies.

State Management: LocalStorage engine handling active game persistence, best times, streak counts, stars collection, and daily challenge progression.

Deployment & Version Control: GitHub repository hosted and deployed via Vercel.

Game Modes & Features
1. Classic Sudoku Mode
Grid Support: 4x4, 6x6, 9x9, 12x12.

Difficulties: Easy, Medium, Hard.

Tools: Pencil notes (with auto-clean logic on number placement), error inspector, hint engine, game pause/resume, personal best records per grid size/difficulty.

2. Competitive Mode
Grid: 9x9 only.

Rules: Strict competition rules — hints, error checking, pause menu, and puzzle regeneration are completely disabled.

Leaderboards: Separate leaderboards for Easy, Medium, and Hard tiers.

3. Daily Challenge Engine (Seeded System)
Rotation Catalog:

X-Sudoku 9x9 (❎): Requires numbers 1-9 to be unique across primary diagonals.

Countdown 9x9 (⏱️): Time-attack countdown timer (Easy: 4:30, Medium: 6:00, Hard: 8:00).

Memory Training 9x9 (🧠): Pencil notes mode disabled; difficulty strictly locked to Hard.

Titan 12x12 (🐘): Extended 12x12 grid awarding double star rewards.

Survival 9x9 (💀): Zero hints with mistake limits (Easy: 1, Medium: 2, Hard: 3).

Scoring Mechanics: Dynamic formula calculating base difficulty score, speed/time bonus, penalties for hints/errors, active daily streak multiplier, and weekly 7-day milestone bonuses.

4. Journey & Leaderboard Hub
Journey Mode: Map-based level progression tracking cumulative star collection.

Leaderboard Tabs: Personal Bests (filterable by grid size), Daily Challenge Standings (Today vs. Cumulative Streak), Competitive Standings, and Global Collector Ranks.

Recent Updates & Key Logic Fixes
1. Persistent Daily Challenge State (Anti-Exploit Architecture)
Problem Addressed: Navigating to the Home screen during an active Daily Challenge previously wiped current elapsed time, hint counts, and error penalties, allowing players to restart with a clean slate.

Solution Implemented:

Implemented date-seeded local persistence using unique keys (sudoku_daily_saved_{seed}_{challengeId}).

Complete session preservation: secondsElapsed, dailyHintsUsed, dailyErrorsMade, board numbers, and pencil note sets are serialized on every tick/action.

Returning to the Home screen and re-entering the Daily Challenge seamlessly resumes the exact timer and mistake state.

State automatically resets only when the daily date seed updates or when the challenge ends in an explicit win/loss state.

2. Memory Training Difficulty Enforcement
Problem Addressed: "Memory Training" mode occasionally generated easy-tier boards.

Solution Implemented: Enforced a hard lock (currentDifficulty = 'hard') specifically for the no_pencil_9x9 challenge catalog entry to guarantee consistent difficulty scaling.

3. Timer & Cross-Mode Isolation
Problem Addressed: State bleeding between game modes when navigating back to the main menu.

Solution Implemented: Explicitly reset and isolated state flags (isCompetitiveMode, isDailyMode, timer intervals) upon menu navigation.

Future Roadmap
Journey Mode Expansion: Full map rendering with unlockable level stages and star milestones.

PWA Capabilities: Add service worker support for offline functionality and home screen installation.

Global Leaderboard Sync: Connect to a backend service for real-time multiplayer score tracking.
