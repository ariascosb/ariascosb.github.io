---
title: "Mis apuntes de R"
date: 2023-10-07T11:07:37-05:00
draft: true
tags: ["R","ciencia de datos","Data science"]
categories: ["R", "programacion"]
showtoc: false #si quiero mostrar la tabla de contenido cambiar a true
---

# R

# Introducción

- En R todos las variables son objetos.
- Configuracion inicial Rstudio: Eliminar rstore and rdata.

![name](images/descarga.jpg)

- Las asignaciones en R se hacen con <-
- Los comentarios se hacen con #

```r
x<-2 #Esto es un comentario

Ctrl+Shift+C #comentarios de mas de una linea

cr3499301
```

- La ayuda se pide con:

```r
?mean()
help("mean")
```

- Directorio de trabajo actual: getwd()
- Cambiar directorio: setwd("C:\otro_directorio")

```
# Ver archivos
list.files()

# Ver directorios
list.dirs()
```

- Revisar archivos guardados en memoria ls()
- Instalar paquetes y librerías

```r
install.packages("readr") #Instalacion (Solo se hace una vez)
library(readr) # Cargue de la libreria (Siempre que se vaya a usar)
update.packages() #Actualizar paquetes R
#3.6.1 
```

- Factores: Agrupación especial de datos. Ejemplo: podemos tener dos tipos de valores en la variable sexo: 1 y 2. A las cuales le podemos asignar unas etiquetas o niveles. Hombres (1) y Mujeres (2). Esto es muy útil para el tratamiento de datos. OJO: los factores siempre quedan guardados como numeros con etiquetas en texto
- En R, usamos NA para representar datos perdidos, mientras que NULL representa la ausencia de datos. La diferencia entre las dos es que un dato NULL aparece sólo cuando R intenta recuperar un dato y no encuentra nada, mientras que NA es usado para representar explícitamente datos perdidos, omitidos o que por alguna razón son faltantes. NA además puede aparecer como resultado de una operación realizada, pero no tuvo éxito en su ejecución.
- A diferencia de la mayoría de los lenguajes de programación, los índices en R empiezan en 1, no en 0.
- Funciones basicas

```r
#Limpiar datos
rm(list=ls())

#Promedio
mean()
#Desviacion estandar
sd()
#Coeficiente de correlacion
cor()
#Resumen estadistico
summary()
#Mirar los primeros 10 datos
head()
#Leer datos CSV paquete base
bcancer <- read.csv("breast-cancer-wis.csv")
bcancer <- read.table(file = "breast-cancer-wis.csv", header = TRUE, sep = ",",
                      col.names = nombres)
#Exportar datos paquete base
write.csv(x = iris, file = "iris.csv", row.names = FALSE)

#OJO NOTA: Se recomiendas usar data table para leer y escribir dado que es mas 
#rapido que el paquete base

#Uso formato .Rds
saveRDS(object = mi_lista, file = "mi_lista.rds")
mi_lista_importado <- readRDS(file = "mi_lista.rds")

#Usar un script R desde otro archivo
source("MyScript.R")
```

Directorios de trabajo

```r
getwd() #Directorio actual de trabajo
setwd("C:\otro_directorio") #Cambiar el directorio
```

Organizar codigo. Rstudio automaticamente organiza nuestro codigo para que sea mas legible

```r
Contorl +I 
Control+shift (Mayus) +A
```

Verificar si las librerias estan y instalarlas

```r
#Verificar librerias
list.of.packages <- c("shiny","shinydashboard","ggplot2","data.table","lubridate")
new.packages <- list.of.packages[!(list.of.packages %in% installed.packages()[,"Package"])]
if(length(new.packages)) install.packages(new.packages)
```

Acomodar ceros a la derecha y a la izquierda

```r
Simula la funcion right de excel
right = function(text, num_char) {
  substr(text, nchar(text) - (num_char-1), nchar(text))
}

cron[,cantidad.requerida.mix:=round((sum.mix/fc.m.kg)*1000,4),]
#Numeros a la derecha
cron[,cantidad.requerida.mix:=sprintf("%f",cantidad.requerida.mix),]
#Numeros a la izquierda
cron[,cantidad.requerida.mix:=paste0("000000000",cantidad.requerida.mix)]
cron[,cantidad.requerida.mix:=right(cantidad.requerida.mix,16)]
```

# Tipos de datos

