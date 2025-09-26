***June 25th, 2025***

**Changes & Updates**

*Phase 1: Frame-Based Categorization*
When initally undertaking this project, it originally started with a 2-dimensional CNN to classify screenshots from .mp4 files of demo footage.
The reasoning behind this was for my own understanding of image processing. Up until this point I only dealt with structured tabular data.
2-dimensional CNNs have their place in image classification, but in regards to identifying cheaters in Counter Strike it lacks temporal context.
Static images lack robustness.

*Phase 2: The Switch*
The next step was moving to video classification rather than static photos. This meant moving to "r3d_18" which is the 3D CNN equivalent of ResNet-18.
The standard input shape is [batch, channels, time, height, width].
Batch: Rather than trying to process hundreds or thousands of .mp4 files at once, it is divided into subsets called "batches."
Channels: This refers to the color channel which is RGB(3).
Time: This is the crucial difference maker, allowing the model to have temporal context. In this case it was 64 (frames not seconds).
Height & Width: Simply the pixel dimensions.

This allows for the model to now learn from behavior, not just visuals. Since the goal is to identify cheating behavior, this is important.


*Phase 3: The ".dem" Arc*
During this phase I took a slight tangent to explore the validity of incorporating .dem file parsing into the model. ".dem" files (short for demo)
are Valve's custom file types that allow a player to rewatch a match. It records structured game data such as tick rates, player position, crosshair angle, TTK(time to kill) thus allowing the user to watch from the perspective of any player in the lobby.
This was with the intent of extracting game data from legit players and cheaters to train a classification model (such as XGBoost) and then cross reference that with the video footage.

Major Issues: 
1. Unreliable sources to actually download the .dem files rather than auto-opening in the game (besides my own matches).
2. Syncing .dem tickrates to portions of .mp4 files. 

Therefore (atleast for now) utilizing .dem files to train a binary classification has been put on the back burner.


*Phase 4: First Successful Flag*
After returning to r3d_18, I created a prediction pipeline where the training model was loaded into a new enviroment, and fed a .mp4 clip from a demo.
Surprisingly it worked great with ClearVision identifying the player as a cheater with a confidence of 58%. The player used in the experiment is a known cheater in the top 200 on Premier.
Thise is a major milestone as it is the first instance of passing a .mp4 file, having every nth frame extracted and allowing the model to temporally analyze each frame sequentially to come to a conclusion.


*Next Phase*
As of now, the next step is to continue gathering demo footage in a class balanced manner. Once I reach ~1,000 snippets of demo footage I will move to training on a server-side GPU in HD quality.





***September 26, 2025***

*Phase 1 ~July 2025*
Implemented a stats module leveraging the newly released Leetify API. The base API provides match-level and account-level metrics such as aim rating, utility, HS%, counter-strafe success, ADR etc. along with identifiers like VAC bans, age of registration and elo. With these base statistics, further metrics were derived such as an "aim-reaction" index and "headshot-spot" index. These are just two examples of many where more in-depth statistics can reveal gameplay patterns. Ex: indexing on average how quickly it takes a player to fire a shot at the enemy's head and how frequently those are headshots. Consistently above average markers for their elo, or other high elo players could potentially raise red flags. 

The purpose for deriving this data is for two resons:
1. Allow for surface level observation of a player's performance by a rolling windowed average (Example: I want to see this user's average spot-reaction time for the past 40 matches).
2. Leverage these points of data as features for machine learning to classify the chance of a player potentially cheating. This will use XGBoost.

XGBoost has been a superior method for predictive modeling due to the fact it's a self correcting algorithm. Unlike Random Forests or Extra Trees, XGBoost sequentially builds each tree. In simplest terms, this is how it works:

You are trying to predict a hidden number.
i. You make an initial guess that is incorrect
ii. Instead of guessing again you ask whether it is too low or too high
iii. Now you guess again, but with the intention of getting closer based on the feedback from step 2.
iv. Repeat steps 1-3 tens, hundreds, thousands or millions of times.

Each iteration is based off of previous attempts with it eventually converging on the correct value. In implementation, if the model is well balanced, it could reliably see new player data and infer their status. If you are interested in reading more about the theory behind XGBoost and why it is so powerful, I suggest this study from 2019 --> [**XGBoost**](https://arxiv.org/pdf/1911.01914).


*Phase 2 ~August 2025*
I began my journey in building a website with the goal being a onestop shop for an individual to look up player statistics via SteamID64 and a place to eventually host the computer vision model. I have never built a website before, so I am self-pacing myself through web development courses online since it is something I've always wanted to learn. Therefore, it is a "build as I go" methodology at the moment. However, I have a skeleton of the landing page as seen below. This will certainly not be hte final product but definitely a start:

![Landing Page Skeleton](media/landingskeleton.gif)


Update about computer vision model: I usual, the last hurdle with the computer vision portion of ClarityCS is the data collection. Training should not be a major obstacle, thanks to the accessibility of cloud GPUs. I will keep people posted on any major updates that happen regarding that.

