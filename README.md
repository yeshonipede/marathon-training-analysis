# Marathon Training Physiology Analysis

An applied analysis of wearable physiology and running data collected across a 16-week marathon training cycle. This project explores how training phase, environmental conditions, recovery metrics, and illness influenced physiological strain and perceived effort during training.

This repository is intended as analysis documentation and interpretation, not a fully executable pipeline. Raw wearable and activity data are private and not included.

### A summary write-up of this project is located here 📄 [Full Visual Write-Up (PDF)](write-up/Marathon_WriteUp.pdf) Check it out!

## Key Questions
- How did physiological recovery metrics change during marathon training compared to non-training periods?
- How strongly did weather conditions (temperature, humidity) influence my long runs vs my short runs?
- Did I successfully “undertrain” my long runs, in line with my intended 80/20 training strategy?
- How did illness (COVID) impact cardiovascular recovery markers during the training cycle?

## Data Sources 
  - Wearable physiological data from a Ringconn Gen 1 Smart Ring: Daily metrics including heart rate variability (HRV), resting heart rate, sleep, steps, and energy expenditure.
  - Run-level training data from Strava (collected with a Gen 5 Apple Watch): Distance, pace, elevation, and relative effort recorded via GPS running sessions. Also, weather conditions during the time of the run.
 
  Raw data is private and intentionally excluded. See data/sample_data/README.md for a description of dataset structure.
 
## Methods Summary
- Segmented physiological data into either being in my 16-week training block or outside of it.
- Segmented training into phases (base, build, peak, taper, race).
- Used correlation analyses to quantify environmental effects on effort for long runs vs short runs.
- Built a regression model to predict expected long-run effort from short-run data.
 - My goal for this training cylce was to "run slow to run fast" on race day. Therefore I intentionally tried to run at a slow, comfortable pace during my long runs. I built this model to retroactively assess if I successfully "undertrained" on my long runs compared to my normal short run efforts.
- Conducted pre/post illness comparisons of physio data to assess physiological disruption.

All analysis was performed locally in Python using pandas, NumPy, and standard statistical modeling tools.

## Key Findings
- Long runs were far more sensitive to environmental stress than short runs.
Heat, apparent temperature, and humidity showed substantially stronger relationships with perceived effort during long runs, suggesting that environmental stressors compound over time and place disproportionate strain on longer efforts.
- Baseline physiology improved during marathon training.
Compared to non-training periods, marathon training was associated with higher average HRV (+7.6%), lower resting heart rate (–6.1%), increased daily activity (+65% steps), and higher daily energy expenditure (+13%), indicating improved cardiovascular efficiency and overall workload tolerance.
- Physiological signals tracked expected training phases.
Resting heart rate and HRV fluctuated predictably across base, build, peak, and taper phases, reflecting adaptations to increasing load, cumulative fatigue during peak training, and recovery during taper.
- Most long runs were successfully “undertrained.”
A regression model trained on short-run data predicted expected effort on long runs. When applied to long runs, 9 of 11 were completed at lower effort than predicted, consistent with adherence to an 80/20, low-intensity training strategy.
- Illness disrupted cardiovascular recovery late in training.
Following COVID infection, resting heart rate and average running heart rate increased significantly (~3%) , while HRV remained relatively stable, suggesting persistent cardiovascular strain despite partial recovery.

## Visual Summaries 
Final figures summarizing the highlights of this analysis are in the figures/ directory. This includes:
- Training phase–dependent physiological changes: Average HRV increased and resting heart rate decreased during marathon training compared to non-training periods.
<img width="4469" height="9283" alt="phases" src="https://github.com/user-attachments/assets/4ac8bb54-0819-47fa-9da9-fbbc899aa9a1" />

<img width="4172" height="1772" alt="hrv" src="https://github.com/user-attachments/assets/0e7274c7-b873-4edc-8c94-11da5dddf857" />
- Environmental correlations with perceived effort: Heat and humidity showed substantially stronger associations with perceived effort during long runs than short runs.
  <img width="2123" height="1768" alt="dif_corr" src="https://github.com/user-attachments/assets/ec2cba56-d2d9-410e-a869-422759ea7896" />
- Modeled vs observed long-run effort: A regression model trained on short runs shows that most long runs were completed at lower effort than expected.
  <img width="2970" height="1771" alt="longrunbar" src="https://github.com/user-attachments/assets/0d4d47e6-6d07-471b-8473-cc2e27ecf37d" />

- Pre/post illness physiological comparisons
<img width="4770" height="2970" alt="covid_plots" src="https://github.com/user-attachments/assets/73c1cd98-145f-4884-b5a7-7fb33169a80b" />

## Limitations & Next Steps
- This analysis is based on a single-subject dataset and is not intended to be generalized.
- The predictive model was trained on short-run data and then applied to long runs. Physiological and environmental stressors may interact differently at longer durations, which could lead the model to underestimate the impact of factors such as heat and humidity on long-run effort.
- Some model predictors (e.g., pace-related and elevation-adjusted metrics) may be correlated, which could affect coefficient stability. Future iterations could explore dimensionality reduction or alternative regularization strategies.