- Conversión (Coercion). Cuando estas funciones tienen éxito en la coerción, nos devuelven datos del tipo pedido. Si fallan, obtenemos NA como resultado.

```r
as.integer()	#Conversion a Entero
as.numeric()	#Conversion a decimal
as.character()	#Conversion a Cadena de texto
as.factor()	#Conversion a Factor 
as.logical()	#Conversion a Lógico
as.null()	#Conversion a NULL

#La conversion se da en el siguiente sentido y nunca en el sentido contrario
lógico -> entero -> numérico -> cadena de texto 
(logical -> integer -> numeric -> character)
```

- Verficar el tipo de dato

```r
str(a) #Me indica que tipo de dato es
class(a) #Me indica que tipo de dato es

is.integer()	#Verificar si es Entero
is.numeric()	#Verificar si es decimal
is.character()	#Verificar si es Cadena de texto
is.factor()	#Verificar si es Factor 
is.logical()	#Verificar si es Lógico
is.null()	#Verificar si es NULL
```

# Operadores

## Matematicos

![R%20648c68dafc5e49449c455147c1f1fa0d/Untitled%201.png](R%20648c68dafc5e49449c455147c1f1fa0d/Untitled%201.png)

## Relacionales

![R%20648c68dafc5e49449c455147c1f1fa0d/Untitled%202.png](R%20648c68dafc5e49449c455147c1f1fa0d/Untitled%202.png)

Si se comparan dos cadenas de texto con < o > se usa como criterio el orden alfabético

## Lógicos

![R%20648c68dafc5e49449c455147c1f1fa0d/Untitled%203.png](R%20648c68dafc5e49449c455147c1f1fa0d/Untitled%203.png)

## Orden de operaciones

![R%20648c68dafc5e49449c455147c1f1fa0d/Untitled%204.png](R%20648c68dafc5e49449c455147c1f1fa0d/Untitled%204.png)

# Estructuras de datos

## Vectores

Un vector es una colección de uno o más datos del **mismo** tipo.

```r
vector=c(1,2,3) #La c indica concatenar
vector + 2  ===> 3,4,5
vector * 2  ===> 2,4,6
vector[1] #Seleccionar el elemento 1 del vector
vector[c(1,3)] #Seleccionar el elemento 1 y 3 del vector
vector[1:2] #Seleccionar los elementos del 1 al 2
```

## Matrices y arrays

Son vectores multidimensionales. Al igual que un vector, únicamente pueden contener datos de un sólo tipo, pero además de largo, tienen más dimensiones. Cuentan con dos dimensiones, un “largo”" y un “alto”. Las matrices son, por lo tanto, una estructura con forma rectangular, con renglones y columnas.

```r
matrix(1:12, nrow = 3, ncol = 4) #Crear matrices con 3 filas y 4 columnas
#Se van organizando de arriba hacia abajo por columnas
      [,1] [,2] [,3] [,4]
[1,]    1    4    7   10
[2,]    2    5    8   11
[3,]    3    6    9   12

cbind() #para unir vectores, usando cada uno como una columna.
rbind() #para unir vectores, usando cada uno como un renglón.
dim() # para la dimension de una matriz
t(matriz) # Trasponer una matriz

Se puede sumar, multiplicar y elevar por un escalar una matriz.
Esto afecta todos los valores que existen en ella

matriz[filas, columnas] #Seleccion de datos 
```

Las matrices siempre serán rectangulares. Cuando intentamos acomodar un número diferente de elementos y celdas, ocurren dos cosas diferentes. Si el número de elementos es mayor al número de celdas, se acomodarán todos los datos que sean posibles y los demás se omitirán. Si, por el contrario, el número de celdas es mayor que el número de elementos, estos se repetirán.

## Dataframes

Los data frames son estructuras de datos  que pueden contener datos de diferentes tipos. los renglones en un data frame representan casos, individuos u observaciones, mientras que las columnas representan atributos, rasgos o variables. Un data frame está compuesto por vectores.

