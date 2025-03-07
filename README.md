13/02/2025:
A complete update of the state of the project
TSS transient classifier the 4th iteration:

Dependencies:
pip install astropy
pip install astro-datalab

lightcurve_classifier_for_tess.py 
prob_source_is_transient.py 
human_component.py 
external_photometry.py

all_uploaded.csv 
transient_classifications.csv

The program can be configured in the second box
You can change the saved catalogue filename
You can turn on/off whether you have somebody manually check through the matches You can decide how many of the highest matches are addended

Program Description:
This program searches through "all_uploaded.csv" and checks if the filename exists in the TESS_events folder, which contains csv's detailing the mjd and counts of a transient event. It then searches "transient_classifications.csv" for aggregate tags.

For each filename which exists in TESS_events, it is checked if there exists a valid catalogue for that event, it is simply skipped if there is not. A lightcurve is plotted and classified for this event, and the aggregate tags are printed.

For each entry in the catalogue, the probability that that entry is the observed TESS source is determined (informed by - color, distance, magnitude and object type). The top result(s) are then appended with their probability, whether the TESS lightcurve was flagged as a mystery and with the agg tags.

If "human checker" is on, it also prints extra information about the highest probability source, and displays an image so that somebody may determine through answering the prompts if the classification makes sense - and their response is written to the new catalogue.

Creates row(s) for this event with the following information:
filename	identifier	 quick_objecUdra	dee	mag_psf_g	mag_psf_r mag_psf_i	mag_psf_z	mag_auto_g	mag_auto_r	mag_auto_i	mag_auto_z magerr_psf_g magerr_psf_r	magerr_psf_i	magerr_psf_z magerr_auto_g magerr_auto_r

magerr_auto_i magerr_auto_z extended_class_g	extended_class_r	extended_class_i extended_class_z	star	final_probabilities	Mystery Flag	 human_check

Saves this event to csv in your cwd called: the filename defined in the program configuration


Extra considerations implemented:
If the star field is crowded, print a statement saying so.

If the highest probability is low, print a statement saying so.

In human_component you can skip ahead (-- skip events) in the all_uploaded csv in case you'd already classified some and decided to take a break


Things discussed but not implemented:
The probability isn't affected by the aggregate tags, additionally there's currently no way to filter misspelled/awkward aggregate tags. All that is dome about these tags is they're printed and written to the new catalogue

The program is intolerant to any catalogue format which isn't DELVE.

Determining if a source candidate is a red giant and applying a "debuff" to its probability if it is for solar flares.
