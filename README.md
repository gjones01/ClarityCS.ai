# ClarityCS
**Computer Vision cheat detection utilizing Deep Learning.**

Clarity is an experimental, research-driven project using Deep Learning and computer vision to detect suspicious gameplay behavior for Counter Strike 2:
- Aimbotting
- Wallhacking
- Unnatural flicks/corsshair movement

Modern cheats utilize exploits such as DLL file manipulation to inject scripts into the game code. The theory behind Clarity is to create a Neural Network that watches game footage. Rather than looking at raw game data (which can be manipulated), analyze the pixels on the screen. There is very limited literature on using computer vision on raw video input. However, cheat developers are already ahead of the curve, utilizing computer vision for real time aimbots that 100% bypass traditional anti-cheat systems such as Ricochet Anti-Cheat. If it can be used to develope cheats, there is a way to leverage it for detecting them. This project is not intended to be a fully fledged anticheat software, but rather a toll that can potentially identify cheaters that have been known to plague Counter-Strike.

In conjunction with this, Clarity derives even more granular statistics (with base stats being sourced form the Leetify API) which aims to further identify ireegular play. Anti-cheats can be bypassed, AI video models can potentially be spoofed, but the stat line is unchanging. Whether it is rage spinbotting or GenAI recoil patterns to fool video models, anomalous reaction times, aim indexes, recoil accuracy and numerous other values will be revealed.

This repository will act as a public space for updates, research notes, model performance and dev logs. Currently, there is a ReadME (this) and an architecture file that goes over the basic structure of my current model without going into too much detail. Finally there is a picture folder where I will be updating a lot more images of progress being made lately. I will sparingly share small portions of actual source code, due to the fact this is experimental. However, when appropriate, I will showcase anything of interest. 

This is a passion project I do in my spare time, so there is no specific timeline at the moment for releasing a Beta.

🔒 Source code is currently private while development is in progress.  
📈 Stay tuned for results, benchmarks, and visualizations.

---
**Developer:** [@gjones01](https://github.com/gjones01)  
**Instagram:** [@clearvision.ai](https://instagram.com/clearvision.ai) 


