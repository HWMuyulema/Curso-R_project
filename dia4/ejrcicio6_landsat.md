require(raster)  
require(rgdal)  
require(randomForest)  
require(RColorBrewer)  

setwd("G:/R_ecohidrologia/clasificacion-imagenes/img")

dir()  
files<-list.files(pattern = '.tif')  
files  
imageraster<-raster(files[1])  
spplot(imageraster)  
names(imageraster)  
rbrick<-imageraster  



for(i in 2:length(files)){  
  imageraster<-raster(files[i])  
  rbrick<-addLayer(rbrick,imageraster)  
}  



rbrick  
names(rbrick)  
summary(rbrick)  
rbrick <- projectRaster(rbrick,crs="+init=epsg:32717")  
rbrick  


#remplazar los valores por NA  
rbrick[rbrick[]==0]<-NA  
projection(rbrick)  
spplot(rbrick)  

## guardar archivo multibanda

writeRaster(rbrick,filename = 'rbrick.tif',format='GTiff',overwrite=T)  

## combinacion de archivo multibanda

### color natural

plotRGB(rbrick,r=3,g=2,b=1, axes=TRUE,colNA='white', stretch='lin')

### falso color vegetacion  

plotRGB(rbrick, r=4, g=3, b=2,axes=TRUE, colNA='white',stretch='hist')

### Falso color urbano

plotRGB(rbrick,r=6,g=5,b=3,axes=TRUE, colNA='white', stretch='hist')

### Agricultura

plotRGB(rbrick, r=5,g=4,b=1,axes=TRUE, colNA='white',stretch='hist')


### NDVI

ndvi<-(rbrick[[4]] - rbrick[[3]])/(rbrick[[4]] + rbrick[[3]])

summary(ndvi)


cuts<-seq(minValue(ndvi), maxValue(ndvi),length.out = 8)  
cuts<-round(cuts,digits = 2)  
col.regions<-brewer.pal(length(cuts)+2,'RdYlGn')  
spplot(as(ndvi, 'SpatialGridDataFrame'),at=cuts,col.regions=col.regions,colorkey=list(labels=list(at=cuts),at=cuts),       pretty=TRUE,scales=list(draw=T))  

## NDVI por partes

ndvi<- function(nir,red, filename) {  
  out <- raster(nir)  
  out <- writeStart(out, filename, overwrite=TRUE)  
  bs <- blockSize(nir)  
  for (i in 1:bs$n) {   
    vnir <- getValues(nir, row=bs$row[i], nrows=bs$nrows[i] )  
    vred <- getValues(red, row=bs$row[i], nrows=bs$nrows[i] )  
    ndvi <- (vnir - vred)/(vnir + vred)  
    out <- writeValues(out, ndvi, bs$row[i])  
  }  
  out <- writeStop(out)  
  return(out)  
}  
ndvi(rbrick[[4]],rbrick[[3]], "ndvi.tif")  

ndvi2<- raster("ndvi.tif")   

cuts <-seq(minValue(ndvi2),maxValue(ndvi2),length.out=8)  
cuts = round(cuts,digits=2)  
col.regions = brewer.pal(length(cuts)+2, "RdYlGn")  
spplot(as(ndvi2, 'SpatialGridDataFrame'),at=cuts,col.regions=col.regions,colorkey=list(labels=list(at=cuts),at=cuts),      pretty=TRUE,scales=list(draw=T))

# Bibliografía
http://sigyury.blogspot.com/p/manual-basico-de-arcgis-10.html
