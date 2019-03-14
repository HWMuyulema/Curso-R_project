# [Básicas](http://www.davidam.com/software/R/primitivasR.html)
## Atajos
Alt + Shift + k
  * Ctrol + Shift + 1
  * Ctrol + Shift + 2
  * Ctrol + Shift + 3
  * Ctrol + Shift + 4

## Configuración del entorno

* getwd ()
* setwd ('  ')
* list.files()
* q()

## Ayuda on line en R

* help()

* ?mean

* help.search()

* ?? 'standard desviation'

* help.start()              # abre una ventana en el navegador

* example()                 # ejemplos del uso de mean


## Operaciones Aritmétics



5+7                          # se evalua y el resultado se imprime

			     # por pantalla pero no se guarda 	
			     
5**7 	

5-7 

5/7 

5^7  	                     # elevado a

51 %% 7                      # modulo (resto de una division entera)

51 %/% 7                     # division entera	

## Asigncaión de valores a variables	

x <- 1                             # asigna el valor 1 a la variable x  

x                                  # lo escribe por pantalla	

y <- x^2   	

x = 1                              # una alternativa

1 -> x                             # otra alternativa	


## Funciones



q                            # Muestra informacion de la funcion	

?q
                             # Algunas funciones elementales: log(), log10(),
			     
                             # exp(), sqrt(), sin(), cos(), tan()	
			     
                             # Mas funciones basicas: c(), max(), min(),
			     
                             # pmax(), pmin(), range(), length(), sort()
			     
                             # sum(), rowSums(), prod(), mean(), colMeans(),
			     
			     
                             # var(), cumsum(), etc.	
c(2,69,5,47,3647)

sum(1,3,5,7)

raiz64 <- sqrt(64)           # el resultado de una funcion	

			     # puede guardarse en una variable	
			     
print(x)

print(pi,digits=16); print(pi,digits=5)	


## Listar y eliminar objetos del espacio de trabajo



ls() # para ver las variables que estan en el espacio de trabajo

rm(x,raiz64) 	

ls() 

rm(list=ls()) 

ls() 	

# Tipos de Datos

## Booleanos

verdad <- T

mentira <- F

edad <- c(27,30,29);

is.numeric(edad)

is.integer(edad)

is.double(edad) # tambien existen is.complex(),

				# is.logical(), is.character()...
				
typeof(edad)    # devuelve el tipo del objeto

				# introducido como argumento
				
				
## Arrays
calle <- c('Av/ Amazonas','Av. Eloy Alfaro')

## Conversión de tipo

as.character(verdad)

as.numeric(verdad)      # doble precision por defecto

y <- c(0,1,27,14.9,NA,-3.2);y   # ojo, trunca en vez de redondear

as.logical(y)

as.character(y)

as.integer(y)

y<-c("hola", "adios","true","TRUE", "T", "F","129",NA ,"6");y

as.logical(y)

as.numeric(y)

# Vectores

## Básico

x <- c(1,4,6,3,7); x

x[3]            # devuelve el valor guardado en 3a posicion

x[-4]           # devuelve todo excepto el valor

						# guardado en 4a posicion
						
x[1] <- 35      # guarda el valor 35 en la primer posicion

length(x)       # devuelve la longitud de x

x[11] <- 99; x

## Cálculo vectorizado, Equivale a un bucle implícito


x <- c(1,2,3,4,5)

y <- c(5,4,3,2,1)

x+y

y <- c(1,2,3);y

suma <- x+y; suma       # recicla el vector mas corto

suma2 <- x-1            # con escalares parece mas natural

x <- c(0.0001, 0.001, 0.01, 0.1, 1)

log10(x)            # muchas funciones tambien se aplica vectorizadamente

## Generación de secuencias regulares


1:10


1:10-1              # el operador ':' tiene maxima prioridad
1:{10-1}

#funcion seq(from, to, by, length)

x <- seq (-3,3,0.5);x       # valores desde -3 hasta 3 a intervalos de 0.5

seq (-3,3,length=10)        # 10 valores equiespaciados desde -3 hasta 3

seq (-3, by=0.5,length=10)  # 10 valores a intervalos de 0.5 desde -3

seq(along=x)            # Genera la secuencia 1, 2, 3,..., length(x)

#funcion rep(x, times, each)

x <- 1:4

rep(x,times=3)          # repite el contenido de x tres veces

rep(x,each=3)               # repite cada elemento de x tres veces

rep(x,times=2,each=3)

rep(c(0,1),times=c(4,3))    # 'times' puede ser un vector. Aqui ya no cabe 'each'

x <- seq(19,6,-3);x

rep(x,1:length(x))      # 'times' puede estar implicito times={1:length(x)}

## Ordenación de vectores



x <- c(20,80,30,50,0)

order (x, decreasing=F)     # devuelve las posiciones del vector ordenadas segun su contenido

sort (x, decreasing=F)      # devuelve el contenido del vector ordenado

rank(x)             # devuelve el orden de cada posicion segun su contenido

min(x)

which.min(x)            # equivale a which(x == min(x))

x <- c(1,1,3:1,1:4,3); y <- c(0,9:1)

x.ord <- order(x,y)     # ordena los valores de x y, en caso de empate, utiliza los valores de y en las posiciones correspondientes. Ambos, x e y deben tener la misma longitud

x.ord;x;y

## Ordenadores comparativos <,<=,>,>=,=,!

x <- c(1:10); x  
valor.verdad <- x>5; valor.verdad  
x <- 1:10  
x[x >= 5] <- 20; x  # condicional implicito  
x[x == 1] <- 25; x  
x <- 1:3; y <- 1:3  
x == y          # equivalente a identical(x, y) o all.equal(x, y, tol=0)  
y <- y+0.001; y  
identical(x, y)  
all.equal(x, y, tol=0.001)  
