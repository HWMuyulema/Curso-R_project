library(raster) 
library(sp) 
library(rgdal)  
library(maptools) 

setwd("I:/MAGAP/INUNDACIONES 2015_2016/SHP")  
list.files()  
arroz<-readOGR('.','EL_ORO2') 
arroz <- spTransform(arroz, CRS('+proj=utm +zone=17 +north +datum=WGS84 +units=m +no_defs +ellps=WGS84 +towgs84=0,0,0'))  
spplot(arroz,'DPA_DESPRO')  



## crear el raster
setwd("I:/ARROZ/MOSAICOS_MODIS/MSC_NDVI_2015")  
files<-list.files(pattern='.tif$')  
files 
ndvi <- raster(files[12])*0.0001  
spplot(ndvi)  

## cortamos la capa

ndvi<-crop(ndvi,arroz)  
spplot(ndvi, col.regions=colorRampPalette(c("blue", "green"))(255)) + as.layer(spplot(arroz[1], fill="transparent", col="black", under = FALSE))  



# mascara 
ndvi<-mask(ndvi, arroz) 
spplot(ndvi, col.regions=colorRampPalette(c("blue", "green"))(255)) + as.layer(spplot(arroz[1], fill="transparent", col="black", under = FALSE))  
rc<-reclassify(ndvi, c(0, 0.25, 1, 0.25, 0.5, 2, 0.5, 1, 3))  


par(mfcol=c(2,1)) 
plot(ndvi,main="original")  
plot(rc,main="reclassed image") 
par(mfcol=c(1,1)) # presentar el gráfico  
pol.ndvi<-rasterToPolygons(ndvi)  

plot(pol.ndvi)  

writeSpatialShape(pol.ndvi,'pol.ndvi.shp')  

ecuador<-CRS('+proj=longlat +ellps=WGS84 +datum=WGS84 +no_defs')  

# reproyeccion  
pol.ndvi<-spTransform(pol.ndvi,ecuador) 

#escribimos el kml y guardamos el archivo 
writeOGR(pol.ndvi,'pol.ndvi.kml','pol.ndvi',driver='KML') 

kml_View('pol.ndvi.kml')  
