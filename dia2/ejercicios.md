a = 1:10  
b = rep(6,times=10)  
m<- cbind(a,b) # bind=enlazar  
m  
m<- cbind(a,b,x=a*b)    
m    

## Matrices

h<- matrix(1:25,ncol = 5);h 

h[3,4];h  

h[,4];h 

h[2,];h 

## Datos no disponibles, missing data


#Generamos una distribución normal  

x=rnorm(100);x  
z=rep(NA,100);z 

#seleccionaremos aleatoriamente 50 elementos de esos 200 valores (combimando ‘y’ y ‘z’), de modo que no sabremos cuantos NA hay en el  #vector resultante, ni donde estan localizados 


## sample presenta muestras aleatorias y permutaciones  

mi_dato<-sample(c(x,z),50)  
mi_dato 

## ubicamos los NA (marcadores de posición) 
mi_na= is.na(mi_dato) 
mi_na 

## Necesitamos determinar cuantos NA existen  
sum(mi_na)  

table(mi_na)  

#No es lo mismo NA que NaN (infinito 0/0) 
#muestrame los 10 primeros valores  
mi_dato[1:10] 

#dim de cuales son los datos diferentes de NA 
y=mi_dato[!is.na(mi_dato)]:y  

mi_dato 

#busque los vectores ubicados en diferentes posiciones  
mi_dato[c(7,10,15,50)]  
y[c(3,7,9)] 

## creamos un vector con nombres  



vect<- c(a=11,b=NA,c=2);vect  

names(vect) 

vect['a'] 

vect[c('a','c')]  

# Matrices y data frames  



mi_vect<- 1:24  
mi_vect 

#dim informa sobre las dimensiones de un objeto



dim(mi_vect)  
length(mi_vect) 

## agregamos filas y columnas 

dim(mi_vect)<- c(6,4) 
dim(mi_vect)  

attributes(mi_vect) 

mi_vect 

class(mi_vect)  

## creamos una matriz directa  
mi_matriz2 <- matrix(1:20, nrow=4, ncol=5)  
mi_matriz2  

estudiantes<- c('juan','anita','oscar','sylvia')  
estudiantes 

cbind(estudiantes,mi_matriz2) 

## creamos data frames


Los data frames son una estructura de datos que generaliza a las matrices


df<- data.frame(estudiantes,mi_matriz2);df  
class(df) 

#vamos a ponerle nombres   
cnames<- c('mate','geol','hist','leng','teled','edu');cnames  
colnames(df)  

colnames(df)<-cnames;colnames 
colnames(df)  
df  

# Listas
Podemos entender una lista como un contenedor de objetos que pueden ser de cualquier clase: números, vectores, matrices, funciones, data.frames, incluso otras listas.

Por ejemplo, podemos crear una lista que contenga el data.frame misDatos, la matriz A, la matrizM, el vector x=c(1,2,3,4) y la constante e=exp(1):

A=matrix(1:9,nrow=3)  
M=matrix(1,4,nrow=2)  
MiLista <- list(misDatos,A,M=M,x=c(1,2,3,4),e=exp(1))  
MiLista  

## set.seed

Para crear simulaciones u objetos aleatorios que se pueden reproducir para asegurar que los datos sean reproducibles.

Si se quiere ejecutar la función anterior, pero partiendo de una semilla concreta (para
garantizar el mismo resultado en cualquier ejecución), se usará la función set.seed()
antes de la anterior
> runif(5) # genera valores de una distribución uniforme 

> runif(5)

> set.seed(32789)  
> runif(5)



> set.seed(32789)  
> runif(5)

## Explorar datos 
#Utilizaremos una dase de datos conocidos 

data("cars")  
class(cars) 
dim(cars) 
nrow(cars)  
ncol(cars)  

## Si queremos conocer el espacio que utiliza en la memoria el archivo  
object.size(cars) 
names(cars) 
cars  
head(cars)  
tail(cars)  

summary(cars) 
## para conocer la estructura de los datos  
str(cars) 

cars[48,2]  
cars[1,]  
cars[,1]    
cars[,2]  
cars[1:20,] 
cars[cars$speed >20,] 
cars[cars$speed == 20,] 

## Si queremos hacer un subconjunto



nuevo_dato<- cars[cars$speed == 20,]  
nuevo_dato  

nuevo_dato<- subset(cars,speed>=20,'speed') 
nuevo_dato  



# Gráficos base 
plot(cars)    
plot(x=cars$speed,y=cars$dist)  
plot(x = cars$speed, y = cars$dist, xlab = "Velocidad", ylab = "Distancia de parada") 
plot(cars,main='Mi gráfico')  
plot(cars,sub='aquí va el subtitulo') 
plot(cars,col=4)  



## vamos a limitar el eje de las x


plot(cars, xlim = c(10, 15))  
#probamos valores del 1 al 25 
plot(cars,pch=25) 

## vamos a plotear con bigotes


data("mtcars")  
dim(mtcars) 
boxplot(mtcars) 


#(~) nos da la relación entre las varables de entrada 
#Esto le permite introducir algo como mpg ~ cil para trazar la relacion entre cilindros (numero de cilindros) en el eje X y mpg (millas por galon) en el eje y. Use boxplot() con formula = mpg ~ cyl y data = mtcars para crear un boxplot.  

  
boxplot(formula = mpg ~ cyl, data = mtcars) 

## Si tenemos una sola variable


hist(mtcars$mpg)  

# Instalación de paquetes
