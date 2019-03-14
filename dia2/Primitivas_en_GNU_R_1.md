# Factores

Son vectores para datos categóricos, Permiten prescindir de la codificaión numérica y referirse a los niveles mediante nombres


estudios <- c(1,3,1,1,3,4,3)  
factor(estudios)  
nivel.estudios <- factor(estudios, levels=1:4,labels=c("primarios", "secundarios", "superiores", "doctorado"), ordered=T)  
nivel.estudios  
factor(c(5,2,2,4,5,4,3,3,1), 2:5, exclude=4) # los valores 1 y 4 se consideran valores perdidos  
#OJO. Internamente R siempre se asigna 1 al primer nivel del factor, 2 al segundo etc.  
levels(nivel.estudios)           # levels() extrae los posibles niveles de un factor  
as.numeric(nivel.estudios)       # recodifica el factor numericamente  
codigo.postal <- factor(c('28011', '28044', '28011','28013', '28013','28023'))  
equipo.futbol <- factor(c('VAL', 'VAL', 'FCB','VAL', 'FCB','ATM'))  
equipo.futbol                        # ordena los factores alfabeticamente  
as.numeric(equipo.futbol)

## Matrices
Suponen la generalización de vectores en 2D. Todos los vectores de uina matriz deben ser del mismo tipo. Una convención relativamente extendida es comenzar con mayuscula el nombe de una matriz

X <- 1:12  
dim(X) <- c(4,3); X # los elementos se organizan por columnas  
matrix(1:12,nrow=3,ncol=4,byrow=T)  
matrix(1:12,nrow=4,byrow=T)  
Mi.matriz <- matrix(1:12,3,4,F); Mi.matriz  
tamano <- dim(Mi.matriz)     # otro uso de dim(); devuelve las dimensiones de la matriz  
rownames(Mi.matriz) <- LETTERS[1:tamano[1]]; Mi.matriz  
colnames(Mi.matriz) <- paste("Var",1:tamano[2], sep=""); Mi.matriz  
dimnames(Mi.matriz)  

## Concatenación de matrices

X1 <- c(3,7,5)  
X2 <- c(8,3,1)  
Xx <- cbind(X1,X2);Xx  
Yy <- rbind(X2,X1);Yy  
Zz <- cbind(X1,Xx);Zz  

## Indexación de matrices

X <- matrix(c(1,4,12,15),2,2);X  
X[1,2]               # elemento guardado en la 1a fila, 2da columna  
X[1, ]               # todos los elementos de la primera fila  
X[ ,2]               # todos los elementos de la segunda columna  
X[3]                 # para pensar un poco...  
Mi.matriz['B',]  #tambien se pueden usar los nombres (se han asignado)  

## Operaciones con matrices

X <- matrix(c(1,4,12,15),2,2); X  
Y <- matrix(1:4,2,2); Y  
X+Y  
X-Y  
X%*%Y                        # producto matricial  
X*Y                      # producto elemento por elemento  
t(X)                     # traspuesta  
det(X)                   # determinante  
X.inv <- solve (X)   # inversa de X (siempre que X sea cuadrada no singular, claro)  
X.inv  
X%*%X.inv                # Comprueba el resultado. Ojo a los errores de redondeo  
#En general, solve(a,b) es una funcion que resuelve a %*% x = b para x, donde b puede ser un vector o una matriz. Si no se explicta se asume que es la matriz identidad y la funcion devuelve la inversa de a  
A <- matrix(c(1,4,12,15),2,2); A  
B <- matrix(c(5,2),2,1);B  
X <- solve(A,B); X  
A%*%X            # comprueba que el resultado es efectivamente B 

## Algunaas funciones que ooperan sobre filas  o columnas completas

X <- matrix(c(1,4,12,15),2,2); X  
rowSums(X)  
colSums(X)  
rowMeans(X)  
colMeans(X)  

## Apply

apply(X,1,sum)       # suma por filas; equivale a rowSums(X)  
apply(X,2,mean)  # media por columnas; equivale a colMeans(X)  
apply(X,1,sd)  

## Matrices multidimencionales

A <- array(1:24, c(3, 4, 2)); A
dimnames(A) <- list(c("fila1", "fila2", "fila3"), c("col1", "col2", "col3", "col4"), c("capa 1", "capa 2"));A

## Listas

Son una especie de contenedores generales donde puede mezclarce todo tipo de componentes (objetos de cualquier tipo y cualquier longitud)

Son unos objetos poco estructurados y, por tanto, muy flexibles

Muchas funciones nativas de R devuelven el resultado en forma de lista

rm(list=ls())  
mis.num <- seq(1.0, 2.0, 0.1); mis.num2 <- 2:4  
Mi.matriz <- matrix(1:12,3,4); Mi.matriz  
mis.caracteres <- paste(LETTERS[1:5]);mis.caracteres  
mis.logicos <- mis.num > 1.65; mis.logicos  
lista1 <- list(mis.num, mis.num2, Mi.matriz, mis.caracteres,mis.logicos)  
lista1

## Indexación, nombres y atributos

length(lista1)       # devuelve el numero de componentes de la lista  
str(lista1)      # devuelve informacion sobre la estructura de la lista  
a <- lista1[[1]] # devuelve el 1er objeto de la lista en forma de vector/matriz (y nombre  excluido)  
a; typeof(a)  
b <- lista1[1]       # devuelve una sublista compuesta por los elementos de la 1a entrada de la lista (nombre incluido)  
b; typeof(b)  

nomb <- c("reales","enteros", "matriz", "caracteres", "logicos")  
names(lista1) <- nomb;   # asigna nombres a los componenes de la lista  
names(lista1)                # devuelve los nombres de los componentes (si los hay)  
lista1[["reales"]]  
lista1$logicos           # equivalente a lista1[["logicos"]] y a lista[[5]]   

#Otro modo de definir una lista que incluye nombres para los componentes 
lista2 <- list(A=mis.num, B=mis.num2); lista2  
names(lista2)

## Attach
Las funciones Attach(), y detach(),"cargan" listas y simplifican las referencias

attach(lista1, warn.conflicts = T)





