# Project Name:
	Spatially organized striatum-wide acetylcholine dynamics for the learning and extinction of Pavlovian cues and actions

# datasets:
	These datasets were generated using the script `data_processing_and_organizing.m` applied to the data in `raw_data` folder.
	These datasets were used directed by `figure_code.m` and `sup_figure_code.m` scripts.
	P.S. Data redundency exist among datasets due to consideration of convenience during programing .
	
	* across_mice_lick_index_data_whole_ITI
		This .mat contains licking information of GRAB-ACh and iGluSnFR mice. 
		For each mouse, field `single_trial_struct` contains (organized by each recording session separately) lick counts within a specified duration before cue onset (pre-licking) and reward onset (iti-licking). It also contains an lick index calculated based on pre-licking and iti-licking.
		Field `single_trial_taking_all_ITI_frame` contains similar thing as `single_trial_struct`, except for that iti-licking is calculated by considering the whole inter-trial interval.
		Field `single_trial_rew` contains lick counts for reward consumption period (0-3 seconds) after reward deliverty.
		
	* components_window_activity_filtered_rebase_rew_consump
		This .mat contains (for each *event_phase*, for each mouse) ,at single trial level, neural signal triggered at cue_onset/reward_consumption.
		The three dimension of field `activity` are timewindow, *number_of_ROIs+3* and number_of_trials. 
		Fields `mu`,`sem` and `null` contains mean, standard error of mean and control calculated based on `activity`.
		P.S. 
			*event_phase*: events includes combinations composed of aligning events [cue1/2, rew1/2 (reward of cue1/2),unprd(unpredicted reward)] against learning phase [early,late,LEDomi,Toneomi].
			*number_of_ROIs+3*: +3 is becase lick count, linear velocity and angular velocity is appended in front of neural signal along the second dimention of the array `activity`.
			
	* components_window_activity_filtered_rebase_rew_consump_rew_merged.mat
		This contains the same structure as components_window_activity_filtered_rebase_rew_consump except for that rew1 now contains the merged data of rew1 and rew2.
		
	* event_aligned_highpass03
		This contains similar structure as components_window_activity_filtered_rebase_rew_consump, but it is organized by each recording session instead of learning phases.
	
	* tri_avg_single_filtered_rebase_rew_consump
		This contains dimension-reduced data based on components_window_activity_filtered_rebase_rew_consump.
		Field `mu_location_value` contains amplitudes and timings of each waveform component for all ROIs. Its three dimentions represents components [early peak,dip,late peak], number of ROIs, measures [amplitudes and timing].
		Field `mu_location_value_significance` contains significance of each components [early peak,dip,late peak] measured by comparing component amplitudes against control amplitude.
		Field `single_values` contains, at single trial level, amplitudes of each waveform component for all ROIs. It's three dimentions represents components [early peak,dip,late peak], number of ROIs, number of single trials.
		Field `half_max_dur` contains, duration information of each waveform component for all ROIs measured at the half-max amplitude. 
			Its three dimentions represents components [early peak,dip,late peak], number of ROIs, measures [half-max duration, leading timing at half-max amplitude in second, ending timing at half-max amplitude in second, leading timing in frame, ending timing in frame].
		Field `half_max_dur_single` contains, at single trial level, similar information as `half_max_dur`. The single trial dimension is set to be the fourth dimension.
		
	* tri_avg_single_filtered_rebase_rew_consump_rew_merged
		This contains the same structure as tri_avg_single_filtered_rebase_rew_consump except for that rew1 now contains the merged data of rew1 and rew2.
	
	* ITI_licking_components_window_activity_filtered
		This contains spontaneous lick-onset aligned data of GRAB-ACh mouse.
		The field `data` contains three cells: [sample_rate, timing of lick-onset in frame, *data array*]. This *data array* have three dimensions, which represents timewindow, *number_of_ROIs+3* and number_of_trials.
		
	* ITI_licking_components_window_activity_filtered_table
		This contains same data as ITI_licking_components_window_activity_filtered, except in table format.
		
	* ITI_licking_aligned_highpass03
		This contains similar structure as ITI_licking_components_window_activity_filtered, but it is organized by each recording session instead of learning phases.
		
	* ITI_licking_tri_avg_single_filtered
		This contains dimension-reduced data based on ITI_licking_components_window_activity_filtered.
		This has a similar structure as tri_avg_single_filtered_rebase_rew_consump.
		
	* DA_across_mice_lick_index_data_whole_ITI
		This contains the same structure as across_mice_lick_index_data_whole_ITI except for this contains licking information of DLight mice. 
		
	* DA_components_window_activity_filtered
		This contains (for each *event_phase*, for each mouse) ,at single trial level, neural signal triggered at cue_onset/reward_consumption of DLight mice.
		This contains a similar structure as components_window_activity_filtered_rebase_rew_consump.
		
	* DA_event_aligned_highpass03
		This contains similar structure as DA_components_window_activity_filtered, but it is organized by each recording session instead of learning phases.
	
	* DA_tri_avg_single_filtered_aDMs_only
		This contains dimension-reduced data based on DA_components_window_activity_filtered. Note that this data only includes fibers in anterior dorsal striatum (the exact criteria for aDMs is described in the paper).
		It has similar structure as tri_avg_single_filtered_rebase_rew_consump.
	
	* DA_ITI_lick_ta
		This contains, with and without highpass, spontaneous lick-onset aligned data during pre-learing (field `pre`) and post-learning phase (field `post`) of DLight mouse.
		`pre` and `post` are arrays whose three dimensions correspond to timewindow, *number_of_ROIs+3* and number_of_trials, similar to field `activity` in components_window_activity_filtered_rebase_rew_consump.
	
	* DA_ITI_lick_ta_table
		This contains same data as DA_ITI_lick_ta, except in table format.
		
	* DA_ITI_lick_tas
		This contains dimension-reduced data based on DA_ITI_lick_ta.
		This has a similar structure as tri_avg_single_filtered_rebase_rew_consump.
		
	* Glu_task_ta
		This contains (for each *event_phase*, for each mouse) ,at single trial level, neural signal triggered at cue_onset/reward_consumption of iGluSnFR mice.
		This has a similar structure as DA_components_window_activity_filtered.
		
	* Glu_task_ta_table
		his contains same data as Glu_task_ta, except in table format.
	