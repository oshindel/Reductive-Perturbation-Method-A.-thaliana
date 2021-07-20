# Reductive-Perturbation-Method-A.-thaliana

The code in the ‘Code’ folder gives data from the Stuart-Landau analysis over 10 models in the following order:
	Locke2005a(sub)	   Locke2005b		Zeilinger2006	  Pokhilko2010
	Pokhilko2012	   Pokhilko2013(sub)	Fogelmark2014	  Ohara2015(sub)
	Foo2016		   Caluwe2016(sub)

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

Here is a description of the files:
The MATLAB_Code folder contains the Grand\_MostDataPoints.m file, and ten folders, one for each model.
Grand_MostDataPoints.m runs the simulation for all models and uses the bifurcation parameter that gives the most data points on bifurcation diagrams with the set percentage error criteria.  Each model folder contains the following files:

1. Main_[ModelName].m, which includes all major steps for choosing bifurcation parameter and calculating Stuart-Landau parameters.
2. Simulate_Circadian_[ModelName].m, which includes the steps for simulation using MATLAB ODE solver.
3. Circadian_[ModelName].mlx, which is the live script function file including all ODEs.  The typeset equations and set(s) of parameter values are also included in this file.
4. Circadian_syms_[ModelName].m, which is the function file including all ODEs.  This file is identical to item 3, but all the parameters and variables are symbolic variables using MATLAB Symbolic Toolbox.
5. Filter.m, which finds all degradation rates that lead to bifurcation.  The searching range of bifurcation is between 0 to the optimal value.  The critical values are also generated through this process.
6. Solve_cp.m, which solves for critical values of the bifurcation parameter with given range.  The function uses binary search.
7. Generate_values.m, which, for each degradation rates that lead to a bifurcation, calculates Stuart-Landau parameters omega_0 and g=g'+ig'', as well as the eigenvalues and eigenvectors of the Jacobian evaluated at criticality.
8. Calc_sigma_omega.m which, for each degradation rates that lead to a bifurcation, calculates the values of sigma_1 and omega_1.
9. Calc_lambdas.m, which returns the two eigenvalues with largest real parts.  These two eigenvalues should be complex conjugate of each other.
10. Jacobian.m, which generates the symbolic Jacobian of the system of equations, L.
11. third_tensor.m, which generates the symbolic third degree tensor of the system of equations, M.
12. fourth_tensor.m, which generates the symbolic fourth degree tensor of the system of equations, N.
13. FixedPt.m, which find the fixed point of the system of equation with given parameter values.  The function uses MATLAB fsolve.
14. Evaluation.m, which substitutes in values for parameter values in a symbolic expressions, e.g. L, M and N.
15. Evaluation_fp.m, which substitutes in values for variables at fixed point in a symbolic expressions, e.g. L, M and N.
16. Mult.m, which multiplies a tensor and a vectot together.  This function compresses the tensor along the last dimension.
17. eigen.m, which returns sorted eigenvalues and eigenvectors.  The eigenvalues and eigenvectors are sorted with respect to real parts of eigenvalues from small to large.

For the models that is in the post-bifurcation region in either perpetual illumination or perpetual darkness, the following files are also included:

18. BifurcationDiagram_TimeSeries_[ModelName].m, which generates 4 plots: time series of LHY mRNA; time series of TOC1 mRNA; bifurcation diagram of fixed point and limit cycle; bifurcation diagram of oscillatory frequency which is only plotted for post-bifurcation region.  The bifurcation diagrams convert mu=1 to be the biological value given in original paper of bifurcation parameter.
19. PhaseDiagram_[ModelName].m, which generates 3 plots: phase diagram of LHY protein vs. LHY mRNA; phase diagram of TOC1 protein vs. TOC1 mRNA; phase diagram of TOC1 mRNA vs. LHY mRNA.  The phase diagrams reflect phase relationship at mu=1, the biological value given in original paper of bifurcation parameter.
20. atan_0to2pi.m, which calculates arctangent value of the input, and shifts the range to 0 to 2pi.

These can only be run after obtaining information of bifurcation for the model from above steps.  All plots include data points or curves from both RPM method and ODE solutions for comparison.
