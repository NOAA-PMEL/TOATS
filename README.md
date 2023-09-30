# TOATS
Best practices for assessing Trends of Ocean Acidification Time Series (TOATS)

CONTENTS OF THIS FILE
--------------------

 * Legal disclaimer
 * Introduction
 * Requirements
 * Installation
 * Troubleshooting
 * FAQ
 * Maintainers
 
LEGAL DISCLAIMER
-----------------------
***

_This repository is a software product and is not official communication of the National Oceanic and Atmospheric Administration (NOAA), or the United States Department of Commerce (DOC). All NOAA GitHub project code is provided on an 'as is' basis and the user assumes responsibility for its use. Any claims against the DOC or DOC bureaus stemming from the use of this GitHub project will be governed by all applicable Federal law. Any reference to specific commercial products, processes, or services by service mark, trademark, manufacturer, or otherwise, does not constitute or imply their endorsement, recommendation, or favoring by the DOC. The DOC seal and logo, or the seal and logo of a DOC bureau, shall not be used in any manner to imply endorsement of any commercial product or activity by the DOC or the United States Government._

INTRODUCTION
------------
***

*Best practices for assessing Trends of Ocean Acidification Time Series (TOATS)* is a supplement to Sutton AJ, Battisti R, Carter B, Evans W, Newton J, Alin S, Bates NR, Cai W-J, Currie K, Feely RA, Sabine C, Tanhua T, Tilbrook B and Wanninkhof R (2022) Advancing best practices for assessing trends of ocean acidification time series. Front. Mar. Sci. 9:1045667. doi: 10.3389/fmars.2022.1045667.

This open-source code is a package of techniques for assessing trends of ocean acidification time series.  These best practices are best suited for time series capable of characterizing seasonal variability, typically those with sub-seasonal (ideally monthly or more frequent) data collection.  We aim that this package of best practices will help expand the community of practice in ocean acidification trend analysis, testing these and new techniques across a diversity of data sets for future improvement and expansion of this code.  

Data analysists do not need Python programming experience to run the code. The user installs Python, creates and activates the environment, and opens and runs the Jupyter Notebook in a browser, all of which are described in detail here. The user also needs to create a data file that includes a column of datetimes and preceding columns of values for the carbon and carbon-related variables of interest. When the program is run, a user interface at the beginning will guide the file upload and ask the user to input some metadata about the input variables. The program will complete the trend analysis and generate a report for each variable including figures, linear regression statistics, the estimate of the number of years of observations needed to detect a statistically significant trend, and a description of the time series variability and uncertainty. 

THIS IS A PRE-PUBLICATION VERSION OF TOATS. If accepted for publication, a description of the method will be described in the associated open-source paper.

REQUIREMENTS
------------
***

**Python setup instructions**

You must have Python installed before you can proceed any further. Common installation approaches are to download a package distribution such as Anaconda or Miniconda. To install Anaconda, please refer to https://docs.anaconda.com/anaconda/install/. To install Miniconda, please refer to https://docs.conda.io/en/latest/miniconda.html, then open the command or conda prompt and install the following additional packages with `pip install [package name]` or `conda install [package name]`: jupyter, numpy, pandas, matplotlib, statsmodels, requests, and tabulate. If using Anaconda or the conda package and environment management system, please refer to the terms and conditions at www.anaconda.com.

**Data File**

Prepare a .csv or .txt file with datetime in the first column and carbon variables in subsequent columns. The first row should have the names of the variables without any spaces (e.g., "pCO2_sw"). Any bad data values should be removed prior to loading into this program or replaced with "NaN". Save the file in the same location on your computer where TOATS.ipynb is saved. The first column must be the date/datetime column.

This code uses the pandas to_datetime function, which can automatically handle several datetime formats.  For the best results, ensure the date in the first column of the data file is in one of the following formats:
* Sep 1, 2022 
* September 1, 2022
* 09/01/2022
* Sep-01-2022
* 01/Sep/2022
* 2022-09-01
* 01Sep2022

Each of these date formats can include times formated with colons (ex. 14:00, 19:17:00). Times should use the 24 hour format rather than the 12 hour format.

