## Instalación de paquetes
library() # para saber cuantas librerias tenemos
install.packages('MODISTools')
remove.packages(MODISTools)
update.packages(MODISTools)
library(MODISTools)
require(MODISTools)

## Lectura de archivos de información geográfica y sistemas de referencia
* aprenderemos:
    * cargar shp tipo líneas, puntos, y poligonos
    * Cargar arachivos de tipo txt,y tipo csv
    * Cargar archivos raster
    * Explorar y transformar sistemas de referencia
    * Asignar coordenadas
    * Guardar archivosd txt y shp

require(sp)
require(rgdal)
require(raster)
require(rgeos)

#setwd()
#shell.exec("https://drive.google.com/uc?export=download&id=0B0ea6usixQHFTktDSC04MHNJY2M")

ogrDrivers()

setwd("D:/Cursos/R_project/dat/dia2")

ogrListLayers('.')

ogrInfo('.','prov_zona_estudio')

#cargar la capa

zona_estudio<- readOGR('.','prov_zona_estudio')

zona_estudio@data

view(zona_estudio@data)

zona_estudio1<-zona_estudio[zona_estudio$DPA_PROVIN !=15] #para quitar esta provincia

class(zona_estudio)

proj4string(zona_estudio)

utm17<-"+proj=utm +zone=17 +south +datum=WGS84 +units=m +no_defs +ellps=WGS84 +towgs84=0,0,0"

wgs84<- '+proj=longlat +ellps=WGS84'

proj4string(zona_estudio)<- CRS(utm17)

summary(zona_estudio)

zona_estudio@data

coordinates(zona_estudio)

names(zona_estudio)

plot(zona_estudio)

#Cargamos los shp de ptos

estaciones<-readOGR(".","estaciones_32717") #estaciones metereológicas

proj4string(estaciones)

class(estaciones)

names(estaciones)

summary(estaciones)

plot(estaciones)

estaciones2<- estaciones[,c(2,3,6,7,8,9)]#opción 1: número de columna

estaciones2<- estaciones[,c("CODIGO","NOMBRE.DE","Lat","Long", "x","y")]#opción 1: nombre de columna

names(estaciones2)<- c("estacion","nombre", "lat", "long", "x", "y") #asignar nuevos nombres a las columnas

l1 = list("sp.points", estaciones2, pch = 19)

spplot(zona_estudio, "DPA_PROVIN", sp.layout = list(l1))

## Cargamos el archivo de txt

observaciones<- read.table('observaciones_2003.csv')

class(observaciones)

str(observaciones)

table(complete.cases(observaciones$VALOR))

observaciones2 <- observaciones[complete.cases(observaciones$VALOR),]#excluir valores vacios

table(complete.cases(observaciones2$VALOR))

write.table(observaciones2, "observaciones_no_missing.txt")

## Asignamos coordenadas a las observacioens

observ_ref <- merge(observaciones2, estaciones2,by.x = "ESTACION", by.y = "estacion")

class(observ_ref)

names(observ_ref)

coordinates(observ_ref)<- ~x+y

class(observ_ref)

proj4string(observ_ref)

proj4string(observ_ref)<- CRS(utm17)

l1 = list("sp.points", observ_ref, pch = 19, col="green")


spplot(zona_estudio, "DPA_PROVIN", col="grey", sp.layout = list(l1))

writeOGR(observ_ref, dsn = ".", layer = "observaciones_georef", driver = "ESRI Shapefile",overwrite_layer = TRUE)

## Cargamos las líneas

rios<-readOGR(".","rio_torrente")#fuente IGM 50k

proj4string(rios)

rios <- spTransform(rios,CRS(utm17))#transformación

class(rios)

names(rios)

rios$nombre

l1 = list("sp.lines", rios,  col="blue")

spplot(zona_estudio, "DPA_PROVIN", col="grey", sp.layout = list(l1))
