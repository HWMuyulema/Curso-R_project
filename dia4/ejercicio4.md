library(maptools)      
library(raster)   

 ## Download data from gadm.org   
 
adm <- getData('GADM', country='EC', level=2)

guy<-(adm[adm$NAME_1=='Guayas',])   
plot(guy, bg='greenyellow', axes=T)# http://mrmrs.io/css-skins/, para buscar el color de fondo que que de mejor   
##Plot downloaded data   
plot(guy, lwd=10, border='skyblue', add=T)  
plot(guy,col='green4', add=T)   
grid()  
box()  
invisible(text(getSpPPolygonsLabptSlots(guy), labels=as.character(guy$NAME_2), cex=0.5, col='white', font=1))  
mtext(side=3, line=1, 'Mapa Cantonal de Guayas', cex=1)  
mtext(side=1, 'Longitud',line=2.5, cex=1.1)   
mtext(side=2, 'Latitud',line=2.5, cex=1.1)  
text(-79,-2.8, 'Projection: Geographic\nCoordinate System: WGS 1984\nData Source: GADM.org\nCreated by: CGSIN', adj=c(0,0), cex=0.5, col='grey20')

