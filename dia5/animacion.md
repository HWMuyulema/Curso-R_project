library(animation)


setwd("G:/ARROZ/RESULTADOS/GUAYAS/DAULE/animar/Nueva carpeta")  

## reading my png files    
bm.files = sprintf("daule%i.png", 1:18)  
head(bm.files)  
#
#ani.options(convert = 'C:\\Program Files\\ImageMagick-6.9.3-Q16\\convert.exe')  
ani.options(convert = 'C:\\Program Files\\ImageMagick-7.0.8-Q16\\magick.exe')  

# try to convert to gif  
im.convert(files = bm.files, output = "bm-Teo2.gif")  
