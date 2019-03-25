require(foreign)  
require(leaflet)  
require(rgdal)  
require(sp)  



setwd("G:/ARROZ/MOSAICOS_MODIS/MSC_NDVI_2015/resultados_tif")

modis<- list.files()  
modis<-readOGR('.','l1p')  

modis<- spTransform(modis, CRS('+proj=longlat +ellps=WGS84 +datum=WGS84 +no_defs'))  
coordinates(modis)  

df<-data.frame(coordinates(modis))  
fix(df) # cambiamos los nombres de x y y x por lat y y por lng  
View(df)  
df$tile<-c(1:32)  
coor_popup<- paste0 paréntesis '<strong>Tile:</strong>',  
                    '<br><strong><a>Arroz 2015:</a></strong>',  
                    '<br><a>Lat=</a>',df$lat, '<br><a>Lng=</a>',df$lng cerrar paréntesis
                    
## realizamos el scrip para el mapa


leaflet(data = df)%>%addTiles()%>%addMarkers(~lng,~lat, popup=coor_popup)
