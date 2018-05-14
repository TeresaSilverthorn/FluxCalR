# FluxCalR
This R package is used to calculate CO2 and CH4 gas fluxes measured with static chamber method. It provide a 
    easy way to calculate multiple flux measurements from one data file. 
    
Load the package in R by:
```R
devtools::install_github("junbinzhao/FluxCalR")
```
The format of data input are specialized to that of from Los Gatos Research (LGR) Ultraportable Gas Analyzers 
    <http://www.lgrinc.com/analyzers/ultraportable/>. Use the the function `Load_LGR()` to load raw data from LGR; 
    it automatic removes the extra rows at the beginning and the end, and convert timestamps into the format that is readable in R. 
    
A function (`Load_other()`) is also provided to load and convert data from other sources (e.g. LICOR) into the format that is 
    compatible with the flux calculation fuction. 
    
The function `FluxCal()` calculates CO2 and/or CH4 flux rates based on the time cues provided for each measurement (i.e. either 
    start or end time). Two options are available to input the time cues: 
    1. (default) after executing the function, manually clicking on a pop-up graph with CO2 concentration time series to choose 
    the END time, which could be identified by the "peaks" or "valleys"; or
    2. loading a file (.csv) into the argument "Time_keys" with times (HH:MM:SS) indicating start or end of each flux measurement. 
    The header for the time must be either "Start" or "End". 
    (see an example file "Time & Ta.csv" at https://github.com/junbinzhao/FluxCalR/tree/master/inst/extdata)
    
Based on the time cues and window width provided for the calculation, the function will automatically scan over data that cover
    1.5x length of the window width and calculate the fluxes based on the best linear regression (i.e. largest R2). After the
    calculations are done, a graph with regression lines plotted on the CO2 and/or CH4 concentration time series will pop up 
    for checkup purposes. 