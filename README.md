# Reductive-Perturbation-Method-A.-thaliana

The code in the ‘Code’ folder gives data from the Stuart-Landau analysis over 10 models in the following order:
	Locke2005a(sub)	Locke2005b		Zeilinger2006	Pokhilko2010
	Pokhilko2012	Pokhilko2013(sub)	Fogelmark2014	Ohara2015(sub)
	Foo2016		Caluwe2016(sub)

The codes search through all degradation rates as potential bifurcation parameters.

Make sure that the folder is named ‘Code’
Make sure that the directory is ‘Code’

Grand_MostDataPoints.m: Uses the bifurcation parameter that gives the most data points on bifurcation diagrams with the set percentage error criteria.
* This file will take considerably huge amount of time to run through.  So make sure you have set the computer sleep-time to be never, and the computer have enough memory (probably going to take 4-5 GB).

To get data from all models (10 models):
1. Open Grand_MostDataPoints.m 
2. Input at first five lines of Define input values section: theta; mu_min, mu_max, number of data points
3. controlErr: include only data points with in controlErr away from the theory curve. To include full range of mu, set controlErr to larger value - 1 should be enough; though this will always give data from the first potential bifurcation parameter.
4. Run
	
* The code will printout:
1. Potential bifurcation parameters in degradation rate(s) array;
2. For each potential bifurcation parameter, the code will run ode simulation and compute scaled amplitude and frequency.  In this process, the code prints out “the current bifurcation parameter in use”; “the current mu value for the iteration”; (except for mu = 0) the scaled amplitude, scaled frequency, error in scaled amplitude comparing to sqrt(mu), and error in scaled frequency comparing to mu [in this given order].  Errors are computed by (measured - theory)/theory.
3. When either of the error in previous line exceed the controlErr value, code will display either ‘amp’ or ‘freq’ to indicate which value has larger-than-desired error.

Output will be arrays / cell arrays:
Data_amp, Data_freq: data points
BP, criticalValues: bifurcation parameter (which degradation rate) and corresponding c.p.
Lambda1, G, Omega0: Stuart-Landau parameters
Omega_s, RR_s: omega_s and R_s from each model
mu1, mu: independent variables for plotting purposes
Save workspace to save data for later
One plot: 
Scaled amp/freq vs. mu of all models on one plot


To run one individual model:
1. Open Grand_MostDataPoints.m 
2. Run first two sections
3. Find the corresponding model section in section 3, run the first two lines under the model (addpath & main_modelname) OR open corresponding folder and run Main_[ModelName].m.

	    
