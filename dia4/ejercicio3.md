library(raster)  
library(sp)  
library(ggplot2)   
library(rgdal)   
library(maptools)  
library(xts)  
library(dygraphs)  

setwd("I:/ARROZ/RESULTADOS/GUAYAS/DAULE/SHP")  
list.files()  
areall<-readOGR('.','AREA_LAS_LOJAS1')  
areall <- spTransform(areall, CRS('+proj=utm +zone=17 +north +datum=WGS84 +units=m +no_defs +ellps=WGS84 +towgs84=0,0,0'))  
spplot(areall)



## cortamos las imagenes  
setwd("I:/ARROZ/MOSAICOS_MODIS/MSC_NDVI_2015")  
files<-list.files(pattern='.tif$')  
files  
ndvi <- raster(files[18])*0.0001  
spplot(ndvi)  
ndvi<-crop(ndvi,areall)  
spplot(ndvi, col.regions=colorRampPalette(c("black", "green"))(255))   
setwd('I:/ARROZ/RESULTADOS/GUAYAS/DAULE/NDVI POR SECTORES MINIMOS/LAS LONJAS NDVI')  
writeRaster(ndvi, filename='353', format='GTiff')  



## stack cortes  
getwd()  
todos<- list.files(pattern = '.tif$')  
todos  
sndvill<- stack(todos)  
xndvill<- cellStats(sndvill, mean)  
xndvill<- as.data.frame(xndvill)  
xndvill  

## cuerpo del script  

names(xndvill)  
names(xndvill)<- 'mediaNDVI'  
xndvill$lugar<-'las lonjas'  
xndvill$anio<-'2015'  

dj<- gsub(pattern = 'X', x= row.names(xndvill), replacement = '')  
dj  
xndvill$dj<-dj  
class(xndvill$dj)   
xndvill$dj<- as.integer(xndvill$dj)  
class(xndvill)  
origin<- as.Date('2015-01-01')  
xndvill$Fechas<- origin + (xndvill$dj-1)  


## gráficos en ggplot  

ggplot(xndvill, aes(dj,mediaNDVI), na.rm=T) + geom_point(size=4) + geom_line()  

## hacemos el dygraph  
xts.ll<- as.xts(xndvill$mediaNDVI,order.by = as.Date(xndvill$Fechas,'%Y/%m/%d'))  
dygraph(xts.ll,'Serie Temporal de Arroz 2015 \n Las Lonjas')%>% dyRangeSelector()  