```r
mi_df <- data.frame(
  "entero" = 1:4, 
  "factor" = c("a", "b", "c", "d"), 
  "numero" = c(1.2, 3.4, 4.5, 5.6),
  "cadena" = as.character(c("a", "b", "c", "d"))
)

dim(mi_df) #Conocer dimensiones dataframe
names(mi_df) #Conocer el nombre de las columnas dataFrame
as.data.frame() #Convertir a data frame
data.frame[indice_filas, indice_columnas] #Seleccion de datos 
data.frame["name_column"] #Seleccion de datos
data.frame$name_column #Seleccion de datos
mi_df$c("nombre", "edad") #Seleccionar datos. 
iris[iris$Sepal.Length > 7.5, ] #Seleccion con validacion
#Otra forma de seleccion
#Data, condicion, seleccion de columnas
subset(x = iris, subset = Sepal.Length > 7.5, select = c("Sepal.Length", "Species"))

```

## Listas

Las listas, al igual que los vectores, son estructuras de datos unidimensionales, sólo tienen largo, pero a diferencia de los vectores cada uno de sus elementos puede ser de diferente tipo o incluso de diferente clase. Al igual que con un data frame, tenemos la opción de poner nombre a cada elemento de una lista.

```r
mi_matriz <- matrix(1:4, nrow = 2)
mi_df     <- data.frame("num" = 1:3, "let" = c("a", "b", "c"))

mi_lista <- list("un_vector" = mi_vector, "una_matriz" = mi_matriz, "un_df" = mi_df)

mi_lista
```

## Coerción

![R%20648c68dafc5e49449c455147c1f1fa0d/Untitled%205.png](R%20648c68dafc5e49449c455147c1f1fa0d/Untitled%205.png)

# Funciones

```r
#Definicion
nombre <- function(argumento1,argumento2,etc) {
  operaciones
}
#Ejemplo
area_cuad <- function(lado1, lado2) {
  lado1 * lado2
}
#Forma de llamado 1 
area_cuad(lado1 = 4, lado2 = 6)
#Forma de llamado 2 
area_cuad(4,6)
```

# Estructuras de control

![R%20648c68dafc5e49449c455147c1f1fa0d/Untitled%206.png](R%20648c68dafc5e49449c455147c1f1fa0d/Untitled%206.png)

## If-Else

```r
if(condición) {
  operaciones_si_la_condición_es_TRUE
} else {
  operaciones_si_la_condición_es_FALSE
}

#Ejemplo
if(media >= 6) {
    print(paste0(texto, "aprobado"))
  } else {
    print(paste0(texto, "reprobado"))
  }

#Otra forma
ifelse(vector, valor_si_TRUE, valor_si_FALSE)

#Ejemplo
ifelse(num %% 2 == 0 & num %% 3, "Divisible", "No divisible")
```

## For

Este ciclo no es el mas recomendado, existe otras alternativas en R mas potenciales para ejecutar estas tareas.

```r
for(elemento in objeto) {
  operacion_con_elemento
}

#Ejemplo
dado <- 1:6
for(cara in dado) {
  dado ^ 2 
}
```

### For para añadir filas a una data table

```r
v<-colores$cod.ext.2
n<-1
list<-as.list(NULL)

for (i in v){
  a<-conector
  a$ext.2<-paste0(i)
  list[[n]]<-a
  conector1<-rbindlist(list)
  n<-n+1
}
```

Para imprimir imagenes de un ggplot

```r
data_g<-data[maquina==i,]

p<-ggplot(data=data_g, aes(x=mes, y=metros, fill=metodo)) +
  geom_bar(stat="identity", position=position_dodge())+
  geom_text(aes(label=metros), vjust=1.6, color="white",
            position = position_dodge(0.9), size=2.8)+
  scale_fill_brewer(palette="Paired")+
  theme_minimal()+ labs(title=paste0(i))+theme(plot.title = element_text(hjust = 0.5))
ggsave(paste0(i,".png"))
print(p)
```

## While

```r
while(condicion) {
  operaciones
}

#Ejemplo
while(i < 10) {
  print("Presiona ESC para detener")
}
```

## Next y Break

```r
#Next (Salta parte de un cilo)
for(i in 1:4) {
  if(i == 3) {
    next
  }
  print(i)
}

#Break (Rompe un ciclo)
for(i in 1:10) {
  if(i == 3) {
    break
  }
  print(i)
}
```

## Repeat

```r
repeat {
  operaciones
  
  un_break_para_detener
}
#Ejemplo
repeat{
  valor <- valor + 1
  if(valor == 5) {
    break
  }
}
```

Si no incluimos un break, el bucle se repetirá indefinidamente y sólo lo podremos detener pulsando la tecla ESC, así que hay que tener cuidado al usar esta estructura de control

# Familia Apply

Se incluye en el paquete base pero se recomienda usar data table, mas rapido y comodo

