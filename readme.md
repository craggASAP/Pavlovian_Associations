# Project Title
    Distinct spatially organized striatum-wide acetylcholine dynamics for the learning and extinction of Pavlovian associations
 # Project Overview
    This repository contains scripts for analyzing and plotting: 1) ACh release dynamics across the 3D volume of the striatum using a multi-fiber photometry array in head-fixed behaving mice, in response 
    to cues, rewards, and spontaneous licking during the learning and extinction of Pavlovian associations. 2) Behavioral changes (licking and movement) during the learning and extinction of Pavlovian 
    associations. 3) DA release dynamics in the anterior dorsal striatum using a multi-fiber photometry array in head-fixed behaving mice, in response to cues, rewards, and spontaneous licking during the 
    learning and extinction of Pavlovian associations. 4) Glutamate release onto cholinergic interneurons in the anterior dorsal striatum in head-fixed behaving mice, in response to cues, rewards, and 
    spontaneous licking during the learning and extinction of Pavlovian associations. 5) Behavioral changes following ACh release inactivation in the anterior dorsal striatum during the learning and 
    extinction of Pavlovian associations
# Folder Structure 
    the following folders are included in this repository: 
    1) commmon functions: has multiple functions necessay for analyzing the data for example: 
         - commun_functions.m has multiple function such as a) ball2xy.m: convert data from optical mouse ball treadmill sensors to m/s^2.  b) Scatter_3d:  makes a 3D heatmap bubblePlot of values from a grid recording (x = ML, y = 
            AP, z = DV) based on the fiber location table.  c) pav2cue_getTrialTimes: This function takes as input the path to a behavior file, or the structitself, and returns a struct, with fields: (trial, cue, cueID, cue 
            start/end, reward, reward on, reward lick, trial times etc...). d)  get_overall_vel_acc: this function takes as input the behav file (path or struct) it outputs overall velocity and overall acceleration. e) 
             eventTriggeredAverage.m: general use event-triggered average function. etc.... 
	 - commun_plot_functions.m: include multiple functions for plotting data
         - data_ processing_and_otganizing.m: all the raw datasets were organized using the data_processing_and_organizing.m script. This script processes the source data (both main and supplementary) available on Zenodo. 
    2) analysis codes: The generated datasets (from the data_processing_and_organizing.m script) are then used as inputs in the figure generation scripts (figure_code.m and sup_figure_code.m) to create the figures for each 
    respective analysis.  
