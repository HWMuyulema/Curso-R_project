library(gstat)
library(sp)
library(ggplot2)
library(rgeos)
library(DescTools)
library(mapview)

#opciones para ggplot para no tener que ponerlas en cada gráfico
theme_set(theme_bw())
theme_update(legend.position='ringth')

#datos---

setwd("D:/Cursos/R_project/dia5")
datos<- read.table("BroomsBarn.txt",header = T,sep = '\t')
datosorig<- datos # hace un respaldo de los datos originales

# exploración de datos
summary(datosorig)
Desc(datos$logK)
apply(datosorig,2,var)
head(datosorig)
quantile(dist(datosorig[,1:2])) # distancias
ggplot(datosorig,aes(logK))+
  geom_histogram(aes(y=..density..), bins= 10, col=1, fill=4,alpha=0.5)+
  geom_vline(xintercept = mean(datosorig$logK),col=2)+
               geom_density(col=4)+
               labs(y='Densidad')

# Preprocesamiento para el análisis espacial
dint<- signif(max(c(diff(range(datos$x))/length(datos$x),diff(range(datos$y))/length(datos$y))))
xint<- seq(min(datos$x),max(datos$x),dint)
yint<- seq(min(datos$y),max(datos$y),dint)
datosint<- expand.grid(x=xint,y=yint)
gridded(datosint)<-~x+y
coordinates(datos)<-~x+y
mapview(datos,burst= T, hide=T)
mapview(datos,zcol='logK',legend=T)

# polígono que contiene los datos
q=min(c(diff(range(datos$x)),diff(range(datos$y))))
outline <- gBuffer(datos,byid=FALSE,id=NULL,width = dint*q,joinStyle = 'ROUND',quadsegs = 10)
plot(outline)

# Variograma experimental omnidereccional
g<- gstat(id ='logK',formula=logK-1,data= datos)
dat.vgm= variogram(g)
head(dat.vgm)
plot(dat.vgm)
dat.vgm = variogram(g,cutoff = 15)
head(dat.vgm)
plot(dat.vgm)
plot(variogram(g,cutoff = 15,width = 3))
plot(variogram(g,cutoff = 15,width = 0.54))

#Mapa de la superficie del variograma
#width es el ancho del tamaño de la celda
#cutoff es la extención lateral
map.vgm<-variogram(g.width=1,cutoff = 15,map = TRUE)
plot(map.vgm)
ggplot(data.frame(map.vgm),aes(x=map.dx,y=map.dy,fill=map.logK))+
  geom_raster()+
  scale_fill_gradientn(colours = rainbow(7))+
  labs(x='Distancia E-W [m]',y='distancia N-S[m]',fill='semivarinza')

#Variogramas direccionales

dat.vgm3<- variogram(g,alpha = c(0,45,90,135),tol.hor = 22.5,cutoff = 15)
ggplot(dat.vgm3,aes(x=dist,y=gamma,col=factor(dir.hor),shape=factor(dir.hor)))+
  geom_point(size=2)+
  geom_hline(yintercept = var(datos$logK, col= 2,linetype=2))

#modelo Teórico
#valores iniciales para el variogramateórico
meseta=0.013
mod='sph'
rango=10
pep=0.005

## modelos
esferico<- function(x,c0,c1,a) {ifelse(x<=a,c0 + c1*(3/2*x/a-1/2*(x/a)^3),c0+c1)}
exponencial<- function(x,c0,c1,a){c0 + c1* (1 - exp(-3*x/a))}
gaussiano<- function(x,c0,c1,a){c0 + c1*(1-exp-3*x/a)^2)}

                                                                                                                                                  