## Apply

`apply` tiene tres argumentos:

- `X`: Una matriz o un objeto que pueda coercionarse a una matriz, generalmente, un data frame.
- `MARGIN`: La dimensión (margen) que agrupará los elementos de la matriz `X`, para aplicarles una función. Son identificadas con números, **1** son renglones (filas) y **2** son columnas.
- `FUN`: La función que aplicaremos a la matriz `X` en su dimención `MARGIN`.

```r
apply(X, MARGIN, FUN)

#Ejemplo
apply(X = matriz, MARGIN = 1, FUN = sum) #Suma todas filas para el objeto matriz
apply(X = matriz, MARGIN = 2, FUN = sum) #Suma todas las columnas para el objeto matriz
```

## Lapply

lapply() es un caso especial de apply(), diseñado para aplicar funciones a todos los elementos de una lista. La l de su nombre se refiere, precisamente, a lista. lapply siempre nos devolverá una lista como resultado

```r
lapply(X, FUN)
#Ejemplo
lapply(X = trees, FUN = mean) #Promedio de un objeto llamado trees
```

En donde:

- `X` es una lista o un objeto coercionable a una lista.
- `FUN` es la función a aplicar

En muchos casos es posible reemplazar un bucle `for()` por un `lapply()`. De hecho, `lapply()` está haciendo lo mismo que un `for()`, está iterando una operación en todos los elementos de una estructura de datos.

# Excel

```r
library("writexl")
library("readxl")

data<- read_excel("data/data.xlsx")
data<-as.data.table(data)

write_xlsx(comision, "exits/comisiones.xlsx")
```

# Data table

Librería mas veloz y flexible para el manejo de tablas en R. 

Siempre que tengás datos para analizar en computador, tratá de tenerlos en formato largo, es mucho más fácil de trabajar con ellos. Para convertir una tabla ancha en una larga, usá `data.table::melt`.

Simepre que tengás que generar datos para interpretación por humanos, considerá ponerlos en formato ancho, son más fáciles de entender. Podés lograrlo con `data.table::dcast`.

```r
#Actualizar todos los paquetes
update.packages(ask = FALSE)

#Instalar paquete
install.packages("data.table")
install.packages("tidyverse", dependencies = TRUE)

#Cargar libreria
library(data.table)

#Crear data table
mi_df <- data.table(
  "entero" = 1:4, 
  "factor" = c("a", "b", "c", "d"), 
  "numero" = c(1.2, 3.4, 4.5, 5.6),
  "cadena" = as.character(c("a", "b", "c", "d"))
)

#leer datos
data <- fread("data/item_julio.csv")
#Se recomienda usa r col class para idnicar que tipo de datos son y ahorrar tiempo de carga
tipo<-c("character","character","character")#Permite cargar mas rapido y evitar errores
conector <- fread("data/conector_ref.csv", colClasses = tipo)

#Escribir datos
fwrite(x =conector, file = "exit/testing.csv", sep = ",", dec = ".")

#eliminar duplicados
unique(Item)

#Estructura
data table[i,j,by=k]

#i sirve para filtrar
irisDT[Species == "setosa", ]
irisDT[Petal.Width > 2, ]
irisDT[Petal.Width <= 0.3 & Sepal.Length > 5,]
irisDT[c(1, 4),]
irisDT[c("color","altura"),]

#La j sirve para operar (¿que queremos hacer con los datos?)
irisDT[Species == "versicolor", mean(Sepal.Length)]
irisDT[Species == "versicolor", .(promedio = mean(Sepal.Length), mediana = median(Sepal.Length))]   #varias operaciones al mismo tiempo
irisDT[Species == "versicolor", hist(Sepal.Length)]

#La k sirve para agrupar
irisDT[ , mean(Sepal.Length), by = Species]
irisDT[Sepal.Width >= 3, mean(Sepal.Length), by = Species]
irisDT[, mean(Sepal.Length), by = .(Species, petaloPequeno = Petal.Width < .3)]

#Contar el número de registros.
.N 

#Cambiar nombres a las variables
names (DatosTdoPeso) = c("Tratamiento", "Variedad", "Parcela", "Peso46a60")

#Cambiar NA por otros valores
my_data[is.na(my_data)] <- 0

#Cambiar solo un nombre de una columna
names (DatosTdoPeso)[3] = "Parcela"

#Cambiar el orden de las columnas, se recomienda hacerlo por nombres
DatosTdoPeso1 = DatosTdoPeso [ , c(3,2,1,7,6,5,4)]
DatosTdoPeso1 = DatosTdoPeso [ , c("name","fecha","key")]

#cambiar el orden del eje x en ggplot2
equiposDeslizadores1$month <- factor(equiposDeslizadores1$month,levels = c(0,1,2,3,4,5,6,7,8,9,10,11,12,13),labels = c("YTD18", "1","2","3","4","5","6","7","8","9","10","11","12","YTD19"))

#Funciones especiales

#Entre
irisDT[Sepal.Length %between% c(5.1, 5.2)]
#Como 
irisDT[Species %like% "v.*",]

#Tabla ancha a larga
dfLarga_2 <- melt(dfAncha, id.vars = "item",  #id=datos que no vamos a cambiar
                  variable.name = "region",  #var.name= nombre encabezados a poner largos
                  value.name = "valor",  #value= valores de los var.name
                  variable.factor = FALSE)

#Tabla larga a ancha
dfAncha_2 <- dcast(dfLarga, 
                   item ~ region, # x ~ y (filas ~ columnas)
                   value.var = "valor")

#Contar el numero de elementos por filas. Se uso en lista de materiales
col.base<-col.base[ , index := 1:.N , by = c("cod.ext.2.col") ]

#Convierte , en .
epoxica$produccion.und<-gsub(",", ".", epoxica$produccion.und)

#Nueva forma buscarv
nominalesEnsamble <- fread("files/nominales/nominales_ensamble.csv")
setkeyv(ensamble, c("maquina", "proceso"))
setkeyv(nominalesEnsamble, c("maquina", "proceso"))
ensamble[nominalesEnsamble, nominal := nominal]
```

