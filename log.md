June 25th, 2025

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
As of now, the next step is to continue gathering demo footage in a class balanced manner. Once I reach ~1,000 snippets of demo footage I will move to training on a cloud GPU in HD quality.
