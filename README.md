# SFalmanac-Py3

SFalmanac-Py3 is a Python 3 script that creates the daily pages of the Nautical Almanac. These are tables that are needed for celestial navigation with a sextant. Although you are strongly advised to purchase the official Nautical Almanac, this program will reproduce the tables with no warranty or guarantee of accuracy.

SFalmanac-Py3 was developed with the intention of having identical output format as Pyalmanac-Py3. As opposed to the older PyEphem astronomy library, the intention was for it to be based entirely on the newer Skyfield astronomical library: https://rhodesmill.org/skyfield/, however PyEphem is still required to calculate the planet magnitudes.

It uses the star database in Skyfield, which is based on data from the Hipparcos Catalogue. The principal disadvantage is that calculating twilight (actual, civil and nautical sunrise/sunset) and moonrise/moonset is **extremely** slow. As a consequence of this a new hybrid version is available that is four times faster. (The hybrid version uses PyEphem to calculate twilight and moonrise/moonset with only a minimal loss of accuracy.)

NOTE: two scripts are included (both can be run): 'sfalmanac.py' and 'increments.py'  
NOTE: a Python 2.7 script with identical functionality can be found at:  https://github.com/aendie/SFalmanac-Py2  
NOTE: a 100% [PyEphem](https://rhodesmill.org/pyephem/) version of SFalmanac is available here:
https://github.com/aendie/Pyalmanac-Py3  
NOTE: the faster hybrid version is available here: 
https://github.com/aendie/SkyAlmanac-Py3

An aim of this development was to maintain:

* **identical PDF output formatting with a similar control program**  
	 It is then possible to display both generated tables (from PyEphem and Skyfield)
	 and compare what has changed by flipping between the two tabs in Adobe Acrobat Reader DC.
	 Anything that has changed flashes, thereby drawing your attention to it.
	 This crude and simple method is quite effective in highlihgting data that
	 might need further attention.

The results have been crosschecked with USNO data to some extent.  
(However, constructive feedback is always appreciated.)

**UPDATE: Nov 2019**

Declination formatting has been changed to the standard used in Nautical Almanacs. In each 6-hour block of declinations, the degrees value is only printed on the first line if it doesn't change. It is printed whenever the degrees value changes. The fourth line has two dots indicating "ditto". This applies to all planet declinations and for the sun's declination, but not to the moon's declination as this is continuously changing.

This also includes some very minor changes and an improved title page for the full almanac with two star charts that indicate the equatorial navigational stars.

**UPDATE: Jan 2020**

The Nautical Almanac tables now indicate if the sun never sets or never rises; similarly if the moon never sets or never rises. For better performance, the *SunNeverSets* or *SunNeverRises* state is determined only by the month of year and hemisphere. (This is reliable for the set of latitudes printed in the Nautical Almanac tables.) The code also has cosmetic improvements.  
P.S. The *Overfull \hbox in paragraph...* messages can be ignored - the PDF is correctly generated.

**UPDATE: Feb 2020**

The main focus was on cleaning up the TeX code and eliminating the *Overfull/Underfull hbox/vbox* messages. Other minor improvements were included. A Skyfield issue with days that have no moonrise or moonset at a specific latitude was resolved.

**UPDATE: Mar 2020**

A new parameter in *config.py* enables one to choose between A4 and Letter-sized pages. A [new approach](https://docs.python.org/3/whatsnew/3.0.html#pep-3101-a-new-approach-to-string-formatting) to string formatting has been implemented:
the [old](https://docs.python.org/2/library/stdtypes.html#string-formatting) style Python string formatting syntax has been replaced by the [new](https://docs.python.org/3/library/string.html#format-string-syntax) style string formatting syntax. 

**UPDATE: Jun 2020**

The Equation Of Time is shaded whenever EoT is negative indicating that apparent solar time is slow compared to mean solar time (mean solar time > apparent solar time).
It is possible to extend the maximum year beyond 2050 by choosing a different ephemeris in config.py.
Bugfix applied to correct the Meridian Passage times.

## Requirements

&nbsp;&nbsp;&nbsp;&nbsp;Most of the computation is done by the free Skyfield library.  
&nbsp;&nbsp;&nbsp;&nbsp;Typesetting is done by MiKTeX or TeX Live so you first need to install:

* Python v3.4 or higher (the latest version is recommended)
* Skyfield 1.20 (latest tested version - older versions work too)
* Pandas (to load the Hipparcos catalog; tested: 1.0.3)
* PyEphem 3.7.6 or 3.7.7 (required for planet magnitudes)
* TeX/LaTeX&nbsp;&nbsp;or&nbsp;&nbsp;MiKTeX&nbsp;&nbsp;or&nbsp;&nbsp;TeX Live
  

### INSTALLATION GUIDELINES on Windows 10:

&nbsp;&nbsp;&nbsp;&nbsp;Install Python 3.8 (add python.exe to path)  
&nbsp;&nbsp;&nbsp;&nbsp;Install MiKTeX 2.9 from https://miktex.org/  
&nbsp;&nbsp;&nbsp;&nbsp;When MiKTeX first runs it will require installation of additional packages.  
&nbsp;&nbsp;&nbsp;&nbsp;Run Command Prompt as Administrator, go to your Python folder and execute, e.g.:

&nbsp;&nbsp;&nbsp;&nbsp;**cd C:\\Python38-32**  
&nbsp;&nbsp;&nbsp;&nbsp;**pip install --upgrade pip**  
&nbsp;&nbsp;&nbsp;&nbsp;... for a first install:  
&nbsp;&nbsp;&nbsp;&nbsp;**pip install pyephem**  
&nbsp;&nbsp;&nbsp;&nbsp;... if already installed, check for upgrade explicitly:  
&nbsp;&nbsp;&nbsp;&nbsp;**pip install --upgrade pyephem**  
&nbsp;&nbsp;&nbsp;&nbsp;**pip install skyfield**  
&nbsp;&nbsp;&nbsp;&nbsp;**pip install pandas**  

&nbsp;&nbsp;&nbsp;&nbsp;Put the SFalmanac files in a new folder, run Command Prompt and start with:  
&nbsp;&nbsp;&nbsp;&nbsp;**py -3 sfalmanac.py**


### INSTALLATION GUIDELINES on Ubuntu 19.10 or 20.04:

&nbsp;&nbsp;&nbsp;&nbsp;Ubuntu 18.04 and higher come with Python 3 preinstalled,  
&nbsp;&nbsp;&nbsp;&nbsp;however pip may need to be installed:  
&nbsp;&nbsp;&nbsp;&nbsp;**sudo apt install python3-pip**

&nbsp;&nbsp;&nbsp;&nbsp;Install the following TeX Live package:  
&nbsp;&nbsp;&nbsp;&nbsp;**sudo apt install texlive-latex-extra**

&nbsp;&nbsp;&nbsp;&nbsp;Install the required astronomical libraries etc.:  
&nbsp;&nbsp;&nbsp;&nbsp;**pip3 install pyephem**  
&nbsp;&nbsp;&nbsp;&nbsp;**pip3 install skyfield**  
&nbsp;&nbsp;&nbsp;&nbsp;**pip3 install pandas**  

&nbsp;&nbsp;&nbsp;&nbsp;Put the SFalmanac files in a folder and start with:  
&nbsp;&nbsp;&nbsp;&nbsp;**python3 sfalmanac.py**  


### INSTALLATION GUIDELINES on MAC:

&nbsp;&nbsp;&nbsp;&nbsp;Every Mac comes with python preinstalled.  
&nbsp;&nbsp;&nbsp;&nbsp;(Please choose this version of SFalmanac if Python 3.* is installed.)  
&nbsp;&nbsp;&nbsp;&nbsp;You need to install the PyEphem and Skyfield libraries to use SFalmanac.  
&nbsp;&nbsp;&nbsp;&nbsp;Type the following commands at the commandline (terminal app):

&nbsp;&nbsp;&nbsp;&nbsp;**sudo easy_install pip**  
&nbsp;&nbsp;&nbsp;&nbsp;**pip install pyephem**  
&nbsp;&nbsp;&nbsp;&nbsp;**pip install skyfield**  
&nbsp;&nbsp;&nbsp;&nbsp;**pip install pandas**  

&nbsp;&nbsp;&nbsp;&nbsp;If this command fails, your Mac asks you if you would like to install the header files.  
&nbsp;&nbsp;&nbsp;&nbsp;Do so - you do not need to install the full IDE - and try again.

&nbsp;&nbsp;&nbsp;&nbsp;Install TeX/LaTeX from http://www.tug.org/mactex/

&nbsp;&nbsp;&nbsp;&nbsp;Now you are almost ready. Put the SFalmanac files in any directory and start with:  
&nbsp;&nbsp;&nbsp;&nbsp;**python sfalmanac**  
&nbsp;&nbsp;&nbsp;&nbsp;or  
&nbsp;&nbsp;&nbsp;&nbsp;**./sfalmanac**
