# Supplemental code for "Distinct spatially organized striatum-wide acetylcholine dynamics for the learning and extinction of Pavlovian associations"

------------------
## Contents
* [Project Overview](#project-overview)
* [Folder Structure](#folder-structure)
* [Data Availability](#data-availability)
* [Documentation and Working Example](#documentation-and-working-example)
* [System Requirements](#system-requirements)
* [License and citation](#license-and-citation)
* [Acknowledgements](#acknowledgements)

------------------
## Project Overview

This repository contains scripts for analyzing and plotting: (1) ACh release dynamics across the 3D volume of the striatum using a multi-fiber photometry array in head-fixed behaving mice, in response to cues, rewards, and spontaneous licking during the learning and extinction of Pavlovian associations; (2) Behavioral changes (licking and movement) during the learning and extinction of Pavlovian associations; (3) DA release dynamics in the anterior dorsal striatum using a multi-fiber photometry array in head-fixed behaving mice, in response to cues, rewards, and spontaneous licking during the learning and extinction of Pavlovian associations. (4) Glutamate release onto cholinergic interneurons in the anterior dorsal striatum in head-fixed behaving mice, in response to cues, rewards, and spontaneous licking during the learning and extinction of Pavlovian associations; and (5) Behavioral changes following ACh release inactivation in the anterior dorsal striatum during the learning and extinction of Pavlovian associations.These scripts were custom-written by Safa Bouabid and used in the study [Distinct spatially organized striatum-wide acetylcholine dynamics for the learning and extinction of Pavlovian associations.](https://pubmed.ncbi.nlm.nih.gov/39071401/).

------------------
## Folder Structure

The following folders are included in this repository: 

1) Folder [**Commmon Functions**](https://github.com/Safa-Bouabid/Pav-Paper/tree/58d77dc9df8d06ebf460e331e690eda6714c84c1/Common%20functions) has multiple functions necessay for analyzing the data: 
 
   - **commun_functions.m** has multiple function such as:
     - **ball2xy.m**: converts data from optical mouse ball treadmill sensors to m/s^2;
     - **Scatter_3d**:  makes a 3D heatmap bubblePlot of values from a grid recording (x = ML, y = AP, z = DV) based on the fiber location table;
     - **pav2cue_getTrialTimes**: takes as input the path to a behavior file, or the structitself, and returns a struct, with fields: (trial, cue, cueID, cue start/end, reward, reward on, reward lick, trial times etc.);
     - **get_overall_vel_acc**: takes as input the behav file (path or struct) it outputs overall velocity and overall acceleration;
     - **eventTriggeredAverage.m**: general use event-triggered average function.
   - **commun_plot_functions.m**: includes multiple functions for plotting data;
   - **data_ processing_and_organizing.m**: all raw datasets were organized using this script, which processes the source data (both main and supplementary) available on [Zenodo](10.5281/zenodo.14728851) in separate .zip folders. 

2) Folder [**Analysis Codes**](https://github.com/Safa-Bouabid/Pav-Paper/tree/58d77dc9df8d06ebf460e331e690eda6714c84c1/analysis%20codes) contains the processed and organised datasets from the **data_processing_and_organizing.m** script which are then used as inputs in the figure generation scripts (**figure_code.m** and **sup_figure_code.m**) to create the figures for each respective analysis.

------------------
## Data Availability

Both raw datasets and processed and organized datasets are available at [Zenodo](10.5281/zenodo.14728851) in separate .zip folders for each figure.

------------------
## Documentation and Working Example

The processed and organised datasets are used directly by the **figure_code.m** and **sup_figure_code.m** scripts found in [**Analysis Codes**](https://github.com/Safa-Bouabid/Pav-Paper/tree/58d77dc9df8d06ebf460e331e690eda6714c84c1/analysis%20codes) folder to generate panels within each figure (both main and supplementary). The processed and organized data (in .mat or .xlsx format) can be found at [Zenodo](10.5281/zenodo.14728851) in **processed_data** subfolders within individual .zip folders corresponding to each figure. In addition to the **processed_data** subfolder, each .zip folder includes the following files:

1) **CT_across_GXX_mice**, contains information of fiber locations for ACh data mice, and CT_across_DLXX_mice, contains information of fiber locations for DA data mice.
 
2) **across_mice_lick_index_data_whole_ITI.mat** contains licking data from GRAB-ACh and iGluSnFR mice.
   * For each mouse, the `single_trial_struct` field (organized by each recording session) includes lick counts within a specified duration before cue onset (pre-licking) and during the inter-trial interval (ITI-licking). It also contains a lick index calculated based on pre-licking and ITI- licking.
   * The `single_trial_taking_all_ITI_frame` field is similar to `single_trial_struct`, except that ITI-licking is calculated across the entire inter-trial interval.
   * The `single_trial_rew` field contains lick counts during the reward consumption period (0–3 seconds after reward delivery).
   
3) **components_window_activity_filtered_rebase_rew_consump.mat** contains (for each *event_phase*, for each mouse), at single trial level, neural signal triggered at cue_onset/reward_consumption.
   * The three dimension of field `activity` are *timewindow*, *number_of_ROIs+3* and *number_of_trials*.
   * Fields `mu`,`sem` and `null` contains *mean*, *standard error of mean* and *control calculated based on `activity`*.
     *event_phase*: events includes combinations composed of aligning events [cue1/2, rew1/2 (reward of cue1/2),unprd(unpredicted reward)] for learning phase [early,late,LEDomi,Toneomi].
     *number_of_ROIs+3*: +3 is because lick count, linear velocity and angular velocity is appended in front of neural signal along the second dimention of the array `activity`.

4) **components_window_activity_filtered_rebase_rew_consump_rew_merged.mat** has the same structure as **components_window_activity_filtered_rebase_rew_consump.mat**, except that rew1 now contains merged data from rew1 and rew2.
   
5) **event_aligned_highpass03** has a similar structure to **components_window_activity_filtered_rebase_rew_consump**, but the data is organized by recording session instead of learning phases.
   
6) **tri_avg_single_filtered_rebase_rew_consump.mat** contains dimension-reduced data based on **components_window_activity_filtered_rebase_rew_consump**.
   * Field `mu_location_value` contains amplitudes and timings of each waveform component for all ROIs. The three dimentions represents components [early peak,dip,late peak], number of ROIs, measures [amplitudes and timing].
   * Field `mu_location_value_significance` contains significance of each components [early peak,dip,late peak] measured by comparing component amplitudes against control amplitude.
   * Field `single_values` contains, at single trial level, amplitudes of each waveform component for all ROIs. The three dimentions represents components [early peak,dip,late peak], number of ROIs, number of single trials.
   * Field `half_max_dur` contains, duration information of each waveform component for all ROIs measured at the half-max amplitude.
   * The three dimentions represents components [early peak,dip,late peak], number of ROIs, measures [half-max duration, leading timing at half-max amplitude in second, ending timing at half-max amplitude in second, leading timing in frame, ending timing in frame].
   * Field `half_max_dur_single` contains, at single trial level, similar information as `half_max_dur`. The single trial dimension is set to be the fourth dimension.
   
7) **tri_avg_single_filtered_rebase_rew_consump_rew_merged.mat** has the same structure as tri_avg_single_filtered_rebase_rew_consump, except that rew1 now contains the merged data from rew1 and rew2.
   
8) **ITI_licking_components_window_activity_filtered.mat** contains spontaneous lick-onset aligned data of GRAB-ACh mouse.
   * The field `data` contains three cells: [sample_rate, timing of lick-onset in frame, *data array*]. This *data array* have three dimensions, which represents timewindow, *number_of_ROIs+3* and number_of_trials.
   
9) **ITI_licking_components_window_activity_filtered_table** contains same data as ITI_licking_components_window_activity_filtered, except in table format.	