The pandas to_datetime function is US-centric, but dates in the dd/MM/yyyy and dd-MM-yyyy formats will also parse correctly. The notebook will attempt to determine whether days come before or after months. If the notebook cannot (for example, the user's data only includes days 1-12), the user will be prompted to specify whether days come first or second.

If your datetimes are not easily converted to the above examples, datetimes without separators (without -, /, or :) are also an acceptable format. If the notebook detects any of these formats, the user will be prompted to provide a format string (see examples for the look of the format):
* 20221101, which has the format yyyymmdd 
* 011122, which has the format ddmmyy
* 11012022 091500, which has the format mmddyyyy hhmmss
* 220111 09, which has the format yyddmm hh

ISO8601 datetime, which has the format yyyy-MM-ddTHH:mm:ss, is also an acceptable format.

Datetime formats must meet the following conditions:
* The same format must be consistent throughout the dataset.
* If there is both date and time, they must be separated by a single space.
* If there is both date and time, date must come before time.
* year (yy or yyyy), month (mm), and day (dd) are all required in the date
* hour (hh) is required if time is included. Minutes (mm) and seconds (ss) are optional.
* Months, days, hours, minutes, and seconds should be represented by two characters (ex. 09 is acceptable, neither 9 nor 009 are acceptable). These are represented as mm (month), dd (day), hh (hour), mm (minute), ss (second) in the format string.
* Years can have either two or four characters (ex. 99 or 1999 are both acceptable, 999 is not). Year is represented as yy or yyyy in the format string. 

INSTALLATION
------------
***

**Setup Instructions (PC and Mac)**
* You may save the notebook (.ipynb) and environment (.yml) file anywhere you wish, but it will be assumed in these instructions that they reside in your Documents folder
* Go to the start menu and launch the conda prompt
* From within the prompt, type `cd Documents` 
* Create the environment by typing `conda env create -f envTOATS.yml`
* Activate the environment with `conda activate envTOATS` (This step must be done every time you open the jupyter notebook)
* Start your jupyter notebook with `jupyter notebook` (This will open jupyter notebook in a browser)
* From within the jupyter notebook, navigate to and open TOATS.ipynb and follow the instructions contained in the notebook

**Running the code**

To run a cell with code, put your cursor in that cell and select the "Run" button on the toolbar.

Dialogue within the notebook will guide the user to enter the data file name and the name of the time series. For each variable of interest (each column past the first), the user will be asked the desired number of decimal points and the uncertainty to use in the analysis as well as the units that will be used in the figures.

The cells should be run sequentially. Near the end of the notebook, in the Summary report section, the user will be prompted to select one of the variables and will receive summary statistics for that variable. These two cells can be rerun, selecting different variables to summarize without needing to rerun the entire notebook. Once the analysis of one data file is complete and the user would like to start an analysis on a new data file, restart the kernel and clear output, then start over from the beginning. 

TROUBLESHOOTING
------------
***

We use Issues in GitHub to keep track of bugs, enhancements, or other requests. To submit an Issue, navigate to the main page of the repository. Under the repository name, select "Issues". Select "New issue". Select "Get started" next to the type of issue you'd like to open. Enter a title and description for your issue and select "Submit new issue".

We are committed to creating a welcoming and safe environment for everyone, and as such, have adopted the Contributor Covenant (www.contributor-covenant.org):  
[![Contributor Covenant](https://img.shields.io/badge/Contributor%20Covenant-2.1-4baaaa.svg)](code_of_conduct.md) 

FAQ
------------
***

Q: The code returns a linear regression slope error of zero for my seawater pH time series: pH slope (total scale) = -0.001 ± 0. per year.  Is the error really 0?

A: It is likely that Python is not returning trailing zeros in the standard error rounded to the user-defined decimal place. Try running the notebook again adding one additional decimal place when prompted by the dialogue box at the beginning.

Q: The plots are not displaying properly when running TOATS.ipynb.

A: Try replacing '%matplotlib notebook' with '%matplotlib inline' in the first code block of TOATS.ipynb. This will cause a loss of the interative functions of the plots, but is an alternative to displaying them.

MAINTAINERS
------------
***

Roman Battisti, NOAA's Pacific Environmental Laboratory and University of Washington's Cooperative Institute for Climate, Ocean, and Ecosystem Studies - https://github.com/Roman-Battisti

Adrienne Sutton, NOAA's Pacific Environmental Laboratory - https://github.com/adriennejune