# Documentation and Workin Example
    These datasets are used directly by the figure_code.m and sup_figure_code.m scripts to generate each figure. The code for each figure and supplementary figure loads and utilizes the following processed and organized data, 
    which can be found on Zenodo in the 'processed_data' folder corresponding to each figure, this incluce:
	1) across_mice_lick_index_data_whole_ITI.mat
		This .mat contains licking data from GRAB-ACh and iGluSnFR mice. 
		For each mouse, the `single_trial_struct` field (organized by each recording session) includes lick counts within a specified duration before cue onset (pre-licking) and during the inter-trial interval (ITI-licking). It also contains a lick index calculated based on pre-licking and 
                 ITI- licking. The single_trial_taking_all_ITI_frame field is similar to single_trial_struct, except that ITI-licking is calculated across the entire inter-trial interval.
		The single_trial_rew field contains lick counts during the reward consumption period (0–3 seconds after reward delivery). 
	2) components_window_activity_filtered_rebase_rew_consump.mat
 	This .mat file contains neural signal data (at the single-trial level) for each event_phase and each mouse, aligned to cue onset or reward consumption.
	The activity field is a three-dimensional array with dimensions: [time window, number of ROIs + 3, number of trials].
	The fields mu, sem, and null contain the mean, standard error of the mean (SEM), and control values, respectively, calculated based on activity.
	Notes:
	event_phase: Events consist of different alignments, where cue and reward events (cue1/2, rew1/2—rewards for cue1/2, unprd—unpredicted reward) are analyzed across different learning phases (early, late, LEDomi, Toneomi).
	number of ROIs + 3: The +3 accounts for the inclusion of lick count, linear velocity, and angular velocity, which are appended in front of the neural signal along the second dimension of the activity array.	
	3) components_window_activity_filtered_rebase_rew_consump_rew_merged.mat
         This file has the same structure as components_window_activity_filtered_rebase_rew_consump.mat, except that rew1 now contains merged data from rew1 and rew2.			
	4) event_aligned_highpass03
		This file has a similar structure to components_window_activity_filtered_rebase_rew_consump, but the data is organized by recording session instead of learning phases
	5) tri_avg_single_filtered_rebase_rew_consump.mat
        This file contains dimension-reduced data based on components_window_activity_filtered_rebase_rew_consump.
        The mu_location_value field contains the amplitudes and timings of each waveform component for all ROIs. Its three dimensions represent:
        1- Components (early peak, dip, late peak)
        2- Number of ROIs
        3- Measures (amplitude and timing).
        The mu_location_value_significance field contains the significance of each component (early peak, dip, late peak) by comparing the component amplitudes against the control amplitude.
        The single_values field contains, at the single-trial level, the amplitudes of each waveform component for all ROIs. Its three dimensions represent:
        1- Components (early peak, dip, late peak)
        2- Number of ROIs
        3- Number of single trials.
        The half_max_dur field contains the duration information of each waveform component for all ROIs, measured at the half-max amplitude. Its three dimensions represent:
        1- Components (early peak, dip, late peak)
        2- Number of ROIs
        3- Measures (half-max duration, leading timing at half-max amplitude in seconds, ending timing at half-max amplitude in seconds, leading timing in frames, and ending timing in frames).
        The half_max_dur_single field contains, at the single-trial level, similar information as half_max_dur. The single-trial dimension is represented as the fourth dimension.	
	6) tri_avg_single_filtered_rebase_rew_consump_rew_merged.mat
		This file has the same structure as tri_avg_single_filtered_rebase_rew_consump, except that rew1 now contains the merged data from rew1 and rew2.
	7) ITI_licking_components_window_activity_filtered.mat
		This contains spontaneous lick-onset aligned data of GRAB-ACh mouse.
		The field `data` contains three cells: [sample_rate, timing of lick-onset in frame, *data array*]. This *data array* have three dimensions, which represents timewindow, *number_of_ROIs+3* and number_of_trials.	
	8) ITI_licking_components_window_activity_filtered_table
		This contains same data as ITI_licking_components_window_activity_filtered, except in table format.	
	9) ITI_licking_aligned_highpass03
		This contains similar structure as ITI_licking_components_window_activity_filtered, but it is organized by each recording session instead of learning phases.
	10) ITI_licking_tri_avg_single_filtered
		This contains dimension-reduced data based on ITI_licking_components_window_activity_filtered.
		This has a similar structure as tri_avg_single_filtered_rebase_rew_consump.	
	11) DA_across_mice_lick_index_data_whole_ITI
		This contains the same structure as across_mice_lick_index_data_whole_ITI except for this contains licking information of DLight mice. 
	12) DA_components_window_activity_filtered
		This file contains neural signal data triggered at cue_onset and reward_consumption for DLight (Dopamine) mice, at the single-trial level, for each event_phase and each mouse. It follows a similar structure to components_window_activity_filtered_rebase_rew_consump	
	13) DA_event_aligned_highpass03
		This contains similar structure as DA_components_window_activity_filtered, but it is organized by each recording session instead of learning phases.
	14) DA_tri_avg_single_filtered_aDMs_only
		This file contains dimension-reduced data based on DA_components_window_activity_filtered. Note that this data includes only fibers in the anterior dorsal striatum (the exact criteria for aDMs are described in the paper).
                It follows a similar structure to tri_avg_single_filtered_rebase_rew_consump
	15) DA_ITI_lick_ta
		This file contains spontaneous lick-onset aligned data, both with and without highpass filtering, during the pre-learning (field pre) and post-learning (field post) phases of DLight mice. 
                The pre and post fields are arrays with three dimensions, corresponding to:
                1- Time window
                2- Number of ROIs + 3
                3- Number of trials
                This structure is similar to the activity field in components_window_activity_filtered_rebase_rew_consump
	16) DA_ITI_lick_ta_table
		This contains same data as DA_ITI_lick_ta, except in table format.
	17) DA_ITI_lick_tas
		This contains dimension-reduced data based on DA_ITI_lick_ta.
		This has a similar structure as tri_avg_single_filtered_rebase_rew_consump.	
	18) Glu_task_ta
		This contains (for each *event_phase*, for each mouse) ,at single trial level, neural signal triggered at cue_onset/reward_consumption of iGluSnFR mice.
		This has a similar structure as DA_components_window_activity_filtered.	
	19) Glu_task_ta_table
		his contains same data as Glu_task_ta, except in table format.
  # System Requirement
    Any operating system able of running Matlab R2022b and R2020b. 
    Hardware requirement : RAM (64GB), processor: Intel(R) Core(TM) i7-8700 CPU @ 3.20GHz   3.19 GHz. 
    Software requirement:  MATLAB can be installed on machines running Windows. MATLAB software requires a paid subscription to be used. 
  # License and Citation 
    If you use use this code in your research, please cite: Safa Bouabid, Liangzhu Zhang, Mai-Anh T. Vu, Kylie Tang, Benjamin M. Graham , Christian
    A. Noggle, Mark W. Howe. (2025) Distinct spatially organized striatum-wide acetylcholine dynamics for the learning and
    extinction of Pavlovian associations
  # Acknoledgement 
    This research was funded in part by Aligning Science Across Parkinson’s [ASAP-020370] through the Michael J. Fox Foundation for Parkinson’s 
    Research (MJFF).
  
  
