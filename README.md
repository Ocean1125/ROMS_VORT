# A simple tutorial for running ROMS_VORT

## About ROMS_VORT

The ROMS_VORT is a package that calculates the vorticity budget equations by using the ROMS diagnostic u/v and averging outputs. There are **three** different forms of vorticity budget equations, the 2D depth-averaged vorticity equation (vort_2d), the 2D transport vorticity equation (vort_2dtrans), and the 3D depth-dependent vorticity equation (vort_3d). The detailed derivation of these forms can be found in Liu et al. (2020).  

Since the ROMS model takes terrain-following s-coordinate as its vertical coordinate, it's more difficult to calculate the horizontal differentiation of variables at the s-coordinate points than that using z-coordinate. In this package, we compute the terms of the vorticity equation by using the diagnostic output data of the 2D/3D momentum equations, which have been built in the ROMS model. 

The package computes each term of the 3 vorticity equations by using the diagnostic data (after you set the CPP "h file" and input "in file" options).

### 1. vort_2d (2D depth-averaged vorticity equation)

The 2D depth-averaged vorticity equation can be derived by taking curl on the 2D depth-averaged momentum equations and can be written as 

![](https://latex.codecogs.com/png.latex?\\underbrace{\frac{\partial\overline{\zeta}}{\partial{t}}}_{I}+\underbrace{\mathbf{U}\cdot\nabla(\frac{f}{D})}_{II}+\underbrace{\mathbf{U}\cdot\nabla(\frac{\overline{\zeta}}{D})}_{III}=\underbrace{J(\chi,D^{-1})}_{IV}+\underbrace{\nabla\times(\frac{\boldsymbol{\tau}_s}{D})}_{V}\underbrace{-\nabla\times(\frac{\boldsymbol{\tau}_b}{D})}_{VI})

Terms in the equation are (I) accelaration term (**acce_curl_2d**), (II) advection of background PV (**adv_bPV**), (III) advection of relative PV (**adv_rPV**), (IV) Joint effects of baroclinicity and relief (**JEBAR**), (V) curl of surface stress (**curl_Ts**) and (VI) curl of bottom stress (**curl_Tb**). 

### 2. vort_2dtrans (2D depth-integrated transport vorticity equation)

The 2D transport vorticity equation is the transport form of the depth-averaged vorticity equation and can be written as 

![](https://latex.codecogs.com/png.latex?\\underbrace{\frac{\partial{\overline{\zeta}}D}{\partial{t}}}_{I}+\underbrace{\nabla\times(D\mathbf{\overline{adv}})}_{II}=\underbrace{\nabla\times(\boldsymbol{\tau}_s-\boldsymbol{\tau}_b)}_{III}+\underbrace{\frac{1}{\rho_0}J(p_b,D)}_{IV})

Terms in the equation are (I) accelaration term (**acce_curl_2dtrans**), (II) curl of the transport advection term (**hadv_2dtrans**), (III) curl of the stress terms (**curlTs_2dtrans and curlTb_2dtrans**), (IV) bottom pressure torque term (**BPT**). The expression J stands for Jaccobian operator. 

### 3. vort_3d (3D depth-dependent vorticity equation)

The 3D depth-dependent vorticity is obtained by taking curl directly on the 3D momentum equations. It can be written as 

![](https://latex.codecogs.com/png.latex?\\underbrace{\frac{\partial{\zeta}}{\partial{t}}}_{I}+\underbrace{\nabla\times(\mathbf{adv})}_{II}\underbrace{-f\frac{\partial{w}}{\partial{z}}}_{III}=\underbrace{\nabla\times(\mathbf{visc})}_{IV})

Terms in the equation are (I) accelaration term (**acce_curl_3d**), (II) **nonlinear** term , (III) **divergence** term, and (IV) **viscous stress** term. 

## Tutorial of the ROMS_VORT package for a built-in test case in ROMS (canyon3d)

### 1. Idealized canyon case (3d)

The idealized canyon case is an idealized test of the interaction between topography and a near-steady current. This case is a suitable case to test the vorticity budget. 

(1) You should first run the idealized canyon (3d) with the following steps:

####  (1) Download and install ROMS 
step by step with the tutorial [ROMS_UNSW2008](https://www.myroms.org/wiki/ROMS_UNSW2008). After running the upwelling case by following the tutorial, the results will be saved as netcdf files.

You can also simply download the nc files we have obtained at [upwelling results](https://figshare.com/account/projects/81329/articles/12375272).

(2) Download the ROMS_VORT package at [github](https://github.com/rayliuxh/pv_balance.git) by run the script 
`git clone https://github.com/rayliuxh/pv_balance.git pv_balance` 
or download directly.

(3) There are 2 Matlab scripts in the ROMS_VORT folder. Run `get_circu_pattern_pub.m` to load the ocean state variables and make some plots. Run `get_pv_conservation_pub.m` to calculate the **three** different forms of the vorticity equations and do some plots. The detailed information of the variables in the script can be found in the above description.  



(1) 

### 1. Upwelling case

The Upwelling case is the default test case in ROMS. If you are not familiar with the compiling and running procedures of ROMS model, you can start from this case and then apply the ROMS_VORT package. Follow the following steps:

(1) Download and install ROMS step by step with the tutorial [ROMS_UNSW2008](https://www.myroms.org/wiki/ROMS_UNSW2008). After running the upwelling case by following the tutorial, the results will be saved as netcdf files. You can also simply download the nc files we have obtained at [upwelling results](https://figshare.com/account/projects/81329/articles/12375272).

(2) Download the ROMS_VORT package at [github](https://github.com/rayliuxh/pv_balance.git) by run the script 
`git clone https://github.com/rayliuxh/pv_balance.git pv_balance` 
or download directly.

(3) There are 2 Matlab scripts in the ROMS_VORT folder. Run `get_circu_pattern_pub.m` to load the ocean state variables and make some plots. Run `get_pv_conservation_pub.m` to calculate the **three** different forms of the vorticity equations and do some plots. The detailed information of the variables in the script can be found in the above description.  

### 2. Idealized canyon case (3d)

The idealized canyon case is more appropriate to test the vorticity budget when a current flowing over a topography. Run the idealized canyon (3d) case and then apply the ROMS_VORT tool. 

(1) 

## References:

Liu, X., D.-P. Wang, J. Su, D. Chen, T., Lian, C., Dong, and T. Liu, 2020. On the Vorticity Balance over Steep Slopes: Kuroshio Intrusions Northeast of Taiwan, Journal of Physical Oceanography, 50, 2089–2104, https://doi.org/10.1175/JPO-D-19-0272.1.
