library(sp)  
library (raster)  
library(rgdal)  
library(landsat)  

alt <- getData('alt', country='EC')  
slope <- terrain(alt, opt='slope')  
aspect <- terrain(alt, opt='aspect')  
hill <- hillShade(slope, aspect, 40, 270)  
plot(hill, col=grey(0:100/100), legend=FALSE, main='Ecuador')  
plot(alt, col=rainbow(25, alpha=0.35), add=TRUE)  
