# ClarityCS

ClarityCS is my research project for **detecting suspicious Counter-Strike 2 behavior using structured demo data** (not screen capture).  
The goal is to turn `.dem` files into **clean, model-ready datasets** and explore signals that differentiate:

- normal matchmaking / FACEIT-level play  
- professional-level play  
- (eventually) cheating patterns like aim assistance, recoil scripts, and information advantage

This repo is where I keep my parsing pipeline, experiments, and visualizations as the project evolves.

---

## What this project is (right now)

### Demo Dataset pipeline
I’m building a repeatable pipeline that:
1. parses CS2 demos (currently using **AWPy / demoparser2**)
2. produces **event-level + tick-level** outputs (parquet)
3. generates **windowed features** around key moments (especially kills)
4. compares distributions across cohorts (ex: **pro vs normal**)

### Early analytics / sanity checks
I’m validating metrics visually before doing serious ML:
- aim-related error distributions (baseline separation)
- visibility/engagement context (line-of-sight style signals)
- “window” summaries around kills (pre/post context)

---

## What this project is NOT
- Not a finished anti-cheat
- Not claiming “I can detect all cheaters”
- Not a tool meant to accuse individual players

This is **research + tooling** focused on building reliable datasets and testing hypotheses.

---

## Current direction

### 1) Baselines first: Pro vs Normal
Before touching “cheater detection,” I’m establishing what *legit high-skill* looks like.  
If we can’t separate *normal vs pro* reliably (or understand the overlap), detecting cheats becomes noise.

### 2) Window + tick analysis
Instead of only looking at one datapoint at the kill moment, I’m moving toward:
- **64 ticks pre / 64 ticks post** windows (≈ 1s before/after)
- time-series features like: stabilization → target acquisition → shot timing → correction patterns

### 3) Player-level vectors (later)
Cheater demos are messy because usually only 1–2 players cheat per lobby.  
So the plan is:
- build **player-specific** feature vectors using attacker/victim SteamIDs
- aggregate across a match (or multiple matches) per player
- model “suspicion” rather than “this lobby is cheating”

---

At the end of the day, I'm just a guy that likes playing CS2 and got fed up playing against tons of cheaters. Curiosity led me here.
---

## Notes
CS2 demos and parsing libraries change over time. If something breaks after game updates, I usually pin versions or adjust the parser config.

---

## Developer
**Gerry Jones**  
GitHub: https://github.com/gjones01  
Instagram: https://instagram.com/clearvision.ai


