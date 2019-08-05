

# Origin of Codes

This is a repo forked from [shupp/sgp4](https://github.com/shupp/sgp4)

The original data comes from [CelesTrak.com](https://www.celestrak.com/publications/AIAA/2006-6753/).
- [Source code](https://www.celestrak.com/publications/AIAA/2006-6753/AIAA-2006-6753.zip) (C++, FORTRAN, Java, MATLAB, Pascal, 1,229,282 bytes)

2019/08/05:\
I have replaced all codes from shupp/sgp4 with those from CelesTrak.com. The `tmatvera.out` file was missing in repo `shupp/sgp4` and is added now.


# My Initialization Modifications

Original codes include implementation and validation of SGP4/SDP4 using four languages: C++, Fortran, Java, MATLAB, and Pascal. 
The work is very well organized and the multi-language implementation works as a great cross-validation to each other.

I just need matlab for my own research, so I decide to prune other languages. 

I improved this README file, with some minor corrections.

To verify your installation, execute the `testmat` script in Matlab. 
- At the input type prompt, `input opsmode afspc a, improved i `, enter `a`. 
- At the input type prompt to choose , `input type of run c, v, m: `, enter `v`.
  - `c`: compare 1 year of full satcat data
  - `v`: verification run, requires modified elm file with
  - `m`: maunual operation- either mfe, epoch, or dayof yr start stop and delta times
- At the input type prompt to choose which WGS model (Earth shape), `input constants 721, 72, 84 `, enter `72`.
- At the input type prompt, `input elset filename: `, enter `SGP4-VER.TLE`.

Then you can get an output file `tmatver.out`, which is exactly the same to that comes with the distribution from CelesTrak.com in file `tmatvera.out`.

With other inputs, the results vary. Just try it!


------------
(Original Descriptions of the codes. Not exactly correct.)

See [CelesTrak.com](https://www.celestrak.com/publications/AIAA/2006-6753/) for more information.

# Matlab

The Matlab version is due to Jeff Beck who performed the original translation. He provides the following notes. 
The code is a line-by-line translation of Vallado's C++ version of 28 Jun 05. 
The files are grouped below according to the “unit” “io” “ext” files in the other languages.
Matt Schmunk has provided a vectorized form of Matlab that should run significantly faster. 
It has not been fully tested against the other approaches yet.

## Contents:
Name | Description
-----|------------
testmat.m | Driver script for testing and example usage
sgp4.m | Main sgp4 routine
sgp4init.m | Initialization routine for sgp4
initl.m | Initialization for sgp4
dsinit.m | Deep space initialization
dspace.m | Deep space perturbations
dpper.m | Deep Space periodics
dscom.m | Deep Space common variables
twoline2rv.m | TLE conversion routine
angl.m Find | the angle between two vectors
constmath.m | set mathematical constants
days2mdh.m | convert days to month day hour minute second
getgravc.m | Get the gravity constants
gstime.m | Find Greenwich sidereal time
invjday.m | Inverse Julian Date
jday.m | Find the Julian Date
mag.m | Magnitude of a vector
newtonnnu.m | Kepler’s iteration given eccentricity and true anomaly
rv2coe.m | Convert position and velocity vectors to classical orbital elements
debug*.m | Debug routines to print out intermediate variables at the end of each function call

To verify your installation, execute the testmat script in Matlab. 
At the input type prompt, enter "v". 
At the input elset prompt, enter "sgp4-ver.tle". 
The elset numbers will scroll down the screen and some error messages will appear. 
When execution is complete, do a file comparison of your output file "tmatver.out" with "tmatver.af80" (or "tmatver.gsfc" if you elected to comment out the AF80 inclination selection in dpper).
To generate debug output, execute the following lines in Matlab before executing sgp4test:
```matlab
global idebug
idebug = 1;
```