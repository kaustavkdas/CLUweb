# ZTF II-CLU Follow-up Web Application

This is a local Python browser application for tracking candidate sources in the Caltech ZTF Census of the Local Universe (CLU) experiment, a volume-luminosity limited supernova sample. The code aggregates sources from the Fritz marshal saved by a scanner to CLU. The web application presents plots and tables summarizing these sources and presenting the current classification completeness of the sample.

# About CLU
At present, the CLU experiment aims to save and classify all subluminous (peaking at magnitudes fainter than -17) supernovae within 150 Mpc (z<0.0331) that are less than 30 kpc (for z>0.01) and/or visibly associated with a CLU host galaxy. CLU host galaxies are those in the Cook et al. 2019 CLU-compliled catalog of ∼234,500 galaxies within 200 Mpc. Supernovae peaking brighter than -17 and/or outside the 150 Mpc volume (but still within 200 Mpc, the limits of the CLU galaxy catalog) are still saved to the Fritz group, but are not targets for spectroscopic follow-up.

# Running the Web Application
Prerequisites
You must be a member of the Census of the Local Universe Caltech group on Fritz (group ID: 43) to use this web application as-is; the current CLU experiment parameters are hard-coded. The versions of various Python packages used in the development of this web application are specified in requirements.txt.

# Getting Started
First, copy and paste your Fritz API access token as specified in user_info.json.

After navigating to the main directory, simply run the application from the terminal/command prompt with the following command:

python sc.py -d [START DATE] -r [REFRESH DATE]

Dates must be specified in YYYY-MM-DD format. By default, the start date is 2021-01-01 and there is no refresh date.

In all use cases, new sources saved to CLU on Fritz will be appended to the most recent .ascii file in query_data (eg. CLU_Query_2022_1_5.ascii). If a refresh date is specified, sources saved after that date are treated as "new" and updated data from Fritz will be downloaded accordingly. Additionally, any query files older than two weeks are automatically deleted from the folder when sc.py is run.

If all goes well, a Flask-based webpage should automatically open in your browser on port 4000. If your computer localhost address is not the default 127.0.0.1, please edit line 113 in sc.py to the correct localhost address.

# Force Refresh Functionality
By not specifying a refresh date, previously downloaded data will not be updated, meaning that new classifications, photometry, and spectra will not be saved. Therefore, it is generally recommended to always refresh one to two months prior to the current date you run the application, especially if there has been a recent observing run.

For example, on 2022-01-05, one might run the following: python sc.py -d 2021-01-01 -r 2021-12-01

The refresh date also takes the string all as an argument. This will redownload the most current data starting from the specified start date, and it is recommended to use this function to fully update the data for any analysis using the query files.

# Source Duplicates
Occasionally, duplicate sources are created through the ZTF pipeline (especially prevalent in April 2022). There is now a new classification taxonomy on Fritz used to mark these duplicates. Running sc.py now has the parameter --removeduplicates which removes any sources saved to CLU that have been marked as duplicates from completeness statistics and related plots (all sources saved to CLU meeting your query dates are downloaded regardless of their duplicate status). This setting is on by default. To keep duplicates in the completeness statistics/plots, include the parameter --no-removeduplicates when running sc.py from the terminal.

# Further Notes
This web application was intitally developed by Andy Tzanidakis and modified by Tawny Sit. Kaustav K. Das **(kdas@astro.caltech.edu)** is the current maintainer and has made few edits to the underlying code.

Feature suggestions and bug reports are welcome!
