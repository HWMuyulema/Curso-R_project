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