# Eficiencia algoritmo en R

## Microbenchmark

Compara tres metodos para calculas el minimo, el promedio, la mediana, etc. Notese que la escala esta en microsegundos, la diferencias porcentual es alta pero la real es muy poca.

```r
library("microbenchmark")
df = data.frame(v = 1:4, name = letters[1:4])
microbenchmark(df[3, 2], df[3, "name"], df$name[3])
# Unit: microseconds
#          expr     min    lq  mean median    uq   max neval cld
#      df[3, 2]   17.99 18.96 20.16  19.38 19.77 35.14   100   b
# df[3, "name"]   17.97 19.13 21.45  19.64 20.15 74.00   100   b
#    df$name[3]   12.48 13.81 15.81  14.48 15.14 67.24   100   a
```

## Profvis

Muestra cuantos segundos me gasto en cada linea de codigo y cuando es el porcentaje relativo.

```r
library("profvis")
profvis(expr = {
  
  # Stage 1: load packages
  # library("rnoaa") # not necessary as data pre-saved
  library("ggplot2")
  
  # Stage 2: load and process data
  out = readRDS("extdata/out-ice.Rds")
  df = dplyr::rbind_all(out, id = "Year")
  
  # Stage 3: visualise output
  ggplot(df, aes(long, lat, group = paste(group, Year))) +
    geom_path(aes(colour = Year)) 
  ggsave("figures/icesheet-test.png")
}, interval = 0.01, prof_output = "ice-prof")
```

![R%20648c68dafc5e49449c455147c1f1fa0d/Untitled%207.png](R%20648c68dafc5e49449c455147c1f1fa0d/Untitled%207.png)

## Memoization

Permite guardar calculos en cache, para que si vuelven a ser solicitados no sean recalculando, ahorrando tiempo y aumentando la eficiencia en procesos recursivos

```r
plot_mpg = function(row_to_remove) {
  data(mpg, package = "ggplot2")
  mpg = mpg[-row_to_remove, ]
  plot(mpg$cty, mpg$hwy)
  lines(lowess(mpg$cty, mpg$hwy), col = 2)
}

m_plot_mpg = memoise(plot_mpg) #Almacena calculos en cache
```

## Feather

Tipo de documento creado por los desarrolladores de python y R para comprimir datos y aumentar velocidad de procesamiento. Es el mas rapido segun el libro

```r
write_feather(dt.iris, "exit/iris.feather")
df_co2_feather = read_feather("exit/iris.feather")
```

![R%20648c68dafc5e49449c455147c1f1fa0d/Untitled%208.png](R%20648c68dafc5e49449c455147c1f1fa0d/Untitled%208.png)