10) **ITI_licking_aligned_highpass03** contains similar structure as ITI_licking_components_window_activity_filtered, but it is organized by each recording session instead of learning phases.

11) **ITI_licking_tri_avg_single_filtered** contains dimension-reduced data based on ITI_licking_components_window_activity_filtered, and has a similar structure as **tri_avg_single_filtered_rebase_rew_consump**.

12) **DA_across_mice_lick_index_data_whole_ITI** contains the same structure as across_mice_lick_index_data_whole_ITI except for this contains licking information of DLight mice.

13) **DA_components_window_activity_filtered** contains neural signal data triggered at cue_onset and reward_consumption for DLight (Dopamine) mice, at the single-trial level, for each *event_phase* and each mouse. It follows a similar structure to **components_window_activity_filtered_rebase_rew_consump**

14) **DA_event_aligned_highpass03** contains similar structure as DA_components_window_activity_filtered, but it is organized by each recording session instead of learning phases.

15) **DA_tri_avg_single_filtered_aDMs_only** contains dimension-reduced data based on DA_components_window_activity_filtered. Note that this data includes only fibers in the anterior dorsal striatum (the exact criteria for aDMs are described in the paper). It follows a similar structure to **tri_avg_single_filtered_rebase_rew_consump**

16) **DA_ITI_lick_ta** contains, with and without highpass, spontaneous lick-onset aligned data during pre-learing (field `pre`) and post-learning phase (field `post`) of DLight mouse.
    * `pre` and `post` are arrays whose three dimensions correspond to timewindow, *number_of_ROIs+3* and number_of_trials, similar to field `activity` in components_window_activity_filtered_rebase_rew_consump.

17) **DA_ITI_lick_ta_table** contains same data as **DA_ITI_lick_ta**, except in table format.

18) **DA_ITI_lick_tas** contains dimension-reduced data based on **DA_ITI_lick_ta**, and has a similar structure as **tri_avg_single_filtered_rebase_rew_consump**.
     
19) **Glu_task_ta** contains (for each *event_phase*, for each mouse) ,at single trial level, neural signal triggered at cue_onset/reward_consumption of iGluSnFR mice, and has a similar structure as **DA_components_window_activity_filtered**.

20) **Glu_task_ta_table** contains same data as Glu_task_ta, except in table format.

------------------
## System Requirements

Any operating system able of running Matlab R2022b and R2020b. 

**Hardware requirement** : RAM (64GB), processor: Intel(R) Core(TM) i7-8700 CPU @ 3.20GHz   3.19 GHz. 

**Software requirement**:  MATLAB can be installed on machines running Windows. MATLAB software requires a paid subscription to be used.

------------------
##  License and Citation
 
If you use use this code in your research, please cite: 

Safa Bouabid, Liangzhu Zhang, Mai-Anh T. Vu, Kylie Tang, Benjamin M. Graham , Christian A. Noggle, Mark W. Howe. (2025) [Distinct spatially organized striatum-wide acetylcholine dynamics for the learning and extinction of Pavlovian associations.](https://pubmed.ncbi.nlm.nih.gov/39071401/).

This repository is released under the [MIT License](https://opensource.org/license/mit) - see the [LICENSE](LICENSE) file for details.

------------------
## Acknowledgements

This research was funded in part by Aligning Science Across Parkinson’s **[ASAP-020370]** through the Michael J. Fox Foundation for Parkinson’s Research (MJFF).
  
  
