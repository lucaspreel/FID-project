
<!-- rnb-text-begin -->

---
title: "FIS project : main notebook"
output: html_notebook
---
### 1) Cargamos los datos

Para empezar, se carga el train set y el test set.


<!-- rnb-text-end -->


<!-- rnb-chunk-begin -->


<!-- rnb-source-begin eyJkYXRhIjoiYGBgclxuZGZfdHJhaW4gPC1yZWFkLmNzdjIoXCJkYXRhL3RyYWluLmNzdlwiKVxuZGZfdGVzdCA8LSByZWFkLmNzdjIoXCJkYXRhL3Rlc3QuY3N2XCIpXG5gYGAifQ== -->

```r
df_train <-read.csv2("data/train.csv")
df_test <- read.csv2("data/test.csv")
```

<!-- rnb-source-end -->

<!-- rnb-chunk-end -->


<!-- rnb-text-begin -->


Se verifican las dimensiones del dataset de entrenamiento y del dataset de test.


<!-- rnb-text-end -->


<!-- rnb-chunk-begin -->


<!-- rnb-source-begin eyJkYXRhIjoiYGBgclxuZGltX3RyYWluID0gZGltKGRmX3RyYWluKVxucHJpbnQocGFzdGUoXCJFbCBjdW5qdW50byBkZSBlbnRyZW5hbWllbnRvIHRpZW5lIFwiLCBkaW1fdHJhaW5bMV0sXCJ2YWxvcmVzIHkgXCIsIGRpbV90cmFpblsyXSwgXCJ2YXJpYWJsZXMuXCIgKSlcbmBgYCJ9 -->

```r
dim_train = dim(df_train)
print(paste("El cunjunto de entrenamiento tiene ", dim_train[1],"valores y ", dim_train[2], "variables." ))
```

<!-- rnb-source-end -->

<!-- rnb-output-begin eyJkYXRhIjoiWzFdIFwiRWwgY3VuanVudG8gZGUgZW50cmVuYW1pZW50byB0aWVuZSAgNDUyMTEgdmFsb3JlcyB5ICAxNyB2YXJpYWJsZXMuXCJcbiJ9 -->

```
[1] "El cunjunto de entrenamiento tiene  45211 valores y  17 variables."
```



<!-- rnb-output-end -->

<!-- rnb-source-begin eyJkYXRhIjoiYGBgclxuZGltX3Rlc3QgPSBkaW0oZGZfdGVzdClcbnByaW50KHBhc3RlKFwiRWwgY3VuanVudG8gZGUgdGVzdCB0aWVuZSBcIiwgZGltX3Rlc3RbMV0sXCJ2YWxvcmVzIHkgXCIsIGRpbV90ZXN0WzJdLCBcInZhcmlhYmxlcy5cIiApKVxuYGBgIn0= -->

```r
dim_test = dim(df_test)
print(paste("El cunjunto de test tiene ", dim_test[1],"valores y ", dim_test[2], "variables." ))
```

<!-- rnb-source-end -->

<!-- rnb-output-begin eyJkYXRhIjoiWzFdIFwiRWwgY3VuanVudG8gZGUgdGVzdCB0aWVuZSAgNDUyMSB2YWxvcmVzIHkgIDE3IHZhcmlhYmxlcy5cIlxuIn0= -->

```
[1] "El cunjunto de test tiene  4521 valores y  17 variables."
```



<!-- rnb-output-end -->

<!-- rnb-chunk-end -->


<!-- rnb-text-begin -->


Se visualiza el header del dataset de entrenamiento para ver un poco los datos.


<!-- rnb-text-end -->


<!-- rnb-chunk-begin -->


<!-- rnb-source-begin eyJkYXRhIjoiYGBgclxuaGVhZChkZl90cmFpbilcbmBgYCJ9 -->

```r
head(df_train)
```

<!-- rnb-source-end -->

<!-- rnb-frame-begin eyJtZXRhZGF0YSI6eyJjbGFzc2VzIjpbImRhdGEuZnJhbWUiXSwibnJvdyI6NiwibmNvbCI6MTcsInN1bW1hcnkiOltdfSwicmRmIjoiSDRzSUFBQUFBQUFBQnJWVnpZN1RNQkIyMHFacHcyKzFadzZJS3kxaVYxeTR3cEVENHJRSEpEUjF2SzNCc1NQSFllbHQ3endBYjhTRGNPRXRkcG1rbWZ4WTdiS3FJTkluejR3OW52SDg1Y1BiODdQa1BHR01qZGc0Q05rb1FwSk4zcngvZWZycWxMRnhpRnpBeG14V3JkL3cxQWtTYzhTRDZoamlOZUk1NGluaVJiTStRenl1OTNlS1NRWWExaUlUMnBIRUNiN1Jra3ZRamVRK2JscVJXNkZGYVJ2WnZaVXF4WUlicFlCRWNhbS9hSE9wOTl3OHRCbG5ZSzBVYWNOT0NxblhTdXpmdk52WjRmMVRKNnlUWUxjTlB5c0VOenE5UmVDNTdySGRmVU03b1RaSFVHMStwcDl3ZlZKSkdZdCsxY2xrN0xkblk3UVZ4VjNKems0dC9MdXplM1Y5YndlWnV6Vk94N0ZkdlVZSE1JaEhCdHRqeWRaU1VOMzZBL0VPOFJIeEUvRzk1MGx3QVBYK3pZR3ZwMy9vKy8reC9BZjFPUmdza1lhc3JhVTVSUlA3bXNqUFp0WHJSdWxBVVpPSnRPVGdwR205VE1VRmxJcm1UTHdDQlpxM3Zid3haZFhjRFR0V3BwMC9NVGFyQTA2S283Uk5hNVRoem9iYU5DMXQzOTZVUTVhRFhCTWY1YWhJOVQ3RmNmWlZvc21XTjZYakppTjNncTBYaUprMWwwc0tScFhuOEdxWDA0a2ZNYTZnb0lpUk1FbkJ3ZkxDb2o1eTE1NUtiUExLYjFRS1QzbzEzdzUzNndrZWxicnlKRjN3RFdaK2NWWVo4S28wYUNxUjZQbk9aSGpUWEJYUlFCVjZMVFc5T2xLd0VwVEFoL2ppK3NITDNNcnU5NERTWXVsTWwrZ0Uvd0lrcWQvR3J2OEFZeExWVGJzR0FBQT0ifQ== -->

<div data-pagedtable="false">
  <script data-pagedtable-source type="application/json">
{"columns":[{"label":[""],"name":["_rn_"],"type":[""],"align":["left"]},{"label":["age"],"name":[1],"type":["int"],"align":["right"]},{"label":["job"],"name":[2],"type":["chr"],"align":["left"]},{"label":["marital"],"name":[3],"type":["chr"],"align":["left"]},{"label":["education"],"name":[4],"type":["chr"],"align":["left"]},{"label":["default"],"name":[5],"type":["chr"],"align":["left"]},{"label":["balance"],"name":[6],"type":["int"],"align":["right"]},{"label":["housing"],"name":[7],"type":["chr"],"align":["left"]},{"label":["loan"],"name":[8],"type":["chr"],"align":["left"]},{"label":["contact"],"name":[9],"type":["chr"],"align":["left"]},{"label":["day"],"name":[10],"type":["int"],"align":["right"]},{"label":["month"],"name":[11],"type":["chr"],"align":["left"]},{"label":["duration"],"name":[12],"type":["int"],"align":["right"]},{"label":["campaign"],"name":[13],"type":["int"],"align":["right"]},{"label":["pdays"],"name":[14],"type":["int"],"align":["right"]},{"label":["previous"],"name":[15],"type":["int"],"align":["right"]},{"label":["poutcome"],"name":[16],"type":["chr"],"align":["left"]},{"label":["y"],"name":[17],"type":["chr"],"align":["left"]}],"data":[{"1":"58","2":"management","3":"married","4":"tertiary","5":"no","6":"2143","7":"yes","8":"no","9":"unknown","10":"5","11":"may","12":"261","13":"1","14":"-1","15":"0","16":"unknown","17":"no","_rn_":"1"},{"1":"44","2":"technician","3":"single","4":"secondary","5":"no","6":"29","7":"yes","8":"no","9":"unknown","10":"5","11":"may","12":"151","13":"1","14":"-1","15":"0","16":"unknown","17":"no","_rn_":"2"},{"1":"33","2":"entrepreneur","3":"married","4":"secondary","5":"no","6":"2","7":"yes","8":"yes","9":"unknown","10":"5","11":"may","12":"76","13":"1","14":"-1","15":"0","16":"unknown","17":"no","_rn_":"3"},{"1":"47","2":"blue-collar","3":"married","4":"unknown","5":"no","6":"1506","7":"yes","8":"no","9":"unknown","10":"5","11":"may","12":"92","13":"1","14":"-1","15":"0","16":"unknown","17":"no","_rn_":"4"},{"1":"33","2":"unknown","3":"single","4":"unknown","5":"no","6":"1","7":"no","8":"no","9":"unknown","10":"5","11":"may","12":"198","13":"1","14":"-1","15":"0","16":"unknown","17":"no","_rn_":"5"},{"1":"35","2":"management","3":"married","4":"tertiary","5":"no","6":"231","7":"yes","8":"no","9":"unknown","10":"5","11":"may","12":"139","13":"1","14":"-1","15":"0","16":"unknown","17":"no","_rn_":"6"}],"options":{"columns":{"min":{},"max":[10],"total":[17]},"rows":{"min":[10],"max":[10],"total":[6]},"pages":{}}}
  </script>
</div>

<!-- rnb-frame-end -->

<!-- rnb-chunk-end -->


<!-- rnb-text-begin -->



### 2) Exploración y visualización de los datos

Para conocer un poco más los datos se procede a visualizar las variables del dataset de entrenamiento.


<!-- rnb-text-end -->


<!-- rnb-chunk-begin -->


<!-- rnb-source-begin eyJkYXRhIjoiYGBgclxuIyBTZSBjYXJnYSBsYSBsaWJyZXLDrWEgdGlkeXZlcnNlIHBhcmEgbWFuaXB1bGFyIGxvcyBkYXRvcyBtw6FzIGZhY2lsbWVudGVcblxubGlicmFyeSh0aWR5dmVyc2UpXG5gYGAifQ== -->

```r
# Se carga la librería tidyverse para manipular los datos más facilmente

library(tidyverse)
```

<!-- rnb-source-end -->

<!-- rnb-output-begin eyJkYXRhIjoiUmVnaXN0ZXJlZCBTMyBtZXRob2RzIG92ZXJ3cml0dGVuIGJ5ICdkYnBseXInOlxuICBtZXRob2QgICAgICAgICBmcm9tXG4gIHByaW50LnRibF9sYXp5ICAgICBcbiAgcHJpbnQudGJsX3NxbCAgICAgIFxuLS0gQXR0YWNoaW5nIHBhY2thZ2VzIC0tLS0tLS0tLS0tLS0tLS0tLS0tLS0tLS0tLS0tLS0tLS0tLS0tLS0tLS0tLS0tLS0tLS0tLS0tLS0tLS0tLS0tLS0tLS0tLS0tLS0tLS0tLS0tLS0tLS0tLS0tLS0tLS0tLS0tLS0tLS0tLS0tIHRpZHl2ZXJzZSAxLjMuMSAtLVxudiBnZ3Bsb3QyIDMuMy41ICAgICB2IHB1cnJyICAgMC4zLjRcbnYgdGliYmxlICAzLjEuNSAgICAgdiBkcGx5ciAgIDEuMC43XG52IHRpZHlyICAgMS4xLjQgICAgIHYgc3RyaW5nciAxLjQuMFxudiByZWFkciAgIDIuMC4yICAgICB2IGZvcmNhdHMgMC41LjFcbi0tIENvbmZsaWN0cyAtLS0tLS0tLS0tLS0tLS0tLS0tLS0tLS0tLS0tLS0tLS0tLS0tLS0tLS0tLS0tLS0tLS0tLS0tLS0tLS0tLS0tLS0tLS0tLS0tLS0tLS0tLS0tLS0tLS0tLS0tLS0tLS0tLS0tLS0tLS0tLS0tLS0tLSB0aWR5dmVyc2VfY29uZmxpY3RzKCkgLS1cbnggZHBseXI6OmZpbHRlcigpIG1hc2tzIHN0YXRzOjpmaWx0ZXIoKVxueCBkcGx5cjo6bGFnKCkgICAgbWFza3Mgc3RhdHM6OmxhZygpXG4ifQ== -->

```
Registered S3 methods overwritten by 'dbplyr':
  method         from
  print.tbl_lazy     
  print.tbl_sql      
-- Attaching packages -------------------------------------------------------------------------------------------------------------- tidyverse 1.3.1 --
v ggplot2 3.3.5     v purrr   0.3.4
v tibble  3.1.5     v dplyr   1.0.7
v tidyr   1.1.4     v stringr 1.4.0
v readr   2.0.2     v forcats 0.5.1
-- Conflicts ----------------------------------------------------------------------------------------------------------------- tidyverse_conflicts() --
x dplyr::filter() masks stats::filter()
x dplyr::lag()    masks stats::lag()
```



<!-- rnb-output-end -->

<!-- rnb-source-begin eyJkYXRhIjoiYGBgclxuIyBHcmFjaWFzIGEgZXNvLCBhaG9yYSBzZSBwdWVkZSB1dGlsaXphciBlbCBvcGVyYWRvciAlPiUgcGFyYSBjcmVhciB1bmEgcGlwZWxpbmUgZW4gbGEgcXVlIHNlIGFwbGlxdWVuIHZhcmlhcyBvcGVyYWNpb25lcyBhIGxvcyBkYXRvcyAocG9yIGVqZW1wbG8gXCJtdXRhdGVcIiBwYXJhIGHDsWFkaXIgbnVldmFzIHZhcmlhYmxlcywgXCJzZWxlY3RcIiBwYXJhIGd1YXJkYXIgc29sYW1lbnRlIGxhcyB2YXJpYWJsZXMgcXVlIHF1ZXJlbW9zLCBcImZpbHRlclwiIHBhcmEgZmlsdHJhciBsb3MgZGF0b3Mgc2Vnw7puIHZhbG9yZXMsIGV0YykuXG5cbmBgYCJ9 -->

```r
# Gracias a eso, ahora se puede utilizar el operador %>% para crear una pipeline en la que se apliquen varias operaciones a los datos (por ejemplo "mutate" para añadir nuevas variables, "select" para guardar solamente las variables que queremos, "filter" para filtrar los datos según valores, etc).

```

<!-- rnb-source-end -->

<!-- rnb-chunk-end -->


<!-- rnb-text-begin -->


#### 2.1) Visualización de la variable "age"

Esta variable representa la edad de cada cliente. Es una variable numérica y se va a visualizar con un gráfico que representa en el eje "x" la edad y en el eje "y" el número de clientes que tienen esa edad. Sin embargo, como hay muchos edades diferentes se van a crear grupos de edad para que sea más facil visualizar.


<!-- rnb-text-end -->


<!-- rnb-chunk-begin -->


<!-- rnb-source-begin eyJkYXRhIjoiYGBgclxuXG4jIHNlIGNyZWFuIGdydXBvcyBkZSBlZGFkIHBvcnF1ZSBoYXkgbXVjaG9zIGVkYWRlcyBkaWZlcmVudGVzXG4jIHNlIGNyZWEgdW5hIHZhcmlhYmxlIHF1ZSBjdWVudGEgcGFyYSBjYWRhIGdydXBvIGRlIGVkYWQgZWwgbsO6bWVybyBkZSBjbGllbnRlc1xuXG5lZGFkIDwtIGRmX3RyYWluICU+JVxuICBtdXRhdGUoZWRhZF9pbnRlcnZhbCA9IGN1dF9pbnRlcnZhbChkZl90cmFpbiRhZ2UsIGxlbmd0aCA9IDUpKSAlPiVcbiAgZ3JvdXBfYnkoZWRhZF9pbnRlcnZhbCkgJT4lXG4gIGNvdW50KClcblxuIyBzZSB2aXN1YWxpemEgZXNvIGVuIHVuIGdyw6FmaWNvXG5cbiBnZ3Bsb3QoZWRhZCwgYWVzKHggPSBlZGFkX2ludGVydmFsLCB5PW4pKSArXG4gICBnZW9tX2JhcihzdGF0PVwiaWRlbnRpdHlcIikgK1xuICAgZ2d0aXRsZShcIk7Dum1lcm8gZGUgY2xpZW50ZXMgZW4gZnVuY2nDs24gZGUgbGEgZWRhZFwiKSArXG4gICBsYWJzKHg9XCJlZGFkXCIsIHkgPSBcIm7Dum1lcm8gZGUgY2xpZW50ZXNcIilcbmBgYCJ9 -->

```r

# se crean grupos de edad porque hay muchos edades diferentes
# se crea una variable que cuenta para cada grupo de edad el número de clientes

edad <- df_train %>%
  mutate(edad_interval = cut_interval(df_train$age, length = 5)) %>%
  group_by(edad_interval) %>%
  count()

# se visualiza eso en un gráfico

 ggplot(edad, aes(x = edad_interval, y=n)) +
   geom_bar(stat="identity") +
   ggtitle("Número de clientes en función de la edad") +
   labs(x="edad", y = "número de clientes")
```

<!-- rnb-source-end -->

<!-- rnb-plot-begin eyJoZWlnaHQiOjQzMi42MzI5LCJ3aWR0aCI6NzAwLCJzaXplX2JlaGF2aW9yIjowLCJjb25kaXRpb25zIjpbXX0= -->

<img src="data:image/png;base64,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" />

<!-- rnb-plot-end -->

<!-- rnb-chunk-end -->


<!-- rnb-text-begin -->

Se puede ver que la mayoria de los clientes tienen entre 25 y 60 años y muchos tienen entre 30 y 40 años. Los clientes representan bien la mayoria de la población trabajadora.

#### 2.2) Visualización de la variable "job"

Esta variable representa qué tipo de trabajo tiene cada cliente. Es una variable categórica (es decir que la variable sólo puede tomar un número finito de categorías) y nominal (es decir que no hay orden entre las diferentes categorías). Se va a visualizar con un gráfico circular.


<!-- rnb-text-end -->


<!-- rnb-chunk-begin -->


<!-- rnb-source-begin eyJkYXRhIjoiYGBgclxuXG4jIHNlIGNyZWEgdW5hIHZhcmlhYmxlIHF1ZSBjdWVudGEgcGFyYSBjYWRhIGpvYiBlbCBuw7ptZXJvIGRlIGNsaWVudGVzLCB5IHNlIGNsYXNpZmljYW4gbG9zIGpvYnMgZGVsIHF1ZSB0aWVuZSBtw6FzIGNsaWVudGVzIGFsIHF1ZSB0aWVuZSBtZW5vc1xuXG5qb2IgPC0gZGZfdHJhaW4gJT4lXG4gIGdyb3VwX2J5KGRmX3RyYWluJGpvYikgJT4lXG4gIGNvdW50KCkgJT4lXG4gIGFycmFuZ2UoZGVzYyhuKSlcblxuIyBzZSB2YSBhIHV0aWxpemFyIGxhIHBhbGV0YSBkZSBjb2xvcmVzIFwidmlyaWRpc1wiIHBhcmEgbGEgdmlzdWFsaXphY2nDs24gKGhhY2UgZmFsdGEgZGVzY29tZW50YXIgbGEgc2lndWllbnRlIGzDrW5lYSBzaSB5YSBubyBlc3TDoSBpbnN0YWxhZG8pXG4jIGluc3RhbGwucGFja2FnZXMoXCJ2aXJpZGlzXCIpXG5saWJyYXJ5KFwidmlyaWRpc1wiKVxuYGBgIn0= -->

```r

# se crea una variable que cuenta para cada job el número de clientes, y se clasifican los jobs del que tiene más clientes al que tiene menos

job <- df_train %>%
  group_by(df_train$job) %>%
  count() %>%
  arrange(desc(n))

# se va a utilizar la paleta de colores "viridis" para la visualización (hace falta descomentar la siguiente línea si ya no está instalado)
# install.packages("viridis")
library("viridis")
```

<!-- rnb-source-end -->

<!-- rnb-output-begin eyJkYXRhIjoiTGUgY2hhcmdlbWVudCBhIG7DqWNlc3NpdMOpIGxlIHBhY2thZ2UgOiB2aXJpZGlzTGl0ZVxuIn0= -->

```
Le chargement a nécessité le package : viridisLite
```



<!-- rnb-output-end -->

<!-- rnb-source-begin eyJkYXRhIjoiYGBgclxuIyBzZSBjb25zdHJ1eWUgZWwgZ3LDoWZpY29cbnBpZSh4PWpvYiRuLFxuICAgIGxhYmVscyA9IGpvYiRgZGZfdHJhaW4kam9iYCxcbiAgICByYWRpdXMgPSAxLFxuICAgIG1haW4gPSBcIk7Dum1lcm8gZGUgY2xpZW50ZXMgZW4gZnVuY2nDs24gZGVsIGpvYlwiLFxuICAgIGNvbCA9IHZpcmlkaXMobGVuZ3RoKGpvYiRuKSkpXG5gYGAifQ== -->

```r
# se construye el gráfico
pie(x=job$n,
    labels = job$`df_train$job`,
    radius = 1,
    main = "Número de clientes en función del job",
    col = viridis(length(job$n)))
```

<!-- rnb-source-end -->

<!-- rnb-plot-begin eyJoZWlnaHQiOjQzMi42MzI5LCJ3aWR0aCI6NzAwLCJzaXplX2JlaGF2aW9yIjowLCJjb25kaXRpb25zIjpbXX0= -->

<img src="data:image/png;base64,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" />

<!-- rnb-plot-end -->

<!-- rnb-chunk-end -->


<!-- rnb-text-begin -->

Ahora se pueden ver los jobs mayoritarios entre los clientes. Se observa que los clientes tienen muchos tipos de jobs, así que los datos son representativos de la población (no representan una única categoría profesional).

#### 2.3) Visualización de la variable "marital"

Esta variable representa la situación marital de cada cliente. Se va a visuar de la misma manera que la variable anterior porque es una variable categórica y nominal.


<!-- rnb-text-end -->


<!-- rnb-chunk-begin -->


<!-- rnb-source-begin eyJkYXRhIjoiYGBgclxuXG4jIHNlIGNyZWFyIHVuYSB2YXJpYWJsZSBxdWUgY3VlbnRhIHBhcmEgY2FkYSBlc3RhZG8gcG9zaWJsZSBkZSBsYSB2YXJpYWJsZSBcIm1hcml0YWxcIiBlbCBuw7ptZXJvIGRlIGNsaWVudGVzIHF1ZSBlc3TDoW4gZW4gZXN0ZSBlc3RhZG9cbiMgc2UgY2xhc2lmaWNhbiBsb3MgZXN0YWRvcyBkZWwgcXVlIHRpZW5lICBtw6FzIGNsaWVudGVzIGFsIHF1ZSB0aWVuZSBtZW5vc1xuXG5tYXJpdGFsIDwtIGRmX3RyYWluICU+JVxuICBncm91cF9ieShkZl90cmFpbiRtYXJpdGFsKSAlPiVcbiAgY291bnQoKSAlPiVcbiAgYXJyYW5nZShkZXNjKG4pKVxuXG4jIHNlIHZpc3VhbGl6YSBlc28gZW4gdW4gZ3LDoWZpY28gY2lyY3VsYXIgKGRlIGxhIG1pc21hIG1hbmVyYSBxdWUgcGFyYSBsYSB2YXJpYWJsZSBcImpvYnNcIilcblxucGllKHg9bWFyaXRhbCRuLFxuICAgIGxhYmVscyA9IG1hcml0YWwkYGRmX3RyYWluJG1hcml0YWxgLFxuICAgIHJhZGl1cyA9IDEsXG4gICAgbWFpbiA9IFwiQ2xpZW50ZXMgZW4gZnVuY2nDs24gZGVsIHZhbG9yIGRlIGxhIHZhcmlhYmxlIG1hcml0YWxcIixcbiAgICBjb2wgPSB2aXJpZGlzKGxlbmd0aChtYXJpdGFsJG4pKSlcblxuYGBgIn0= -->

```r

# se crear una variable que cuenta para cada estado posible de la variable "marital" el número de clientes que están en este estado
# se clasifican los estados del que tiene  más clientes al que tiene menos

marital <- df_train %>%
  group_by(df_train$marital) %>%
  count() %>%
  arrange(desc(n))

# se visualiza eso en un gráfico circular (de la misma manera que para la variable "jobs")

pie(x=marital$n,
    labels = marital$`df_train$marital`,
    radius = 1,
    main = "Clientes en función del valor de la variable marital",
    col = viridis(length(marital$n)))

```

<!-- rnb-source-end -->

<!-- rnb-plot-begin eyJoZWlnaHQiOjQzMi42MzI5LCJ3aWR0aCI6NzAwLCJzaXplX2JlaGF2aW9yIjowLCJjb25kaXRpb25zIjpbXX0= -->

<img src="data:image/png;base64,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" />

<!-- rnb-plot-end -->

<!-- rnb-chunk-end -->


<!-- rnb-text-begin -->


De nuevo se puede observar que los datos representan bien cada categoría de la población porque hay muchos cientes para cada categoría.

#### 2.4) Visualización de la variable "education"

Esta variable representa el nivel de educación de cada cliente. Es una variable categórica y nominal.


<!-- rnb-text-end -->


<!-- rnb-chunk-begin -->


<!-- rnb-source-begin eyJkYXRhIjoiYGBgclxuXG5uaXZlbF9lZHVjYWNpw7NuIDwtIGRmX3RyYWluICU+JVxuICBncm91cF9ieShkZl90cmFpbiRlZHVjYXRpb24pICU+JVxuICBjb3VudCgpICU+JVxuICBhcnJhbmdlKGRlc2MobikpXG5cbnBpZSh4PW5pdmVsX2VkdWNhY2nDs24kbixcbiAgICBsYWJlbHMgPSBuaXZlbF9lZHVjYWNpw7NuJGBkZl90cmFpbiRlZHVjYXRpb25gLFxuICAgIHJhZGl1cyA9IDEsXG4gICAgbWFpbiA9IFwiTml2ZWwgZGUgZWR1Y2FjacOzbiBkZSBsb3MgY2xpZW50ZXNcIixcbiAgICBjb2wgPSB2aXJpZGlzKGxlbmd0aChuaXZlbF9lZHVjYWNpw7NuJG4pKSlcbmBgYCJ9 -->

```r

nivel_educación <- df_train %>%
  group_by(df_train$education) %>%
  count() %>%
  arrange(desc(n))

pie(x=nivel_educación$n,
    labels = nivel_educación$`df_train$education`,
    radius = 1,
    main = "Nivel de educación de los clientes",
    col = viridis(length(nivel_educación$n)))
```

<!-- rnb-source-end -->

<!-- rnb-plot-begin eyJoZWlnaHQiOjQzMi42MzI5LCJ3aWR0aCI6NzAwLCJzaXplX2JlaGF2aW9yIjowLCJjb25kaXRpb25zIjpbXX0= -->

<img src="data:image/png;base64,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" />

<!-- rnb-plot-end -->

<!-- rnb-source-begin eyJkYXRhIjoiYGBgclxuTkFcbk5BXG5gYGAifQ== -->

```r
NA
NA
```

<!-- rnb-source-end -->

<!-- rnb-chunk-end -->


<!-- rnb-text-begin -->

Otra vez se puede ver que los datos representan bien cada categoría de la población.

#### 2.5) Visualización de la variable "default"

Esta variable trata de si los clientes tienen un credito impagado (si o no). Es una variable binaria que también se va a visualizar con un gráfico circular.


<!-- rnb-text-end -->


<!-- rnb-chunk-begin -->


<!-- rnb-source-begin eyJkYXRhIjoiYGBgclxuXG5jcsOpZGl0b19pbXBhZ2FkbyA8LSBkZl90cmFpbiAlPiVcbiAgZ3JvdXBfYnkoZGZfdHJhaW4kZGVmYXVsdCkgJT4lXG4gIGNvdW50KClcblxucGllKHg9Y3LDqWRpdG9faW1wYWdhZG8kbixcbiAgICBsYWJlbHMgPSBjcsOpZGl0b19pbXBhZ2FkbyRgZGZfdHJhaW4kZGVmYXVsdGAsXG4gICAgcmFkaXVzID0gMSxcbiAgICBtYWluID0gXCJDbGllbnRlcyBxdWUgdGllbmVuIHVuIGNyw6lkaXRvIGltcGFnYWRvIHkgbG9zIHF1ZSBub1wiLFxuICAgIGNvbCA9IHZpcmlkaXMobGVuZ3RoKGNyw6lkaXRvX2ltcGFnYWRvJG4pKSlcblxuYGBgIn0= -->

```r

crédito_impagado <- df_train %>%
  group_by(df_train$default) %>%
  count()

pie(x=crédito_impagado$n,
    labels = crédito_impagado$`df_train$default`,
    radius = 1,
    main = "Clientes que tienen un crédito impagado y los que no",
    col = viridis(length(crédito_impagado$n)))

```

<!-- rnb-source-end -->

<!-- rnb-plot-begin eyJoZWlnaHQiOjQzMi42MzI5LCJ3aWR0aCI6NzAwLCJzaXplX2JlaGF2aW9yIjowLCJjb25kaXRpb25zIjpbXX0= -->

<img src="data:image/png;base64,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" />

<!-- rnb-plot-end -->

<!-- rnb-chunk-end -->


<!-- rnb-text-begin -->

Se puede ver que la mayoría de los clientes no tienen crédito impagado.

#### 2.6) Visualización de la variable "balance"

Esta variable representa el saldo anual medio (en euros) de los clientes.


<!-- rnb-text-end -->


<!-- rnb-chunk-begin -->


<!-- rnb-source-begin eyJkYXRhIjoiYGBgclxuXG4gZ2dwbG90KGRmX3RyYWluLCBhZXMoeCA9IGJhbGFuY2UpKSArXG4gIGdlb21faGlzdG9ncmFtKGJpbnMgPSAzMCkgK1xuICBnZ3RpdGxlKFwiTsO6bWVybyBkZSBjbGllbnRlcyBlbiBmdW5jacOzbiBkZWwgc2FsZG8gYW51YWwgbWVkaW9cIikgK1xuICBsYWJzKHg9XCJzYWxkbyBhbnVhbCBtZWRpbyAoZXVyb3MpXCIsIHkgPSBcIm7Dum1lcm8gZGUgY2xpZW50ZXNcIikgK1xuICB4bGltKC01MDAwLCAyNTAwMClcbmBgYCJ9 -->

```r

 ggplot(df_train, aes(x = balance)) +
  geom_histogram(bins = 30) +
  ggtitle("Número de clientes en función del saldo anual medio") +
  labs(x="saldo anual medio (euros)", y = "número de clientes") +
  xlim(-5000, 25000)
```

<!-- rnb-source-end -->

<!-- rnb-output-begin eyJkYXRhIjoiV2FybmluZzogUmVtb3ZlZCA5OSByb3dzIGNvbnRhaW5pbmcgbm9uLWZpbml0ZSB2YWx1ZXMgKHN0YXRfYmluKS5cbldhcm5pbmc6IFJlbW92ZWQgMiByb3dzIGNvbnRhaW5pbmcgbWlzc2luZyB2YWx1ZXMgKGdlb21fYmFyKS5cbiJ9 -->

```
Warning: Removed 99 rows containing non-finite values (stat_bin).
Warning: Removed 2 rows containing missing values (geom_bar).
```



<!-- rnb-output-end -->

<!-- rnb-plot-begin eyJoZWlnaHQiOjQzMi42MzI5LCJ3aWR0aCI6NzAwLCJzaXplX2JlaGF2aW9yIjowLCJjb25kaXRpb25zIjpbXX0= -->

<img src="data:image/png;base64,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" />

<!-- rnb-plot-end -->

<!-- rnb-chunk-end -->


<!-- rnb-text-begin -->

Se puede ver que la mayoría de los clientes tienen un saldo anual medio cerca de 0 (menos de 5000 euros), mientras que hay una pequeña parte de los clientes que tienen un saldo anual medio más importante. Esto parece ser representativo de la población. Además, no se ve en el gráfico porque el eje "x" se para en 25 000 pero hay algunos clientes con un saldo anual medio muy grande que se pueden considerar como outliers.

#### 2.7) Visualización de la variable "housing"

Esta variable determina si el cliente tiene una propiedad (si o no).


<!-- rnb-text-end -->


<!-- rnb-chunk-begin -->


<!-- rnb-source-begin eyJkYXRhIjoiYGBgclxuaG91c2luZyA8LSBkZl90cmFpbiAlPiVcbiAgZ3JvdXBfYnkoZGZfdHJhaW4kaG91c2luZykgJT4lXG4gIGNvdW50KClcblxucGllKHg9aG91c2luZyRuLFxuICAgIGxhYmVscyA9IGhvdXNpbmckYGRmX3RyYWluJGhvdXNpbmdgLFxuICAgIHJhZGl1cyA9IDEsXG4gICAgbWFpbiA9IFwiUmVwYXJ0aWNpw7NuIGRlIGxvcyBjbGllbnRlcyBlbiBmdW5jacOzbiBkZSBzaSB0aWVuZW4gdW5hIHByb3BpZWRhZCBvIG5vXCIsXG5cbiAgICBjb2wgPSB2aXJpZGlzKGxlbmd0aChob3VzaW5nJG4pKSlcbmBgYCJ9 -->

```r
housing <- df_train %>%
  group_by(df_train$housing) %>%
  count()

pie(x=housing$n,
    labels = housing$`df_train$housing`,
    radius = 1,
    main = "Repartición de los clientes en función de si tienen una propiedad o no",

    col = viridis(length(housing$n)))
```

<!-- rnb-source-end -->

<!-- rnb-plot-begin eyJoZWlnaHQiOjQzMi42MzI5LCJ3aWR0aCI6NzAwLCJzaXplX2JlaGF2aW9yIjowLCJjb25kaXRpb25zIjpbXX0= -->

<img src="data:image/png;base64,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" />

<!-- rnb-plot-end -->

<!-- rnb-chunk-end -->


<!-- rnb-text-begin -->

Se puede ver que hay muchos clientes para ambas categorías.

#### 2.8) Visualización de la variable "loan"

Esta variable determina si el cliente tiene prestamos activos (si o no).


<!-- rnb-text-end -->


<!-- rnb-chunk-begin -->


<!-- rnb-source-begin eyJkYXRhIjoiYGBgclxubG9hbiA8LSBkZl90cmFpbiAlPiVcbiAgZ3JvdXBfYnkoZGZfdHJhaW4kbG9hbikgJT4lXG4gIGNvdW50KClcblxucGllKHg9bG9hbiRuLFxuICAgIGxhYmVscyA9IGxvYW4kYGRmX3RyYWluJGxvYW5gLFxuICAgIHJhZGl1cyA9IDEsXG4gICAgbWFpbiA9IFwiUmVwYXJ0aWNpw7NuIGRlIGxvcyBjbGllbnRlcyBlbiBmdW5jacOzbiBkZSBzaSB0aWVuZW4gdW4gY3JlZGl0byBhY3Rpdm8gbyBub1wiLFxuICAgIGNvbCA9IHZpcmlkaXMobGVuZ3RoKGxvYW4kbikpKVxuYGBgIn0= -->

```r
loan <- df_train %>%
  group_by(df_train$loan) %>%
  count()

pie(x=loan$n,
    labels = loan$`df_train$loan`,
    radius = 1,
    main = "Repartición de los clientes en función de si tienen un credito activo o no",
    col = viridis(length(loan$n)))
```

<!-- rnb-source-end -->

<!-- rnb-plot-begin eyJoZWlnaHQiOjQzMi42MzI5LCJ3aWR0aCI6NzAwLCJzaXplX2JlaGF2aW9yIjowLCJjb25kaXRpb25zIjpbXX0= -->

<img src="data:image/png;base64,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" />

<!-- rnb-plot-end -->

<!-- rnb-chunk-end -->


<!-- rnb-text-begin -->

Muchos clientes no tienen credito activo pero ambas categorías están bien representadas, así que esta variable también parece ser representativo de la población.

#### 2.9) Visualización de la variable "contact"

Esta variable determina el medio por el cual el cliente fue contactado.


<!-- rnb-text-end -->


<!-- rnb-chunk-begin -->


<!-- rnb-source-begin eyJkYXRhIjoiYGBgclxuXG5jb250YWN0IDwtIGRmX3RyYWluICU+JVxuICBncm91cF9ieShkZl90cmFpbiRjb250YWN0KSAlPiVcbiAgY291bnQoKVxuXG5waWUoeD1jb250YWN0JG4sXG4gICAgbGFiZWxzID0gY29udGFjdCRgZGZfdHJhaW4kY29udGFjdGAsXG4gICAgcmFkaXVzID0gMSxcbiAgICBtYWluID0gXCJOw7ptZXJvIGRlIGNsaWVudGVzIGVuIGZ1bmNpw7NuIGRlbCBtZWRpbyBwb3IgZWwgY3XDoWwgZnVlcm9uIGNvbnRhY3RhZG9zXCIsXG4gICAgY29sID0gdmlyaWRpcyhsZW5ndGgoY29udGFjdCRuKSkpXG5gYGAifQ== -->

```r

contact <- df_train %>%
  group_by(df_train$contact) %>%
  count()

pie(x=contact$n,
    labels = contact$`df_train$contact`,
    radius = 1,
    main = "Número de clientes en función del medio por el cuál fueron contactados",
    col = viridis(length(contact$n)))
```

<!-- rnb-source-end -->

<!-- rnb-plot-begin eyJoZWlnaHQiOjQzMi42MzI5LCJ3aWR0aCI6NzAwLCJzaXplX2JlaGF2aW9yIjowLCJjb25kaXRpb25zIjpbXX0= -->

<img src="data:image/png;base64,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" />

<!-- rnb-plot-end -->

<!-- rnb-chunk-end -->


<!-- rnb-text-begin -->

No hay mucho que interpretar de este gráfico.

#### 2.10) Visualización de la variable "day"

Esta variable representa el día del mes en el cual fue contactado el cliente. Puede ser útil tener eso porque puede tener un impacto en la decisión del cliente. Por ejemplo los clientes pueden decir mas facilmente "si" al principio del mes.


<!-- rnb-text-end -->


<!-- rnb-chunk-begin -->


<!-- rnb-source-begin eyJkYXRhIjoiYGBgclxuXG5nZ3Bsb3QoZGZfdHJhaW4sIGFlcyh4ID0gZGF5KSkgK1xuICBnZW9tX2hpc3RvZ3JhbShiaW5zID0gMzEpICtcbiAgZ2d0aXRsZShcIk7Dum1lcm8gZGUgY2xpZW50ZXMgZW4gZnVuY2nDs24gZGVsIGTDrWEgZW4gZWwgY3VhbCBmdWVyb24gY29udGFjdGFkb3NcIikgK1xuICBsYWJzKHg9XCJkw61hIGRlbCBtZXNcIiwgeSA9IFwibsO6bWVybyBkZSBjbGllbnRlc1wiKVxuXG5gYGAifQ== -->

```r

ggplot(df_train, aes(x = day)) +
  geom_histogram(bins = 31) +
  ggtitle("Número de clientes en función del día en el cual fueron contactados") +
  labs(x="día del mes", y = "número de clientes")

```

<!-- rnb-source-end -->

<!-- rnb-plot-begin eyJoZWlnaHQiOjQzMi42MzI5LCJ3aWR0aCI6NzAwLCJzaXplX2JlaGF2aW9yIjowLCJjb25kaXRpb25zIjpbXX0= -->

<img src="data:image/png;base64,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" />

<!-- rnb-plot-end -->

<!-- rnb-chunk-end -->


<!-- rnb-text-begin -->


En general, se puede observar que hay muchos clientes para cada día del mes, así que no hay desequilibrio en los datos.

#### 2.11) Visualización de la variable "duration"

Esta variable representa la duración de la llamada (en segundos).


<!-- rnb-text-end -->


<!-- rnb-chunk-begin -->


<!-- rnb-source-begin eyJkYXRhIjoiYGBgclxuZ2dwbG90KGRmX3RyYWluLCBhZXMoeCA9IGR1cmF0aW9uKSkgK1xuICBnZW9tX2hpc3RvZ3JhbShiaW5zID0gMjApICtcbiAgZ2d0aXRsZShcIk7Dum1lcm8gZGUgY2xpZW50ZXMgZW4gZnVuY2nDs24gZGUgbGEgZHVyYWNpw7NuIGRlIGxhIGxsYW1hZGFcIikgK1xuICBsYWJzKHg9XCJkdXJhY2nDs24gZGUgbGEgbGxhbWRhZGEgKHNlZ3VuZG9zKVwiLCB5ID0gXCJuw7ptZXJvIGRlIGNsaWVudGVzXCIpICtcbiAgeGxpbSgwLDEwMDApXG5gYGAifQ== -->

```r
ggplot(df_train, aes(x = duration)) +
  geom_histogram(bins = 20) +
  ggtitle("Número de clientes en función de la duración de la llamada") +
  labs(x="duración de la llamdada (segundos)", y = "número de clientes") +
  xlim(0,1000)
```

<!-- rnb-source-end -->

<!-- rnb-output-begin eyJkYXRhIjoiV2FybmluZzogUmVtb3ZlZCAxMDU4IHJvd3MgY29udGFpbmluZyBub24tZmluaXRlIHZhbHVlcyAoc3RhdF9iaW4pLlxuV2FybmluZzogUmVtb3ZlZCAyIHJvd3MgY29udGFpbmluZyBtaXNzaW5nIHZhbHVlcyAoZ2VvbV9iYXIpLlxuIn0= -->

```
Warning: Removed 1058 rows containing non-finite values (stat_bin).
Warning: Removed 2 rows containing missing values (geom_bar).
```



<!-- rnb-output-end -->

<!-- rnb-plot-begin eyJoZWlnaHQiOjQzMi42MzI5LCJ3aWR0aCI6NzAwLCJzaXplX2JlaGF2aW9yIjowLCJjb25kaXRpb25zIjpbXX0= -->

<img src="data:image/png;base64,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" />

<!-- rnb-plot-end -->

<!-- rnb-chunk-end -->


<!-- rnb-text-begin -->


Sólo se puede observar que la mayoría de las llamadas duran menos de 10 minutos y muchas duran 2-3 minutos.

Las visualización de las siguientes variables es de poco interés, así que ahora solo se va a visualizar la clase final.

#### 2.12) Visualización de la clase final

Esta variable dice si el cliente ha suscrito a un un term deposit (si o no). La visualización de esta variable permite ver si no hay desequilibrio entre las 2 clases que queremos predecir.


<!-- rnb-text-end -->


<!-- rnb-chunk-begin -->


<!-- rnb-source-begin eyJkYXRhIjoiYGBgclxuXG5jbGFzZV9maW5hbCA8LSBkZl90cmFpbiAlPiVcbiAgZ3JvdXBfYnkoZGZfdHJhaW4keSkgJT4lXG4gIGNvdW50KClcblxucGllKHg9Y2xhc2VfZmluYWwkbixcbiAgICBsYWJlbHMgPSBjbGFzZV9maW5hbCRgZGZfdHJhaW4keWAsXG4gICAgcmFkaXVzID0gMSxcbiAgICBtYWluID0gXCJOw7ptZXJvIGRlIGNsaWVudGVzIGVuIGZ1bmNpw7NuIGRlIHNpIGhhbiBzdXNjcml0byBhIHVuIHVuIHRlcm0gZGVwb3NpdFwiLFxuICAgIGNvbCA9IHZpcmlkaXMobGVuZ3RoKGNsYXNlX2ZpbmFsJG4pKSlcblxuYGBgIn0= -->

```r

clase_final <- df_train %>%
  group_by(df_train$y) %>%
  count()

pie(x=clase_final$n,
    labels = clase_final$`df_train$y`,
    radius = 1,
    main = "Número de clientes en función de si han suscrito a un un term deposit",
    col = viridis(length(clase_final$n)))

```

<!-- rnb-source-end -->

<!-- rnb-plot-begin eyJoZWlnaHQiOjQzMi42MzI5LCJ3aWR0aCI6NzAwLCJzaXplX2JlaGF2aW9yIjowLCJjb25kaXRpb25zIjpbXX0= -->

<img src="data:image/png;base64,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" />

<!-- rnb-plot-end -->

<!-- rnb-chunk-end -->


<!-- rnb-text-begin -->

Se puede observar que hay un pequeño desequilibrio entre las clases pero no demasiado importante.

Para concluir sobre esta parte de visualización, se puede decir que hay muchos datos (más de 47 000), y además son datos muy completos que representan muchos tipos de clientes diferentes. Por lo tanto, es un buen conjunto de datos para entrenar modelos predictivos.

### 3) Aprendizaje supervisado : entrenamiento de un algoritmo de regresión

Ahora se van a aplicar técnicas de regresión aprendidas en clase para hacer predicciones.
Más precisamente, lo que se va a hacer es intentar predecir el saldo anual medio de un cliente a partir de las otras variables.

#### 3.1) Preprocesamiento

Se ha visto en la parte de visualización que hay outliers en los valores del saldo anual medio. Por lo tanto, se van a eliminar los clientes con un saldo anual medio superior a 15 000, ya que pueden impedir que el modelo se ajuste a los datos correctamente.


<!-- rnb-text-end -->


<!-- rnb-chunk-begin -->


<!-- rnb-source-begin eyJkYXRhIjoiYGBgclxuZGF0b3Nfc2luX291dGxpZXJzIDwtIGRmX3RyYWluICU+JVxuICBmaWx0ZXIoYmFsYW5jZSA8IDE1MDAwKVxuYGBgIn0= -->

```r
datos_sin_outliers <- df_train %>%
  filter(balance < 15000)
```

<!-- rnb-source-end -->

<!-- rnb-chunk-end -->


<!-- rnb-text-begin -->


#### 3.2) Regresion lineal simple

Primero se verificará si es posible predecir el saldo anual medio con solamente una variable que es la variable edad. Se puede suponer que es dificil hacer eso pero al menos se puede ver si hay una tendencia que hace que las personas mayores tienen un saldo anual más alto, por ejemplo.

Para empezar se pone en un gráfico el saldo anual en función de la edad.


<!-- rnb-text-end -->


<!-- rnb-chunk-begin -->


<!-- rnb-source-begin eyJkYXRhIjoiYGBgclxucGxvdCh4ID0gZGF0b3Nfc2luX291dGxpZXJzJGFnZSxcbiAgICAgeSA9IGRhdG9zX3Npbl9vdXRsaWVycyRiYWxhbmNlLFxuICAgICBtYWluID0gXCJzYWxkbyBhbnVhbCBtZWRpbyBlbiBmdW5jacOzbiBkZSBsYSBlZGFkXCIsXG4gICAgIHhsYWI9XCJlZGFkXCIsXG4gICAgIHlsYWI9XCJzYWxkbyBhbnVhbCBtZWRpb1wiLFxuICAgICB5bGltPWMoLTUwMDAsIDE1MDAwKSlcbmBgYCJ9 -->

```r
plot(x = datos_sin_outliers$age,
     y = datos_sin_outliers$balance,
     main = "saldo anual medio en función de la edad",
     xlab="edad",
     ylab="saldo anual medio",
     ylim=c(-5000, 15000))
```

<!-- rnb-source-end -->

<!-- rnb-plot-begin eyJoZWlnaHQiOjQzMi42MzI5LCJ3aWR0aCI6NzAwLCJzaXplX2JlaGF2aW9yIjowLCJjb25kaXRpb25zIjpbXX0= -->

<img src="data:image/png;base64,iVBORw0KGgoAAAANSUhEUgAAArwAAAGwCAMAAAB8TkaXAAAAqFBMVEUAAAAAADoAAGYAOjoAOmYAOpAAZpAAZrY6AAA6ADo6AGY6OgA6OmY6ZpA6ZrY6kLY6kNtmAABmADpmOgBmOjpmkLZmkNtmtttmtv+QOgCQZgCQZjqQkGaQkLaQttuQtv+Q29uQ2/+2ZgC2Zjq2kDq2kGa225C227a229u22/+2/7a2///bkDrbkGbbtmbbtpDb27bb////tmb/25D/27b//7b//9v////XeMuCAAAACXBIWXMAAA7DAAAOwwHHb6hkAAAgAElEQVR4nO2dCZccOXadwZ5uk/Isbkr2TFOSZbPGi8Zd0ojFIfH//5kzM7C8++ICgViQGah69xxWMiOwBfDFwwWiKtN5k2lQuUc3wGTaKoPXNKwMXtOwMnhNw8rgNQ0rg9c0rAxe07AyeE3DyuA1DSuD1zSsDF7TsDJ4TcPK4B1Qz+7dL49uwxn0uuD9/sn99CW+eXI//HpkeYu6Vrgux1TJnz8494cVjfn20dXZZVfe2rBCrx3QmcfL4G0ub1Eb4X1xF/28ojEvS6kN3hH1eHg3VHIxAZ83ZFvZEIP3TPq33zr37vd/uf73r/9wiV2/+5xG6DoR//gvob//+l+d+81/y+OWEl+p+Z9/du7H6/+nxJcJ+WdSnr+def/X37p3f/L/9mHKcanl0oA/fJn+GyuMOXStObGs1d9qvujdZ9kATPLvlwv9zZ9yY3LRuii8ctE+n3Lnq9ftgrwiGXTmuTQsvM/upmuXvkz/vcSvaYQuP/PJkC5FnZw4nrr9X7Kjy7vqcmbSb2PB4ciPv3pZYcihaxWJZa1XUXhFkqfp/z/7edG6KLhyUWU4dcnyojLwi5DJoDNPplHhvUbCL/7fw6D+py/+64c0vpeuf//lGlIu/X05fDnynEylSHw9+uNfwjnBzqy8UN/l/aU+96ec4y+hIFHhlEPXKhPLWm96nt09Msml7P/y5W8fadGzouSViyrDhf/0RV69bhdeREomizybRoX30rM//mt++x//+xIR3wfYEgfTEF47HWa9kPg66r/cSnqvbIMq76rLmcv/pp+3UQ1Jn3Ml3zJhulaZWNZ6E4VXNez59//q50XPihINkVVelS4lXr1ul+w1kUwdPpVGhXeazSbr9/2fpontfQovt7GRFjQvinLicPAaw5EdVd4t25Rq+nmD9/Ijzq2zCme1isRQ600M3pRErLPmReuiZENklSm3vHrVLpkXeyAfPptGhdf/7R+mXv8fN45//O//kYY6DubTFH9u/39xYWtUJCbwRq8A5d3yzeANtvA67rJCaEGqVSSuwxudhYQ3ppsXrYuSDZFVptzy6lW71EXEZPJwj2HcpWHhveD7z7+9LVymAc9xKhJHI69IXIJXl3fLxyJvfFIwq5DVmh4rrIZ3VeRNDZFVpnPy6lW7VF7dAwbv4fr+j1OM+cXLBVbN84rEMPbT/1/cFFOxvKtm8Ar6mjxvSlyAVzSA3FUvv/sX6nlVUeh5U5W3rrrmllev2yXyymTmeY/XbRF+9Q63cPLTl799yh51WiA/0d0GkVjBe0lxPf6zn5V31Qzey6i++5P/20dVYXG3ISUuwpsaAEkuZf/hNt3/wnYbVFHyykWVV8XIm65et0vklclkkWfTqPD6PydHl3YiE2xPYmtS7biKxDD2aenyMynPM3jDFqnci13c580hdgavaAAmeVKNgX1eVZS8ctk+LzyvXLCVLyInk515Mg0L7+3Bk/vd9QnbdW384788Z3S+/68P7jd/kk/Y/piy5cQ49l8vC8Df/9+02wDleQav/9s/XXibHvHlCuExWK5VJC7AKxuASW5P2P6onrD90bOi4MpF+7zcbQhXr9sl88pk0Jnn0rjwmt68DF7TsFoHbzRDJ5xCTG9Pq+B9jqvnxd8oNZn6aw283z8lZJ/X/sa1yXS41sD77WN6ZvNixsH0cFnkNQ2rlZ43hF7zvKYTaN1uQ/x7Aou7phPI9nlNw8rgNQ0re0hhGlYHP6RwJtNu9YC3YavMXIhpt7rA2/CQwuA17ZZFXtOw6gJvw0MKg9e0W33gXX5IYfCadqsTvPcuzvQWZfCahlUneBcfUgwJ74qdRdMd1GvBtviQYk1xh4tRuEym85V2dwTb7pmC3uRWGXs6UyUzpSimWc6+WR2LHlx3fkix/sleB90qVy2okqmSkNY3ZN+qjkWPrrEjb/tNIFMyHFbAGyPhUpEHyeAtauiHFO0TKgC3Ed5QSGJYzh8G7yM08kOK9mG9oZaAY7ah6UaQ6KtCePZD7JF53pJG3uddAW+IugE4arpbQYvwqspDdiiFGYwNst2Ggl49vCFapohbW3KtsSAxmFdK0SaZNKytQoOXq9Nuw9XpvnR/SNEAXCBNxj+aoxBIeZm3+6HkPXIphRjd0HYav01a/eC97TOITbPtxVUatRSTEj8u/JsDRxdxNWDi/UDMRxO8xUWjqoGWebDGDurd4A3YPvghhVpdlZ9OaOyYJ8AiWRJ9C7icRt0XNSTpLUBTznKuZHF9UD8V7d3g/frhBu+D/5JCk8bZnRlTHqKxSB7FZSnxXmGBtGZT0JqvgHcti+uD+rkszKuIvJVwEHq73OmU65bIy/kuQ6gOKszlO5WkGZjVLPbP0Fed4L2GnPc+Lt12Frek6uiyLSw87+cQpoP0N3j8RFaZb5GwbHYrD+iUs1i5ideU9k4Z+qoLvP7G77vPlY8qO7ADGjCq5Vbwyq01fVvIG6HiRHLD8k9fmgSoNVjrF2h9jTn6+oyu6gXvHYurGdTlsKXQD0HPiZyaPnxXG/94rhxydZCttGzv72zyHN1XeD31GuCtFRj3F4ruAZkK7/RDDVJPSlIL+6FuXwHUp5OzQtTN0vC7eP33Al7/bsN9i6stndIemS9P2XJLwOXjMvKSaby6dYwNya0swsuf+cn7oqGiN6fXAG/lQS2CU7AIYjNWJWRgx8yM71nTJPQsulKzS8/pik4VAh+kLvDG3ylz5QfER/Z8hQr1EqPXLJI6RVh8gacMMHFHeDG0q0bgQ4ry1gV9x+Hlc8jbVJ/I+/3T0sdDHtrxdM7NJ5yjhIrw6mcRFB1wyCb9M3pe7glqYLO2q1IQZXolb1udbMP3T+/rCXr3uwIuOgQvAQjyRcKQTIW+y3F1YTW2eaMW9yUcu9fetHp53hdX+I2cbcWtV4SR7M3Oo7LjhCHYdQtCfHeBsOaNYZaPb+Kt16twzr3gvXNxUHR5XBSFIpTxyMs8Mt8jW85eS1k/BxtuEPA363U451cBL+BaHZcUbp3LbIkXGqllmwsPMPjzNvAsopCF6KqPeXnHRauzK2a+Euf8GuAFXGswpgwSXjStWJbAOxWS8RcUFZzzbFejYDBmVzRfxanr2hczDd771NtalJrOKYwqQ5yB5xsLOsxhdcltiKUg5KPti+/UDaHSyslDXZ5s0k7sDN771NtaVDYE6Q0xBZgh7zZkCOEO4PDq3KJydm0r4MVZAAN3utMOgNc8733qbS1K7wIwGFUGgZGa/iEq66ayWKvrQZcir7dmG7g1iC/a6+zqROamhtMrgFcvpCQ/EF6dyiAwUnERX2b1zX2GWpupiEYsbPFCyHSB9QXTUiyEV/sq9Rrgha0BDSPCKwOOTJmDMhrnSpSECB/jImuDzlg7JcnkXie+WSZzcE/QoFcBby5SRz01/7P4CLaWWxBenfTXhZhZyrhwCXyXYvrZjORuZ3F+vSJ4mY/DlZde7WRnIcuQzpJG3uwqStCrfK0GU1lm5BTAbpDBuyHhQ4orVsM8LAyrGuMYmyFEqzJ9cVLnnhfLrLUWS1GcrrSwBu+GhA8prlgN2AbmGzmEKliSFZdKqUyEjLz11R+0tmqZ166/zPOuT/iQ4orVgFHQiyw/86c6DouEHpPoWEtMBM9QbW4okrmO9SyupX04vXZ4k3PNICezO6VgCy9o5IxvsiXAk2AbIElDa/NRRrTp1cOrAiPdIQB7y4MscAOOtGAioJQW2yDtBqbUB199PG3Xa4cXd3ajAfYiaIZUuNBXePs5THAdykRoz5tsd5ndUHCojllmqGEc9bzXXj2880qRg4odVkxhIbLMnDJWQGwD3he5TfOQi2EcG1jdvTthVO56r71eeMlAsjkej9HfUaCxVtdTC9WiOj2cNOSyW4f7YSjlhFFZd1aP0o9M+IDi2L4WG0gd2dJrRgT9aXYZMtZK48xNMhLGgrPKAC/qTlALRBJ5dfbzyOBtKWs21ataxIbDLPjJiTsciSekRxbpXakeThipQaQXtLM7IR0Mtj23z6uUBu/uhHcvjkYvCpUKmuAs4qIq/ldIJYwVoMHIxRSGrBj2RXRlFemDQ0Ve87xNRVXh5aRlon2CNzrLxG0pICqDMW8SOzYLpOquinVWSqnV15WUjbLdhoaiNLUIHATUeb68owDv6sHSp5NkacgOhR/oleHWUYXRNSeJvHQqeQN6BfBqz6ugm1LIgApN0JEa/KnMoAJ2NsQMppi0OOGrG4LdJfRKThldH6XXAK/aZmDwViIvcxQprDJ448qJnsN2YTb5rmBr4CA3LbWb5Y3pVcA7L1iv0Vnk9fmtwJRaUdJgilY91tYir2wLJqGmZWWnvFJ1gvf7p2kw+n6JYLngFEnBTDbAq+I2vmA9DjYIAHoIzukGguvGeBrvBGhePmXwUvWB9zl+F0Xfb30vF5yZDG9I5BV8+5zCs3jK6oEoGY1wLDgULwtDV61tDcR9OFgwwvW2vQ26u8D7/VNC9v5fIgioaJQhFELkBddZj28htxfwqupiMqAvWhFSspoS5NGZc16Gd/nOeyXqAq/40tYHfImgZAtNRPIGXgRGFaJDemwjWgMnIjZ6giq81D34nEMzSY1Jg214O85imMi7ciqkNkCF12w0M2jAsGysS9RCyoRyqDT9FKhDYfwRGYu8tBEGr1AvzxtC72Ged/VUCMAlkjxYCoEdLvDUciokAe+BwpVaCu14LhYTqmD7EnjQi4yFx9GFKzd4tyW8KX4rRSHuru7bNQMCczx7mc/qC8upkF6UPoOX18OQZERzP6yg9yLSV2ei1Tf6qOoE79HFFeBlI8ipgFkZDwoceSF0Q0J5Dwi5uhQgWloEYHp+lewOouxXu6WC+eAaGl42gnyyjYjFwxAY46GMpYrD0QX4TE8mfiq5Fr8hrGIYrxkFdV14z1RSkg55pfR2gvfwhxTLnNKDhTg3TxnfRMImruGddgpwMNQGpeC+BIZOrKEQefNFeF0KT0m0AvPh1AfeDg8pyORXn3rDJC2yqojI4NWEwUG2pqulxOBM533FMPMZKnCrC1rut+aU46kLvHd6SKHGBQFQU70Xk7tGRZSlfS2LdmAwfEYxn6NTPI28/OZiPgPrazcDBu+ahP5+DylgBPVTAycWWYiYjsOiLEVtZD4AA5ymjMAbGgUsxUsPAk3BMmvn1K2ztpNmJ4dezI0ceRV9zqehxpnfZaK99wV40WZg7hq8AJP2CzLI0jbgzQJ9M4NXZqc90NBJ+hSUNZy6wNvhIcWyVPQCfnQ4nlKSoeO2AbyHggnvDpUvsTvzGdzzwpWoZmIGkXR7VxYsxTDhuA+8hz+kaBCPvGAbNDjzhujIm+JvGSZ50EHdmmEvnAWirB5nQA0qYuNVkkuQF1PuZRrGc6Fj0NsJ3nsX573HmET50XE4Z0uFMNtQm7+5C2DQpxcMnaGR4ZQXuCLKdMe6Cm8NwvLtu3BDnEqvAl6IV3ECl+EOYUxNyNykbNw2YG6acmpHxWeoOMxvAQBb9pSK5niOd0rDOca3wXvXv6RQE7GXuDLEIF/DvM9NRwyW6R6Rpch8CmUIsjRi656CO0hdgi92ZRPYs9oM3v5/SSE7neOQwyr4AAEH0CA8RPagGIBpyEWilSFBX8vDMbQWYnuaQ+QVaFwJffGM+Lnm3Fv3vN23yqB/NQfTCzKyEl7uNiDkqp0LpIgRpjZ/Y3AOuWXR9GAtWDZ00opz7TU8Wl3gLT+kmBG0SRg4eBADODS8ENI8BGxSCA/m8DJr4Rxl7RA8CbK8BozKK7qpknwYQGsaMvIqeDE00Xkc4YV5HOf2WCLAixM+zN86IBIoUsNy8wq3sA7q2Ijd9/yrUxd4ez+kUOEuh9M8ytpvzpjR/CC8SDkGRFWBF1N8wS+E1kJ05fBi+zyYiMeye8Ybpw+8vR9SMEYQv3yGUAunZHu0r0WG1YQvK+cmAoMz8yf6shyJ9OiDHqSqSX6UtsD79cOlH999vk+9hewQB8r8IIXaD8vAG39iePTRQ8gATCjilYeflGEaeWMpsqIa7X1Eguwda1+hDfBOViA5g871NpalF0Sa6HJIi2VIJClFqZ618FL3wODFGgrwdp+/WZB9LfDG1VhpKRYSTYNzj4cUanQDFGr+93MLITLEsz6hhdm8uB8wpWyE06XEMzKax/TKfKTDblYYXFD/+btgaMjBh2s9vHEfrPSbulf1e0hRmdJgyFMcBlrFTydDWp7GARiZT9tovYACsBV9HrBDlMktoNZ0/IboJl5D9Z7pPhmU6l2dsCHy9tsqU31IA9x0IhxEChFGEfwgHGfToQ7mosUZOXK88nhQ1JrghVsgtcXnYvWts6f3igqV1W6PCqDdJ4NaxSsTLnvebn9JoTqWzaQFfpy0j5JQBS9UoCMv3B3xVGyHiKeInTLcsWG5efm+gLarVSPtgQ1dSCDEflzL4uMsxQZ4l3cbukVexVb8SYJfCnD4TtIE6QvwwingTbPoErY5ZrKUmkyEFzCP+WTk3RvmWHZ1v691AWPBu6xeDykK8M7S6FCobYAOdxpJFUgBbI0k4U2XSRkm8FLPi5F3NVq1DsSD6/1Cpcy7qA+8hzykYL3GHIJOGYbbT/x4OecyeIHrtMaa3ih4kakykqlMqBNcrnbO4VLc3BbTrbmtqk1W9ViwUOgj2O0F7wHF8S4BTismDcOkjrxeEu1FlNTYiTJm7xi8quSEabYuVXgx7mM0pz2wVqotzf24UOqeJu3QSni/ffw5BtXyHu4h9bb3WuGpgQyTzZ7X5+Rzh6CsgUuRVCOdWgcZ8Abinjf8BHi5590ITOyIXF3qR1rm4zxBg04bedsdmA5N8qBe8AtWErxIXy1b/CdZVGYA4ZX5NJKQAq8EbjVt4kOjW/qQ9qsspSF5c8oHaDB4WdyhKeszvs/4VXHFbNSDguvQ55xLwTb5hZBLuZV4VPgMjMMq0rd1Ykkrsqu7xBVj9APcw2rbkMeybBsaUi3Xyx0YBqPpII28LNYKwmL8mXEKx+AdulWMvNQhKKOAhcG5BKiXk3o4EjGHBjZ24prOLSWVXQtN2l7mQdoQeaftr5f6Ru+SIW6ol9zIdOgKnjcXIVhMwWtuVz2w4WSQFeyKoryY21OwlBmwfdwowN2ow2q6xbzOvgZe0o9bo6SeE8i5DaVu1np4v396f3td+MWc9wfVS3LpzmNeQuHAgp+4EzKuitBQnURZs+ghYsuX2BJWgz4H14UhlxmaFWHuyIA4PLwtv5hzDc/135hsv0iJZCHuODHnFqbsGZROUigD6hyROezzSIjZoX00qKf2YVPgHL/xPBiT5e5b2d0thWE7e1S0pjlrEsZnv0+1yHtsvTnG0riTj4mwBRnm7OagCaYVHYIizImTXmMe0nsRLGttKFgRKKXY+DVT/rFMwZygh+HAetpbszLhFFSf9/0pRWu9NIjpcOzJ1IuRF87xeRxYAu9aIMxlQmfxNKepR1C93mNtwYNwX4g+KHXowQERrkgVXW5EJ22Ad9pM2BV3N8MboZIlKDJzQqCxaCFiQppiIZuGMLYoFupFgJqbFdHMGt/sRfeSq9N7MFQ6TjxKW+C9Z70qkE7vakSr6FoKsiS0cTAJvVAkug4VmTAJlIlFY6NjEko0AbXuJcpcb5XBuyKhdllVL6EYDqB6GfwYDu3wxoNTrbHkUE/46eHOYaWoNtAXTOgEyso4tXTpkQzjoDxMG23DT1+eCr/reHS9EHL1u5hAAEqDH/VqNc+LaFVDYPxBWMTqXKo05cirzNiEclswxMfKRE/Uu3QFaKHkGu0NSe6gDfC+vPv8/NOXbx930bvyotXwOHwjGYkHZwMvrGVMIX9itPMp+YK/ULFW1e3nwbnGoi6TVgRFx4uV71o6sIYdD6sP5pRqPbzXrbLrA4rnvr9VxpLzvtcOzEEolGNdeAcwVYBBooE+Dm8t7KubZWp7+D+Dd3498v5Nh1jfzSerWhzW3bmY4XFaD+/1IcUV3vpDisPqFenneQQDeQb2Ms6Be0Am63RoVIBIGWuxAj/3rqmtmMHndmZg5DlaO4d3OZCqeUll1+ln8LYYk0L1HSP29sh7p4cUKQPphDjBuRRchDUg1Gr8lnH1xPPykr2c/iGJuAIBPYu8HF52CQ1GATra4d1/P3i7RuzNnvcEn5iDQ679gi+H1pBPHtEpkCJaFjmo5ug4cqFKaB8NwPRmYS1LRsEtEYxuSh8s5XC+nfam2rtoA7zTQ4rHflaZKCMOYvILftEQ1OAok6nOsXCMEKKtiY3O6aXXcaK0hpkhFb3YlRyfaj4n7rWmDGtrP0pb4L1rvYtlOPXSAO/cknJXrN9Btkifm5sIZWSAN4o5mQsWL0D0wGIvEce11oquzpAqN3iLhcwAUBHRe0K0fLfaFdMgC01RYMdsXqBc3bqIjcZLkG2HXlwyDpuwO0hn87zx7yTuuttQKEXEMs0pvhD8GqRKxnNwEFOqDJ4gmbPNgno1DgfoZS8+kM1luY63znp4v3/a+Ts56+qtlyKNX+AkDHEzoDWx26LmVjV9HpBkLWLOmd5xqlrRjcfB4TqC1kPr4RUfRHaPepcKybgEeBhbNRvQQrlnSzTvJWL6DQv4ResybxG3Mtl0pC44hDcng8A42hJ59/1WQ3O9i+OCUQinbOUwG+SbYfLS5S6v1HhFKsh6EdSjHaLUxiRHKl6K7M4RtMHzfv27fbtkjfUux4EqvAhAFaPlZOFHSi8rkNk1fYtFq6ak/3tfgBc97zHSPTeMtsD7YerGO31ijmOBxsX4JjCKBnUaXRX8fDNGCikRxSFYakDlS24kFAYQ8nNYdDgVrsTnvthBWChC9uobgnfxD4OPqRfBISdd9SXZTr+JWkFvRisWiUzp9HIucOJ2EpjOV3jAsEqCpbT1XrVbc181dPWxkvfMAaWtTninBVstHOiQG1KSQW6nVDG1nJKRmSZ1J1ZAFNCWdWLVFu/pdt2rqa2Hu2lS/YFVbIm891mwVVYRNbNbh8OXgKbwpoNecKMDqZ/bE+UzVFM8+AzktMawbNJW0AohoTu1UPvB5a1KeKcFm/K188wzeGtQlVWJ1Gg+ZxmlpZidKmdjGeotlLdOLKStD3m35xnivno8vHf6iFOZsOR58R2M7gpGfBHCqj/lZTmItZgB3q1oHyuzhT5H4in01W6tLOTx8N65Xt5B4aB8mY35lpVaw3Kqnj+3qq0p3FJUio415GO1Lib0ir5qHoNVNRyZYbm4YxPesTi1ZnY7FmyCpXL49ktIUue8YommM1ZuHZ9IrvZwWjzyc7u7fy29h5rrkeHFuVMPuW9klwLK5/2mskqBm4Pd0JZK0bMeEYfSvhvp7WMWbAV4txW2RUPDCyO43VNKXDk+fh3D9cp9Hl+SrbHV1PPiTAQV1Xpu5+qv1oi+GhpeHnnD4MYEu0CrJfGVe2XWnvlBmiSVtbhO9PPIizDV4MUF2+YI2hLUe6oTvHf54uw0grduVltlfBVHWSlTvt6mVvI13wKFAOzFDIH0QZ8meMH8z/vOFfLBgnNxBDrZ6Tb1gbffF2djGU64uvUOUwDD11g8fDd4guWwWgW0alNu57xIPesP2cMLO8JTU3BEoDs3D8o9tBLetu+k6PfF2ViGWl1tlF+MvA0xk+arVuqcvGegsFp2jKdIZiwpd7Hmm4yC01459+3iMLGiR/e83b44W5fBBrnFfbL0iwlpvq0RtN2TF/LfOkC73HwqvF/qwPDTKeYb4eWeN15df3WB906RV4FTQ3lncK5AhG1or7XKfkO90/VDX662mwk0R+Bdtg20vpN73oY/wOz1xdm6kDDyftkpLtNAIVouMjdEluXnLrypfa2XEGuAvlwPbzTQkC16iXR18RJn2Vl9J4f36acvz+/91w+134w84ouzG5rkZIA7wPrqdw1FYpKdTWnOnkKj7Mo1a6xYRrxY6R7wJY/X3CH4wtHTet7rZ5u+XD8l8r6fVaayT33vDwi5FJ8FcpbiaWxjS4VwlyxnU73ngDCn39a632l41fJNZl/DaaXag7UF3l/81//86+3fHeot5k6TZpWtbmZ3524DlrLa+pb6ZSlYQu+72gvdgqjWd3+th/e6Gvv295/r8O56SLHYJbimaKHpbvLCRK7PLH4uVrOkmvlUizKMBfDSUNjjtMHzXj9V+unnqm3Y9ZBi2TSl/nXdPG+mabfn3byjUKu1eodPCWJXkZTYgZiBwrvbydaau73QDQmf3l8XZJXNhl1bZQ03uTZpR8BxrL/wGycB32jitb2ddY/TncSSFLYZIHs6uXSzVNVnFbcF3kXtekhRh9fBItvJNTMM63oY/RwYflu0hGNPSmuovWXdJs+pbsGQyyEkGfjBdt6ap8qm0laoC7z9Ii9QG4+pkSeDfGJhM+mVlPOpblG4OnAPDXIM5eVcyzWcBt6Wv2Hb9ZCiciPTTjjW+i6qh4Wd1bF448WOcEtutR55ax3vWHBuHZTVSbZoc+Stf5/KrocU5e6iRmzFjN9DpPJ76FZt8khTZ4TeoU523pH6IN4Q0VVzomuDUhq4M3nep10fnLPtSlQ/haGjw8r88OlVnTV8+XJg0mmY/hWneDCYD+nOVI+T0pbGk2Tbr+3wbvoqKxiKDYJ+qo3ng+EtN6wpt2P3pDyI922KkqHq3NmVbpzFaGo+lAeByFCoyDXajf3aDm/1SwSP/0sK0iW1QNXTNvgON0VDmSGJX5pY0rxf7uZEppOhOoTceE6+oLmuxtpwro9RmFe1KeG3jxXbcPxfUrAuOQ6d4aTh9RJsgLDWnZgBAVXnGNiVga0mOUzr4V1ci/X4fV4aKu5NzEHyB7RcTSyxd8jLrCfFDMZThhJFWzXRdXinhm0Z5bXabhsqOv4vKWg4qONAD55AW7fyVD68PC8ibxVeDKSURadKEv2Puxt8pJb5Pkxd4O0deRPKfJTlQJ5QhzSs1gOhx8AM6H7E7nSJSM/JRP1ZNEAAABMjSURBVOtbtdPKivTUBngXF2M9/pKChYo3KXb7qpkeqcVlQsgXcKUrCUAZ+z+/Le42FPbrumgDvE8Ne2TH/yVFGJbFoesJTkf5PTcjOlk+4cO7FAQcibwu/pj3f3ksF9jvoy0Ltsd9GxD3vDAEj1VDGw5ppl5VLXW0E8S6+QzmBa4FeBtqyG/vw+4meO/zPWxsoqrvNnh56AwoHyRfNPG1+Tt1o3PO6+kJZzDleeU7Gs3ZUJay99R6eBu+UGUKzi9uz0MKfT87lyMG321AXIeCV1seP+dU52CdSI0pXS2E5HAu5ZLvqC2ujRRvWR9t8Lwvbin03uC97TMUw/RKeOUoC4fg2SDTg69NrBNV0AtkqiAbEsbzMJ/lNE6xWEVSed6m4T1EW2xD6L/yuu0Kb8B281aZhteTuXOo6HqwQqc4ManXsNMQYr5Y4nTSSWum8vGxkpbi1J63QVd4w+c6bH9Iwe5nHXL9eYJse4uOaHSysF5M6kgm7TK6jZbb5eP7ZJKb4FUDt2a1t0vd4N0bebETtNn156H2IcIJXwN6S6H3cl08L6gV/axdrqL9jvG0XRvgXf64pynFe1/ZV1vZEXzM3q74Cg+6RTMckoner+42UINBhmXdOB6rDfC2fNzTld93n8sP2Fbfxdj3apL2/u2RDJcOQVYvDEKPOeZknQjcMDJNRuHR4XjLgu2+H/fkyJ0/jYoKOG8qHIuucfGlQKZMqdwx8wQu97BzpWGSFTWP5OHaAu9dP+6Jeq6pX98WrqjQDTR0YkK0t6FP40HM7oQfxrlOxRC1QHyU1sPb9HFPh9VLJ7E37Reoch+JHvEyHOfFWnaylGhcV8jw7jy/E/SQnXm3oeHjno6rt7qmeLtKME1vWiKvg2UYdq58SaV46TOAfU37bMTuRO8GeJc/7unAerUDy0Pm3qbZDcIJn8VMngRSVm+B0PHqxbGdCDJg64nYoC3w3r1evet4f1ZOp4pbpXsx2rROJ+BFmw+f4eTLvsrAGrwhJYkmJiQTrWg8eDtPYVKlYL44QA563LM7oTiwBm9KqMfFGFbRNfROfHEiHCOSsVNjIU64ALQNPDhjpKcMn9zz3rNeTS28wyF4U2K+ljpShWToVdWB6ZhwsqmaKUUobEriUkJGbzEqH61B4EVbZkryc/eg0BLJcq9iGZgS5zocLepPHqYTw+sgcMh3Ji7qF6YzOJvPs0lrMKWAFzoo97S3VFvg/frh0vZ3nzvXi2EkHgz965YZ9nqM3oA8Wb7BSwI7pHfgedlLLNjlHlU7Ebs42KUN8E6/bfO8+PcU++qlqw9zD0merAGWWUQnm8oi+aj5oI2YjVx5MXew1sMbP1Gk8xM22pWqt01RXlhfjJmKTH7be8E+mmReQy6ZsOvJjNlH6+GNf5a26SNO2+vFyEu3G01RdLdhOoMRVPdjzA/rvXAEh4G80Oha8MpddNrIi3cwHyWTupm9WKLpx8PTQZXbAfRuvgzTDhgqKg/sWeG9k+dVC1sLuVRIJntXzz71M2M4D0JKOqt2vMh7r92GmG55CN6iuENw6ahMym57D0YhFOJJWIWitRVhA9nF8zoa57fAe4Sa4a2tMArj+gaCMzdV6STc716u4uBcbXbDBZu6PZjBEENW3m2gBxsoYPWMAC8fu7cejmHixu0COsXz7IF9ahviuWkUANeCNXAVavOobwCp5EFWwps+ccRVP+K0tbiGdLrX30BYbRHCy2OtW7zDkfbQ4fSlkkQOad0vbDXCB8F71bRge9lnemm9bn7PqpGwkBvlhWldfU978VMc9NKKiBFxGlfGKcZoOqaPhzd+0N7xW2Xsnp0PmYVeofabmVkDhB7nfb3F5uUKjzkEpJ2O6VZ4j/O83R5SpEuDPjRV5Re7aOpVvWDzYm1GOx45VZtj1cgrC1NFb/S8JR+9JfJODymejo68dE5SAyF+vm1xG+Ulyiwq82UYhtWY0Il1G7cUOJJgYTCljtgHaZPnvYbe58M9byFG1AbrDcvL0KkCMDmISHLMK1G5fbdB+xOa8iBtgHfactgVd2ueV68UnFFLxC2sTiGOKpj0Kfk2JGl4cbA2g1GkAfhgbYG3W71O2CRbm+2UjoSyVxNTbr4oqwYPyB7y1UZRW+ZjdSp486ni9g89aMJu8QlTPY2rZVjNfADYeokWssfaQlXwf9mI7Su1qk4IL0YM6EpzD1zUNuTedBq7dMrPo2vK4GShMXSS7KqiOL5OxNpzRN47PmGLAVgMxZHj/arEegfDo8YHzqmMDu4EL6Iy3RxLJXpAuZwSG7FDp4281f41RXky4Ycz8adMIroY5jWPtJbWZiqeKn+C4+rkKFaWdguc1Pg+IbyiO7OvUr1tkir0jieeQHRxTiKK0WszaouxFL1Em42z45wWwjHLvh6iUsLlj/VfVdzsDMxQ5nIbpNdf4aibT/8qJVtXKL+GhcWxc7mubPBkDTDMM9Mizy1TUkyyAd6mj/VvL46f0Xe+MVxRy7yEZNaia23dFsvyYvUXCYsZ5OjiYNKBXqbkQHh7f6y/htd0jHyOiS7HTZbQzfceaBK1W8zcQw3eBs/bAd6+H+tPA8DRI/laFHqsJaWThjYfK3plzKdo9/M7IaEMw1vxvAurMZl9NUSlhN0/1j/0Tug68wvNUiwCdlUnyzJUDXQYpzhcXqKshjeccIuc8gzVfBs8b++P9cchMB2itFILb50j8ZSe88sMO7mYWzYDZMARjGKoboeomLDbx/pP/asWE6YjVN9DcCQA1/jOCdMmgt6JUDGz8q55hdcG0a6E24uL/ettf+F4TT1Mjs4OtQyDjxFX7C9gsGx5l3I3rvBaINqXcHNxahYyHSraqy0HPazNSBIaaymS6h1b4fWG97pX9rz3F3opvKwrTffWNBjxjfgpksR/MgCncSzGU24MkYfOnvfppy9fP7y/Ot8dYvCaTqEwGBNhaqHHl28+Meh9LZ5qRyIPSgzEy1qIFhJe93mvfwl0/B9gVtYGpvVaMZF5YW8x1mp4K/kw5DKXm4K6l/Cu2EZbhmgh4RXepwu4z8f/9XB7b5tWyy9HBi9cQDwE75w4qm0x7j3Q/QX98I5zsAuipYRP7799/OnLt4+H2waDt6d8Gd5qx3uy6TCNVzE9xFzhAg4LuWWIlhJ+++jefY4fPXJgvRsGxLRTfoqZ3ntEU6Rw68yHWr7B+gvr269OW2XfP03XU7QWBu+JpMJq/FcOruJnzgCWGR2wSqIWZW45APMkfeB9dtMHk4TPNWsr7tgBMQF93LuqlPjScK6cpL5Eywy07YoVknSBN36oji9/olmxKXtG662LraPUOXzJCf38YO1dGClf9sPsBSFU5yoqJekCb/w4Mz/7RDOH14g12FbZXrEOjLiG7k8//RxzzO6BzPngFarNY5lxjeEYpv+Twrsx8ppWiy6naAAOXYwsMreqt3vpyMBBFc1lfbhHxhA4Hbz521bWeN5o9VOHmJaUbOPtTXqpHcRzcDCSh++wFPpSKVoM92zIz+l58x9pFn8BghbnxOpzNkwGtFR13b71BYeBDMpRZdKia+JJOsG7v7jZaIEDe+s6bKt0aJ0X3tpq18RM5JvTaeFNG4XTKMVVq2lSjzEZTueFly0fLABH9RiT4XRieGNKuTXIN25et9gNa573qvPDC7kmeN/Ybhpcs9pmeNMaDd4wmi7H4MEZ9uumEgu5QoPBqxbZjuwIvwZ5clWx25yF3Kix4KVxJw6u+HlH9V9ChouM1+8M3qjB4GVDl8Y4/PCtwfgY7kJ1zbXWUlb3tv1kfXd03mvTaPCyouJQ+7VbwX6H58AFVGuOpZQe7gTZvlTfwb03sgaF18kADMNahIL+ukSbQm4WF7lZ4Zyy5oWU6dG3eAieik6VG7yoMeHNSMW3XsGrofIilnlxRG1ZxFM0N1SAgFYNtwK0ci6+hB5y8GBGNmJX770aDQlvhJCUmJ/6Z2L15J4ggFOhSAQGOfVewuclTJT2/ManJ9z6ZgkHUwqvm6kWbOZ5s8aElxYBAOSjzuVzAqZ4UDlLqECwuxSO44uMoCpf7a6KGbzgW9EeGyYu4K3rFcELnOpBzhRpQsNpnwkpwQuF8OAs2zHjFBsdChMt1XE/HIzl+/ls88Y1JrzVgUSG1RmAV0KB6XEaR7ABV0SrEMaBRWxRvh4/u3XwHEwapquGhLdhIGuopEL8fKYXNeS4iCxGdr1wIqIsYWhVPfMGecyHzdRgG7taY8K7PJAcXojYYsqeW0qYv8EFcKMAhpZ6ENpo5Y5FjuR5Cx7JNCy8jeXPIi9ClcARb7zgJkVXL0Knpla+xJLVTaLQlAxzQOUdZPsLRb1WePmQw0FhJr2iCIMlXY3hO10yMcmFhrm4r6BappOY5nq18PIhL0S9eTxF+rzEVcVohziLDLnO+fJNNUv8LMwaprleL7wNyhhpFwD0qb2uFKfl3I7lViIv3ymhU4JpQW8a3quUUUCXmxKB+Vy2ohUWC2Tq9dqJeui8MnjDTyCTzu1rCGs1EeU2naaDTqw3D692AenYQhvbw2N1+VbIYku0Fhm8lJTl2LdibkcTQT2vaYsMXq7l2LdibsegTh2JaYMM3s1qn9ttNdZHBm9/YYy21dhhMni7S8fa8v6waZ0M3hbtAo0bBQvA+2XwNmgfaBRes74HyOBd1l7QGPsG7wEyeKtiv/O1sRR1aG+ZJoO3rvCbDun/hxdt2iODtyL9ew/HFm67DXtl8FaUQq6BdkoZvBU92pjaPVOXwVtT1S90R8ts8YIM3qoqgHZH69Fx//wyeDeqP1oG75IM3o0yeB8vg3ej7oCWed4FGbxbdQe0bLehrk7wfv80/anWD78eUtwpZWg9Wn3gfXY/T/95if/ZVZzJxNQF3u+fErLPP33ZXZzJRNUF3m8ff4n/fSkYB4N3q8ytJFnkHUy2BZHVy/OG0Gue92DZ5q9Qp92Gbx+n3YZC3LXu3yqDV8j2eceSwStk8A4m87xZ9pBiNNluQ5I9pDANK9sqMw0re0hhGlYWeU3Dyh5SmIaVPaQwDSvb5zUNK4PXNKzsIYVpWN35IYVLWlOcycRkW2WmYWUPKUzDyiKvaVjZQwrTsLKHFKZhZfu8pmFl8JqGVafdhqvTfbGHFKau6gfvbZ9BbJptL85kouoGb8DWtspM3dQN3q8fbvAWH1KYTLvVC96FyHt0lZ11oqZYW9ZrHbzX2+K9j0u3O1TZWSdqirVlvVY288Lvu8/lB2w9quypEzXF2rJeD2jmiXrmRE2xtqzXhmaK38+5V5W9dKKmWFvWy+A9i6wtq2XwnkXWltUyeM8ia8tqGbxnkbVltQZppsk0l8FrGlYGr2lYGbymYWXwmoaVwWsaVgavaVgZvKZhZfCahpXBaxpWBq9pWBm8pmFl8JqG1R3hvX0nwO0X0l7c9S/hHqyn2x9An6ApXz9Mf9V6hrY8X4bol5O0ZVn3g/f7p0tvPF+H6eX6N5yP7pqX20ddnqApL5d2fPt4jm55vv117S+naEuD7gfv9HElzz/8Ov0+8NP7u9XM9O3jFd4TNGVqwjm65fun91MTTtCWFt3b815u50TxnasGPf/0jxd4T9CUr38X4tsJ2pLgPUFbWnRveJ9++HUartIHRt1HlzZcPe8JmvLyw//7eFsKnKAtyTacoS0NujO8148rmbzUQx3VdVq8wnuCpjxfPy/2GvJO0Ja0TjtFW5Z1X3hf4nrt0cRcwD0LvO9CkDtBW67z4sUynCK+tOiu8E4fE/X4OenWgpPYhslYXkzmCdqSrO4J2tKie8IbvkDz8auB5/BRmr88vimBkAstZ2hLDLgnaEuL7ghv/CKsk+zDPJ1jq2z6zNiXU2yVTcyeoy0tuuc+b/y4h3PsgD+d5CHFc7yJTtCW6HnP0JYG3Q/eMFdfe+T5DM8ep8fDJ2jKS3xqfoK2PJ2oLcuyX8wxDSuD1zSsDF7TsDJ4TcPK4DUNK4PXNKwMXtOwMnhNw8rgNQ0rg9c0rAxe07AyeE3DyuA1DSuD1zSsDF7TsDJ4TcPK4DUNK4PXNKwMXtOwMnhNw8rgNQ0rg9c0rAxe07AyeE3DyuA1DSuD1zSsDF7TsDJ476r5h9ed/+PsziuD964yeI+UwXtXGbxHyuDtrWf5qaH/fEX1KX7NZDpi2iSDt7OuX5hy+7zm6wc3v1w/9Pb6geO3r1FJR0zbZPD21beP16j78sOv00fmP737/O3vP08foJ+OPLiJ48rg7avJ0l44nb44JTjcl6tvgCOmDTJ4++olfvHQc0L14nR/+D+XqPts8O6UwdtXic0UZ29u4frDIu9eGbx9NX1TlU/fPvfu843Z2xf8xiOPbN/QMng7a9pXuLqF25dST5H328fr7lk88ugmDiuDt7eu+7w3gxB3dW/fEvUUv9LL9nm3y+A1DSuD1zSsDF7TsDJ4TcPK4DUNK4PXNKwMXtOwMnhNw8rgNQ0rg9c0rAxe07AyeE3DyuA1DSuD1zSsDF7TsDJ4TcPK4DUNK4PXNKwMXtOwMnhNw8rgNQ0rg9c0rAxe07AyeE3D6v8DIeyZX57oLUEAAAAASUVORK5CYII=" />

<!-- rnb-plot-end -->

<!-- rnb-chunk-end -->


<!-- rnb-text-begin -->

No se pueden ver muchas cosas con eso. Ahora se va a calcular y dibujar una recta de regresión en el gráfico.


<!-- rnb-text-end -->


<!-- rnb-chunk-begin -->


<!-- rnb-source-begin eyJkYXRhIjoiYGBgclxuIyBDYWxjdWxhbW9zIGxhIHJlZ3Jlc2nDs25cbmxpbmVhbF9zaW1wbGUgPC0gbG0oYmFsYW5jZSB+IGFnZSwgZGF0YSA9IGRhdG9zX3Npbl9vdXRsaWVycylcblxuIyBQb25lbW9zIG90cmEgdmV6IGVsIGdyw6FmaWNvIHBlcm8gY29uIGxhIHJlY3RhIGRlIHJlZ3Jlc2nDs25cbnBsb3QoeCA9IGRhdG9zX3Npbl9vdXRsaWVycyRhZ2UsXG4gICAgIHkgPSBkYXRvc19zaW5fb3V0bGllcnMkYmFsYW5jZSxcbiAgICAgbWFpbiA9IFwic2FsZG8gYW51YWwgbWVkaW8gZW4gZnVuY2nDs24gZGUgbGEgZWRhZFwiLFxuICAgICB4bGFiPVwiZWRhZFwiLFxuICAgICB5bGFiPVwic2FsZG8gYW51YWwgbWVkaW9cIixcbiAgICAgeWxpbT1jKC01MDAwLCAxNTAwMCkpXG5hYmxpbmUobGluZWFsX3NpbXBsZSRjb2VmZmljaWVudHMsIGNvbCA9IFwicmVkXCIpXG5cbmBgYCJ9 -->

```r
# Calculamos la regresión
lineal_simple <- lm(balance ~ age, data = datos_sin_outliers)

# Ponemos otra vez el gráfico pero con la recta de regresión
plot(x = datos_sin_outliers$age,
     y = datos_sin_outliers$balance,
     main = "saldo anual medio en función de la edad",
     xlab="edad",
     ylab="saldo anual medio",
     ylim=c(-5000, 15000))
abline(lineal_simple$coefficients, col = "red")

```

<!-- rnb-source-end -->

<!-- rnb-plot-begin eyJoZWlnaHQiOjQzMi42MzI5LCJ3aWR0aCI6NzAwLCJzaXplX2JlaGF2aW9yIjowLCJjb25kaXRpb25zIjpbXX0= -->

<img src="data:image/png;base64,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" />

<!-- rnb-plot-end -->

<!-- rnb-chunk-end -->


<!-- rnb-text-begin -->

Hay una pequeña pendiente que parece decir que las personas mayores tienen un saldo anual medio un poco más alto. Pero para evaluar la calidad de la regresión se va a calcular una métrica de evaluación : el R_square que es un valor entre 0 (malo) y 1 (bueno).


<!-- rnb-text-end -->


<!-- rnb-chunk-begin -->


<!-- rnb-source-begin eyJkYXRhIjoiYGBgclxuXG4jIFBhcmEgY2FkYSBjbGllbnRlIHNlIGludGVudGEgcHJlZGVjaXIgZWwgc2FsZG8gYW51YWwgbWVkaW8gYSBwYXJ0aXIgZGUgbGEgZWRhZFxuc2FsZG9fYW51YWxfcHJlZGljY2lvbiA8LSBwcmVkaWN0KGxpbmVhbF9zaW1wbGUpXG5cbiMgU2UgY2FsY3VsYSBsYSBkaWZlcmVuY2lhIGNvbiBlbCB2YWxvciByZWFsXG5kaWZlcmVuY2lhIDwtIGRhdG9zX3Npbl9vdXRsaWVycyRiYWxhbmNlIC0gc2FsZG9fYW51YWxfcHJlZGljY2lvblxuXG4jIFNlIGNhbGN1bGEgZWwgdmFsb3IgZGVsIFJfc3F1YXJlXG4jICAgLT4gc2UgY2FsY3VsYSBsYSBzdW1hIGRlIGxvcyByZXNpZHVvcyAoPSB2YXJpYW56YSBkZWwgc2FsZG8gYW51YWwgbWVkaW8gcXVlIG5vIHNlIHB1ZWRlIGV4cGxpY2FyIGNvbiBsYSByZWdyZXNpw7NuKVxuIyAgIC0+IHNlIGNhbGN1bGEgbGEgc3VtYSB0b3RhbCBkZSBsYSB2YXJpYW56YSBkZWwgc2FsZG8gYW51YWwgbWVkaW9cbiMgICAtPiBzZSB1dGlsaXphIGxhIGbDs3JtdWxhIHF1ZSBwZXJtaXRlIGNhbGN1bGFyIGVsIFJfc3F1YXJlICg9IHBvcmNlbnRhamUgZGUgbGEgdmFyaWFuemEgdG90YWwgcXVlIHNlIHB1ZWRlIGV4cGxpY2FyIGNvbiBsYSByZWdyZXNpw7NuKVxuc3VtYV9yZXNpZHVvcyA8LSBzdW0oZGlmZXJlbmNpYV4yKVxuc3VtYV90b3RhbCA8LSBzdW0oKGRhdG9zX3Npbl9vdXRsaWVycyRiYWxhbmNlIC0gbWVhbihkYXRvc19zaW5fb3V0bGllcnMkYmFsYW5jZSkpIF4gMilcbnJfc3F1YXJlIDwtIDEgLSAoc3VtYV9yZXNpZHVvcyAvIHN1bWFfdG90YWwpXG5wcmludChwYXN0ZShcIlJfc3F1YXJlID0gXCIsIHJfc3F1YXJlKSlcbmBgYCJ9 -->

```r

# Para cada cliente se intenta predecir el saldo anual medio a partir de la edad
saldo_anual_prediccion <- predict(lineal_simple)

# Se calcula la diferencia con el valor real
diferencia <- datos_sin_outliers$balance - saldo_anual_prediccion

# Se calcula el valor del R_square
#   -> se calcula la suma de los residuos (= varianza del saldo anual medio que no se puede explicar con la regresión)
#   -> se calcula la suma total de la varianza del saldo anual medio
#   -> se utiliza la fórmula que permite calcular el R_square (= porcentaje de la varianza total que se puede explicar con la regresión)
suma_residuos <- sum(diferencia^2)
suma_total <- sum((datos_sin_outliers$balance - mean(datos_sin_outliers$balance)) ^ 2)
r_square <- 1 - (suma_residuos / suma_total)
print(paste("R_square = ", r_square))
```

<!-- rnb-source-end -->

<!-- rnb-output-begin eyJkYXRhIjoiWzFdIFwiUl9zcXVhcmUgPSAgMC4wMDk4MTg4MjkwMjQ2NzgyM1wiXG4ifQ== -->

```
[1] "R_square =  0.00981882902467823"
```



<!-- rnb-output-end -->

<!-- rnb-chunk-end -->


<!-- rnb-text-begin -->

Se tiene un R_square muy cerca de 0, lo que significa que este modelo de regresión es muy malo y que sólo la edad no es suficiente para predecir el saldo anual medio de un cliente (lo que de hecho parece bastante lógico).

#### 3.3) Regresión multivariable

Ahora se intentará predecir el saldo anual de un cliente pero mirando a todas las otras variables y no sólo la edad.


<!-- rnb-text-end -->


<!-- rnb-chunk-begin -->


<!-- rnb-source-begin eyJkYXRhIjoiYGBgclxuXG4jIFNlIGNvbnN0cnV5ZSBlbCBtb2RlbG8gZGUgcmVncmVzacOzblxubXVsdGl2YXJpYWJsZSA8LSBsbShiYWxhbmNlIH4gLiwgZGF0YSA9IGRhdG9zX3Npbl9vdXRsaWVycylcbiMgU2Ugb2JzZXJ2YW4gdG9kYXMgbGFzIG3DqXRyaWNhc1xuc3VtbWFyeShtdWx0aXZhcmlhYmxlKVxuYGBgIn0= -->

```r

# Se construye el modelo de regresión
multivariable <- lm(balance ~ ., data = datos_sin_outliers)
# Se observan todas las métricas
summary(multivariable)
```

<!-- rnb-source-end -->

<!-- rnb-output-begin eyJkYXRhIjoiXG5DYWxsOlxubG0oZm9ybXVsYSA9IGJhbGFuY2UgfiAuLCBkYXRhID0gZGF0b3Nfc2luX291dGxpZXJzKVxuXG5SZXNpZHVhbHM6XG4gICAgTWluICAgICAgMVEgIE1lZGlhbiAgICAgIDNRICAgICBNYXggXG4tNzA3MS41IC0xMDE1LjMgIC01NTkuMSAgIDIzNi4zIDE0MDA5LjggXG5cbkNvZWZmaWNpZW50czpcbiAgICAgICAgICAgICAgICAgICAgIEVzdGltYXRlIFN0ZC4gRXJyb3IgdCB2YWx1ZSBQcig+fHR8KSAgICBcbihJbnRlcmNlcHQpICAgICAgICAgIDQyOC43MDk3ICAgMTAyLjMxNzUgICA0LjE5MCAyLjc5ZS0wNSAqKipcbmFnZSAgICAgICAgICAgICAgICAgICAxOC4yMzczICAgICAxLjEzMjAgIDE2LjExMSAgPCAyZS0xNiAqKipcbmpvYmJsdWUtY29sbGFyICAgICAgICAzNy4wNDMxICAgIDM1LjM0MzIgICAxLjA0OCAwLjI5NDU5OSAgICBcbmpvYmVudHJlcHJlbmV1ciAgICAgIC02NS41NzEwICAgIDU4Ljk0OTAgIC0xLjExMiAwLjI2NjAwMCAgICBcbmpvYmhvdXNlbWFpZCAgICAgICAgICAgMi41NDU0ICAgIDYzLjg4MjAgICAwLjA0MCAwLjk2ODIxNiAgICBcbmpvYm1hbmFnZW1lbnQgICAgICAgIDE2OS42Mjc0ICAgIDM5LjI2NTggICA0LjMyMCAxLjU2ZS0wNSAqKipcbmpvYnJldGlyZWQgICAgICAgICAgICAzNS44MDgwICAgIDU1LjAzNjUgICAwLjY1MSAwLjUxNTI5MyAgICBcbmpvYnNlbGYtZW1wbG95ZWQgICAgIDE0MC43MDU3ICAgIDU3LjU1OTggICAyLjQ0NSAwLjAxNDUwOSAqICBcbmpvYnNlcnZpY2VzICAgICAgICAgICAtNi4xNTQ2ICAgIDQwLjcwMzggIC0wLjE1MSAwLjg3OTgxNSAgICBcbmpvYnN0dWRlbnQgICAgICAgICAgIDIwOC43MjgwICAgIDcyLjE3ODMgICAyLjg5MiAwLjAwMzgzMiAqKiBcbmpvYnRlY2huaWNpYW4gICAgICAgICA4NC42NTY4ICAgIDM1LjY4MjUgICAyLjM3MyAwLjAxNzY3MiAqICBcbmpvYnVuZW1wbG95ZWQgICAgICAgIDE1MS42NTcyICAgIDYxLjIyNzggICAyLjQ3NyAwLjAxMzI1NSAqICBcbmpvYnVua25vd24gICAgICAgICAgICA4Ni45ODIzICAgMTIxLjEyMzAgICAwLjcxOCAwLjQ3MjY4MCAgICBcbm1hcml0YWxtYXJyaWVkICAgICAgIDI2MC41NDQ0ICAgIDI5Ljg1MTQgICA4LjcyOCAgPCAyZS0xNiAqKipcbm1hcml0YWxzaW5nbGUgICAgICAgIDI5NC44ODExICAgIDM0LjU2MzYgICA4LjUzMiAgPCAyZS0xNiAqKipcbmVkdWNhdGlvbnNlY29uZGFyeSAgICAxNy41NzI5ICAgIDI5LjYxMDYgICAwLjU5MyAwLjU1Mjg3MiAgICBcbmVkdWNhdGlvbnRlcnRpYXJ5ICAgIDIzMi45NDc0ICAgIDM3LjA5MTQgICA2LjI4MCAzLjQxZS0xMCAqKipcbmVkdWNhdGlvbnVua25vd24gICAgIDEwOC4wMDI0ICAgIDUyLjc5MjcgICAyLjA0NiAwLjA0MDc4NCAqICBcbmRlZmF1bHR5ZXMgICAgICAgICAtMTE2Mi41ODU4ICAgIDY5LjE3NDkgLTE2LjgwNiAgPCAyZS0xNiAqKipcbmhvdXNpbmd5ZXMgICAgICAgICAgIC03Ni4xNzg3ICAgIDIyLjM1OTEgIC0zLjQwNyAwLjAwMDY1NyAqKipcbmxvYW55ZXMgICAgICAgICAgICAgLTQyMC44NjM3ICAgIDI1LjY5NTAgLTE2LjM3OSAgPCAyZS0xNiAqKipcbmNvbnRhY3R0ZWxlcGhvbmUgICAgIDE1MS4xMzU3ICAgIDM5LjIzMjggICAzLjg1MiAwLjAwMDExNyAqKipcbmNvbnRhY3R1bmtub3duICAgICAgIC03Ni44NDQ5ICAgIDMxLjcxMzAgIC0yLjQyMyAwLjAxNTM5MSAqICBcbmRheSAgICAgICAgICAgICAgICAgICAgNS43MDg4ICAgICAxLjI3OTcgICA0LjQ2MSA4LjE4ZS0wNiAqKipcbm1vbnRoYXVnICAgICAgICAgICAgLTI2NS42NjYyICAgIDQ2Ljk3MjkgIC01LjY1NiAxLjU2ZS0wOCAqKipcbm1vbnRoZGVjICAgICAgICAgICAgIDIwOS4zOTYwICAgMTM5LjQ1MjUgICAxLjUwMiAwLjEzMzIxOCAgICBcbm1vbnRoZmViICAgICAgICAgICAgLTIzNC43MTc0ICAgIDU1LjAzOTAgIC00LjI2NSAyLjAxZS0wNSAqKipcbm1vbnRoamFuICAgICAgICAgICAgLTU3OC4xMjY4ICAgIDY1LjI4MjMgIC04Ljg1NiAgPCAyZS0xNiAqKipcbm1vbnRoanVsICAgICAgICAgICAgLTQyNS4wMjEyICAgIDQ0Ljg4NDYgIC05LjQ2OSAgPCAyZS0xNiAqKipcbm1vbnRoanVuICAgICAgICAgICAgIDE0Ni45MzU4ICAgIDUzLjMyMDEgICAyLjc1NiAwLjAwNTg1OSAqKiBcbm1vbnRobWFyICAgICAgICAgICAgIDI3NC4wNDEzICAgIDk3Ljc2MDAgICAyLjgwMyAwLjAwNTA2MiAqKiBcbm1vbnRobWF5ICAgICAgICAgICAgLTI1Mi4xMjI0ICAgIDQzLjU3MzkgIC01Ljc4NiA3LjI1ZS0wOSAqKipcbm1vbnRobm92ICAgICAgICAgICAgIDY3MS43MDAxICAgIDQ4LjU2MDkgIDEzLjgzMiAgPCAyZS0xNiAqKipcbm1vbnRob2N0ICAgICAgICAgICAgIDE5Mi4zNjIwICAgIDgyLjI0MDMgICAyLjMzOSAwLjAxOTMzOSAqICBcbm1vbnRoc2VwICAgICAgICAgICAgICA2NC4yMTUzICAgIDkwLjc4NzYgICAwLjcwNyAwLjQ3OTM3NSAgICBcbmR1cmF0aW9uICAgICAgICAgICAgICAgMC4xNzIzICAgICAwLjAzOTQgICA0LjM3MyAxLjIzZS0wNSAqKipcbmNhbXBhaWduICAgICAgICAgICAgICAtNC40NDA1ICAgICAzLjEzMTEgIC0xLjQxOCAwLjE1NjEzNiAgICBcbnBkYXlzICAgICAgICAgICAgICAgICAtMC45MjcxICAgICAwLjE5ODQgIC00LjY3MyAyLjk3ZS0wNiAqKipcbnByZXZpb3VzICAgICAgICAgICAgICAgMy4zODg5ICAgICA0LjcyNzggICAwLjcxNyAwLjQ3MzUwMCAgICBcbnBvdXRjb21lb3RoZXIgICAgICAgIC0yNi43MjA2ICAgIDUzLjc5NTkgIC0wLjQ5NyAwLjYxOTQwMSAgICBcbnBvdXRjb21lc3VjY2VzcyAgICAgICAzOS4yNDQxICAgIDYyLjA1MzYgICAwLjYzMiAwLjUyNzExNCAgICBcbnBvdXRjb21ldW5rbm93biAgICAgLTI3MC41MTg4ICAgIDU5LjM2OTAgIC00LjU1NyA1LjIxZS0wNiAqKipcbnl5ZXMgICAgICAgICAgICAgICAgIDE3NC40ODgxICAgIDM0LjIwOTcgICA1LjEwMSAzLjQwZS0wNyAqKipcbi0tLVxuU2lnbmlmLiBjb2RlczogIDAg4oCYKioq4oCZIDAuMDAxIOKAmCoq4oCZIDAuMDEg4oCYKuKAmSAwLjA1IOKAmC7igJkgMC4xIOKAmCDigJkgMVxuXG5SZXNpZHVhbCBzdGFuZGFyZCBlcnJvcjogMTk0NCBvbiA0NDgxNyBkZWdyZWVzIG9mIGZyZWVkb21cbk11bHRpcGxlIFItc3F1YXJlZDogIDAuMDY3MTksXHRBZGp1c3RlZCBSLXNxdWFyZWQ6ICAwLjA2NjMyIFxuRi1zdGF0aXN0aWM6IDc2Ljg2IG9uIDQyIGFuZCA0NDgxNyBERiwgIHAtdmFsdWU6IDwgMi4yZS0xNlxuIn0= -->

```

Call:
lm(formula = balance ~ ., data = datos_sin_outliers)

Residuals:
    Min      1Q  Median      3Q     Max 
-7071.5 -1015.3  -559.1   236.3 14009.8 

Coefficients:
                     Estimate Std. Error t value Pr(>|t|)    
(Intercept)          428.7097   102.3175   4.190 2.79e-05 ***
age                   18.2373     1.1320  16.111  < 2e-16 ***
jobblue-collar        37.0431    35.3432   1.048 0.294599    
jobentrepreneur      -65.5710    58.9490  -1.112 0.266000    
jobhousemaid           2.5454    63.8820   0.040 0.968216    
jobmanagement        169.6274    39.2658   4.320 1.56e-05 ***
jobretired            35.8080    55.0365   0.651 0.515293    
jobself-employed     140.7057    57.5598   2.445 0.014509 *  
jobservices           -6.1546    40.7038  -0.151 0.879815    
jobstudent           208.7280    72.1783   2.892 0.003832 ** 
jobtechnician         84.6568    35.6825   2.373 0.017672 *  
jobunemployed        151.6572    61.2278   2.477 0.013255 *  
jobunknown            86.9823   121.1230   0.718 0.472680    
maritalmarried       260.5444    29.8514   8.728  < 2e-16 ***
maritalsingle        294.8811    34.5636   8.532  < 2e-16 ***
educationsecondary    17.5729    29.6106   0.593 0.552872    
educationtertiary    232.9474    37.0914   6.280 3.41e-10 ***
educationunknown     108.0024    52.7927   2.046 0.040784 *  
defaultyes         -1162.5858    69.1749 -16.806  < 2e-16 ***
housingyes           -76.1787    22.3591  -3.407 0.000657 ***
loanyes             -420.8637    25.6950 -16.379  < 2e-16 ***
contacttelephone     151.1357    39.2328   3.852 0.000117 ***
contactunknown       -76.8449    31.7130  -2.423 0.015391 *  
day                    5.7088     1.2797   4.461 8.18e-06 ***
monthaug            -265.6662    46.9729  -5.656 1.56e-08 ***
monthdec             209.3960   139.4525   1.502 0.133218    
monthfeb            -234.7174    55.0390  -4.265 2.01e-05 ***
monthjan            -578.1268    65.2823  -8.856  < 2e-16 ***
monthjul            -425.0212    44.8846  -9.469  < 2e-16 ***
monthjun             146.9358    53.3201   2.756 0.005859 ** 
monthmar             274.0413    97.7600   2.803 0.005062 ** 
monthmay            -252.1224    43.5739  -5.786 7.25e-09 ***
monthnov             671.7001    48.5609  13.832  < 2e-16 ***
monthoct             192.3620    82.2403   2.339 0.019339 *  
monthsep              64.2153    90.7876   0.707 0.479375    
duration               0.1723     0.0394   4.373 1.23e-05 ***
campaign              -4.4405     3.1311  -1.418 0.156136    
pdays                 -0.9271     0.1984  -4.673 2.97e-06 ***
previous               3.3889     4.7278   0.717 0.473500    
poutcomeother        -26.7206    53.7959  -0.497 0.619401    
poutcomesuccess       39.2441    62.0536   0.632 0.527114    
poutcomeunknown     -270.5188    59.3690  -4.557 5.21e-06 ***
yyes                 174.4881    34.2097   5.101 3.40e-07 ***
---
Signif. codes:  0 ‘***’ 0.001 ‘**’ 0.01 ‘*’ 0.05 ‘.’ 0.1 ‘ ’ 1

Residual standard error: 1944 on 44817 degrees of freedom
Multiple R-squared:  0.06719,	Adjusted R-squared:  0.06632 
F-statistic: 76.86 on 42 and 44817 DF,  p-value: < 2.2e-16
```



<!-- rnb-output-end -->

<!-- rnb-chunk-end -->


<!-- rnb-text-begin -->

El valor de R_squared es 0.06, lo que significa que solo el 6% de la variación del saldo anual medio se puede explicar con las variables de entrada, lo que significa que el modelo no se ajusta bien a los datos. Puede ser que las otras variables no tienen mucha influencia en el saldo anual medio.


<!-- rnb-text-end -->


<!-- rnb-chunk-begin -->


<!-- rnb-source-begin eyJkYXRhIjoiYGBgclxuIyBBbGd1bm9zIGdyw6FmaWNvcyBwYXJhIHZpc3VhbGl6YXIgdW4gcG9jbyBsb3MgcmVzdWx0YWRvcyBkZSBsYSByZWdyZXNpw7NuXG5wYXIobWZyb3c9YygyLDIpKVxucGxvdChtdWx0aXZhcmlhYmxlKVxuYGBgIn0= -->

```r
# Algunos gráficos para visualizar un poco los resultados de la regresión
par(mfrow=c(2,2))
plot(multivariable)
```

<!-- rnb-source-end -->

<!-- rnb-plot-begin eyJoZWlnaHQiOjQzMi42MzI5LCJ3aWR0aCI6NzAwLCJzaXplX2JlaGF2aW9yIjowLCJjb25kaXRpb25zIjpbXX0= -->

<img src="data:image/png;base64,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" />

<!-- rnb-plot-end -->

<!-- rnb-chunk-end -->


<!-- rnb-text-begin -->

### 4) Aprendizaje supervisado : entrenamiento de clasificadores

Ahora, se van a entrenar varios clasificadores para predecir si el cliente es interesante o no. Se va a probar cada clasificador con el conjunto de test y despues se va a comparar los resultados de cada uno para elegir lo mejor.

#### 4.1) Árbol de decisión

rpart (Rercursive Partitioning And Regression Trees) es una librería que permite entrenar árboles de decisión para hacer predicciones. Se va a utilizar para construir un árbol de decisión que permite predecir el valor de la variable "y" que representa la respuesta del cliente (si o no) para suscribir a un term deposit.


<!-- rnb-text-end -->


<!-- rnb-chunk-begin -->


<!-- rnb-source-begin eyJkYXRhIjoiYGBgclxuXG4jIGRlc2NvbWVudGFyIGxhcyBzaWd1aWVudGVzIGzDrW5lYXMgc2kgeWEgbm8gZXN0w6FuIGluc3RhbGFkb3MgbG9zIHBhY2thZ2VzIFwicmF0dGxlXCIgeSBcInJwYXJ0LnBsb3RcIlxuIyBpbnN0YWxsLnBhY2thZ2VzKFwicmF0dGxlXCIpXG4jIGluc3RhbGwucGFja2FnZXMocnBhcnQucGxvdClcblxuIyBzZSBjb25zdHJ1eWUgZWwgw6FyYm9sXG5saWJyYXJ5KHJwYXJ0KVxuXG5teXRyZWUgPC0gcnBhcnQoXG4gIHkgfiAuLFxuICBkYXRhID0gZGZfdHJhaW4sXG4gIG1ldGhvZCA9IFwiY2xhc3NcIlxuKVxuXG4jIHNlIGltcHJpbWUgZWwgw6FyYm9sIGNvbnN0cnVpZG9cbm15dHJlZVxuYGBgIn0= -->

```r

# descomentar las siguientes líneas si ya no están instalados los packages "rattle" y "rpart.plot"
# install.packages("rattle")
# install.packages(rpart.plot)

# se construye el árbol
library(rpart)

mytree <- rpart(
  y ~ .,
  data = df_train,
  method = "class"
)

# se imprime el árbol construido
mytree
```

<!-- rnb-source-end -->

<!-- rnb-output-begin eyJkYXRhIjoibj0gNDUyMTEgXG5cbm5vZGUpLCBzcGxpdCwgbiwgbG9zcywgeXZhbCwgKHlwcm9iKVxuICAgICAgKiBkZW5vdGVzIHRlcm1pbmFsIG5vZGVcblxuIDEpIHJvb3QgNDUyMTEgNTI4OSBubyAoMC44ODMwMTUyMCAwLjExNjk4NDgwKSAgXG4gICAyKSBkdXJhdGlvbjwgNTIxLjUgNDAyMzggMzEwNiBubyAoMC45MjI4MDkyOCAwLjA3NzE5MDcyKSAgXG4gICAgIDQpIHBvdXRjb21lPWZhaWx1cmUsb3RoZXIsdW5rbm93biAzODk0MSAyMzAxIG5vICgwLjk0MDkxMDYxIDAuMDU5MDg5MzkpICpcbiAgICAgNSkgcG91dGNvbWU9c3VjY2VzcyAxMjk3ICA0OTIgeWVzICgwLjM3OTMzNjkzIDAuNjIwNjYzMDcpICBcbiAgICAgIDEwKSBkdXJhdGlvbjwgMTYyLjUgMzYwICAxMTMgbm8gKDAuNjg2MTExMTEgMC4zMTM4ODg4OSkgKlxuICAgICAgMTEpIGR1cmF0aW9uPj0xNjIuNSA5MzcgIDI0NSB5ZXMgKDAuMjYxNDcyNzkgMC43Mzg1MjcyMSkgKlxuICAgMykgZHVyYXRpb24+PTUyMS41IDQ5NzMgMjE4MyBubyAoMC41NjEwMjk1NiAwLjQzODk3MDQ0KSAgXG4gICAgIDYpIGR1cmF0aW9uPCA4MjcuNSAzMTkxIDExNDcgbm8gKDAuNjQwNTUxNTUgMC4zNTk0NDg0NSkgIFxuICAgICAgMTIpIHBvdXRjb21lPWZhaWx1cmUsb3RoZXIsdW5rbm93biAzMDQ3IDEwMzAgbm8gKDAuNjYxOTYyNTkgMC4zMzgwMzc0MSkgKlxuICAgICAgMTMpIHBvdXRjb21lPXN1Y2Nlc3MgMTQ0ICAgMjcgeWVzICgwLjE4NzUwMDAwIDAuODEyNTAwMDApICpcbiAgICAgNykgZHVyYXRpb24+PTgyNy41IDE3ODIgIDc0NiB5ZXMgKDAuNDE4NjMwNzUgMC41ODEzNjkyNSkgKlxuIn0= -->

```
n= 45211 

node), split, n, loss, yval, (yprob)
      * denotes terminal node

 1) root 45211 5289 no (0.88301520 0.11698480)  
   2) duration< 521.5 40238 3106 no (0.92280928 0.07719072)  
     4) poutcome=failure,other,unknown 38941 2301 no (0.94091061 0.05908939) *
     5) poutcome=success 1297  492 yes (0.37933693 0.62066307)  
      10) duration< 162.5 360  113 no (0.68611111 0.31388889) *
      11) duration>=162.5 937  245 yes (0.26147279 0.73852721) *
   3) duration>=521.5 4973 2183 no (0.56102956 0.43897044)  
     6) duration< 827.5 3191 1147 no (0.64055155 0.35944845)  
      12) poutcome=failure,other,unknown 3047 1030 no (0.66196259 0.33803741) *
      13) poutcome=success 144   27 yes (0.18750000 0.81250000) *
     7) duration>=827.5 1782  746 yes (0.41863075 0.58136925) *
```



<!-- rnb-output-end -->

<!-- rnb-chunk-end -->


<!-- rnb-text-begin -->




<!-- rnb-text-end -->


<!-- rnb-chunk-begin -->


<!-- rnb-source-begin eyJkYXRhIjoiYGBgclxuIyBTZSB0cmF6YSBlbCDDoXJib2wgZGUgZGVjaXNpw7NuXG5saWJyYXJ5KHJwYXJ0LnBsb3QpXG5ycGFydC5wbG90KG15dHJlZSlcbmBgYCJ9 -->

```r
# Se traza el árbol de decisión
library(rpart.plot)
rpart.plot(mytree)
```

<!-- rnb-source-end -->

<!-- rnb-plot-begin eyJoZWlnaHQiOjQzMi42MzI5LCJ3aWR0aCI6NzAwLCJzaXplX2JlaGF2aW9yIjowLCJjb25kaXRpb25zIjpbXX0= -->

<img src="data:image/png;base64,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" />

<!-- rnb-plot-end -->

<!-- rnb-chunk-end -->


<!-- rnb-text-begin -->


Se puede ver que la duración de la llamada y el éxito (o no) de la campaña de marketing anterior tienen mucho impacto en el resultado.


<!-- rnb-text-end -->


<!-- rnb-chunk-begin -->


<!-- rnb-source-begin eyJkYXRhIjoiYGBgclxuIyBTZSBoYWNlbiBwcmVkaWNjaW9uZXMgc29icmUgZGF0b3MgZGUgcHJ1ZWJhXG5wcmVkcyA8LSBwcmVkaWN0KG15dHJlZSwgbmV3ZGF0YSA9IGRmX3Rlc3QsIHR5cGUgPSBcImNsYXNzXCIpXG5gYGAifQ== -->

```r
# Se hacen predicciones sobre datos de prueba
preds <- predict(mytree, newdata = df_test, type = "class")
```

<!-- rnb-source-end -->

<!-- rnb-chunk-end -->


<!-- rnb-text-begin -->



<!-- rnb-text-end -->


<!-- rnb-chunk-begin -->


<!-- rnb-source-begin eyJkYXRhIjoiYGBgclxuI3NlIGNvbXBydWViYSBsYSBwcmVjaXNpw7NuIGRlbCDDoXJib2wgZGUgZGVjaXNpw7NuIGVuIGxvcyBkYXRvcyBkZSBwcnVlYmFcbnByZWNpc2lvbiA9IG1lYW4ocHJlZHMgPT0gZGZfdGVzdCR5KVxucHJpbnQocGFzdGUoXCJFbCDDoXJib2wgY2xhc2lmaWNhIGJpZW4gXCIscHJlY2lzaW9uKjEwMCxcIiUgZGUgbG9zIGRhdG9zLlwiKSlcbmBgYCJ9 -->

```r
#se comprueba la precisión del árbol de decisión en los datos de prueba
precision = mean(preds == df_test$y)
print(paste("El árbol clasifica bien ",precision*100,"% de los datos."))
```

<!-- rnb-source-end -->

<!-- rnb-output-begin eyJkYXRhIjoiWzFdIFwiRWwgw6FyYm9sIGNsYXNpZmljYSBiaWVuICA5MC4wMDIyMTE5MDAwMjIxICUgZGUgbG9zIGRhdG9zLlwiXG4ifQ== -->

```
[1] "El árbol clasifica bien  90.0022119000221 % de los datos."
```



<!-- rnb-output-end -->

<!-- rnb-chunk-end -->


<!-- rnb-text-begin -->

Este resultado parece bueno, pero no significa que el clasificador es bueno : por ejemplo si se tiene 90% de los clientes que dicen "no", un clasificador estúpido que clasifica todos los clientes como clientes que van a decir "no" tiene 90% de precisión, por eso hay que mirar a la matriz de confusión para verificar que el algoritmo funciona bien.


<!-- rnb-text-end -->


<!-- rnb-chunk-begin -->


<!-- rnb-source-begin eyJkYXRhIjoiYGBgclxuIyBNYXRyaXogZGUgY29uZnVzacOzbiBkZWwgw6FyYm9sIGRlIGRlY2lzacOzbiBzb2JyZSBsb3MgZGF0b3MgZGUgcHJ1ZWJhLlxubWF0cml6X2NvbmZ1c2lvbiA9IHRhYmxlKGRmX3Rlc3QkeSwgcHJlZHMpXG5tYXRyaXpfY29uZnVzaW9uXG5gYGAifQ== -->

```r
# Matriz de confusión del árbol de decisión sobre los datos de prueba.
matriz_confusion = table(df_test$y, preds)
matriz_confusion
```

<!-- rnb-source-end -->

<!-- rnb-output-begin eyJkYXRhIjoiICAgICBwcmVkc1xuICAgICAgICBubyAgeWVzXG4gIG5vICAzODk2ICAxMDRcbiAgeWVzICAzNDggIDE3M1xuIn0= -->

```
     preds
        no  yes
  no  3896  104
  yes  348  173
```



<!-- rnb-output-end -->

<!-- rnb-chunk-end -->


<!-- rnb-text-begin -->


Se puede ver que el clasificador no es estúpido y clasifica bastante bien tanto los clientes que dan una respuesta positiva como los que dans una respuesta negativa.

#### 4.2) Clasificador Knn

Ahora se va a utilizar el algoritmo Knn (K-Nearest-Neighbors), visto en clase para hacer la clasificación.

Primero hay que que convertir las variables categóricas en variables numéricas porque con el algoritmo KNN hace falta calcular la distancia entre los datos y para hacer eso se necesitan variables numéricas.


<!-- rnb-text-end -->


<!-- rnb-chunk-begin -->


<!-- rnb-source-begin eyJkYXRhIjoiYGBgclxuIyBjb252ZXJ0aXIgdmFyaWFibGVzIGNhdGVnw7NyaWNhcyBlbiBudW3DqXJpY2FzIHBhcmEgbG9zIGRhdG9zIGRlIGVudHJlbmFtaWVudG9cbiMgaW5zdGFsbC5wYWNrYWdlcyhcImZhc3REdW1taWVzXCIpXG5saWJyYXJ5KGZhc3REdW1taWVzKVxuZGZfdHJhaW5kIDwtIGRmX3RyYWluXG5kZl90cmFpbmQkZGVmYXVsdCA8LSBpZmVsc2UoZGZfdHJhaW5kJGRlZmF1bHQgPT0gXCJ5ZXNcIiwxLDApXG5kZl90cmFpbmQkaG91c2luZyA8LSBpZmVsc2UoZGZfdHJhaW5kJGhvdXNpbmcgPT0gXCJ5ZXNcIiwxLDApXG5kZl90cmFpbmQkbG9hbiA8LSBpZmVsc2UoZGZfdHJhaW5kJGxvYW4gPT0gXCJ5ZXNcIiwxLDApXG5kZl90cmFpbmQkbW9udGggPC0gcmVjb2RlKGRmX3RyYWluZCRtb250aCwgXCJqYW5cIiA9IDEsIFwiZmViXCIgPSAyLCBcIm1hclwiID0gMywgXCJhcHJcIiA9IDQsICBcIm1heVwiID0gNSwgXCJqdW5cIiA9IDYsIFwianVsXCIgPSA3LCBcImF1Z1wiID0gOCwgXCJzZXBcIiA9IDksIFwib2N0XCIgPSAxMCwgXCJub3ZcIiA9IDExLCBcImRlY1wiID0gMTIpXG5kZl90cmFpbmQgPC0gZHVtbXlfY29scyhkZl90cmFpbmQscmVtb3ZlX3NlbGVjdGVkX2NvbHVtbnMgPSBULCBzZWxlY3RfY29sdW1ucyA9IGMoXCJqb2JcIiwgXCJtYXJpdGFsXCIsIFwiZWR1Y2F0aW9uXCIsIFwiY29udGFjdFwiLCBcInBvdXRjb21lXCIpKVxuYGBgIn0= -->

```r
# convertir variables categóricas en numéricas para los datos de entrenamiento
# install.packages("fastDummies")
library(fastDummies)
df_traind <- df_train
df_traind$default <- ifelse(df_traind$default == "yes",1,0)
df_traind$housing <- ifelse(df_traind$housing == "yes",1,0)
df_traind$loan <- ifelse(df_traind$loan == "yes",1,0)
df_traind$month <- recode(df_traind$month, "jan" = 1, "feb" = 2, "mar" = 3, "apr" = 4,  "may" = 5, "jun" = 6, "jul" = 7, "aug" = 8, "sep" = 9, "oct" = 10, "nov" = 11, "dec" = 12)
df_traind <- dummy_cols(df_traind,remove_selected_columns = T, select_columns = c("job", "marital", "education", "contact", "poutcome"))
```

<!-- rnb-source-end -->

<!-- rnb-output-begin eyJkYXRhIjoiUmVnaXN0ZXJlZCBTMyBtZXRob2Qgb3ZlcndyaXR0ZW4gYnkgJ2RhdGEudGFibGUnOlxuICBtZXRob2QgICAgICAgICAgIGZyb21cbiAgcHJpbnQuZGF0YS50YWJsZSAgICAgXG4ifQ== -->

```
Registered S3 method overwritten by 'data.table':
  method           from
  print.data.table     
```



<!-- rnb-output-end -->

<!-- rnb-chunk-end -->


<!-- rnb-text-begin -->




<!-- rnb-text-end -->


<!-- rnb-chunk-begin -->


<!-- rnb-source-begin eyJkYXRhIjoiYGBgclxuI2NvbnZlcnRpciB2YXJpYWJsZXMgY2F0ZWfDs3JpY2FzIGVuIG51bcOpcmljYXMgcGFyYSBkYXRvcyBkZSBwcnVlYmFcbmRmX3Rlc3RkIDwtIGRmX3Rlc3RcbmRmX3Rlc3RkJGRlZmF1bHQgPC0gaWZlbHNlKGRmX3Rlc3RkJGRlZmF1bHQgPT0gXCJ5ZXNcIiwxLDApXG5kZl90ZXN0ZCRob3VzaW5nIDwtIGlmZWxzZShkZl90ZXN0ZCRob3VzaW5nID09IFwieWVzXCIsMSwwKVxuZGZfdGVzdGQkbG9hbiA8LSBpZmVsc2UoZGZfdGVzdGQkbG9hbiA9PSBcInllc1wiLDEsMClcblxuZGZfdGVzdGQkbW9udGggPC0gcmVjb2RlKGRmX3Rlc3RkJG1vbnRoLCBcImphblwiID0gMSwgXCJmZWJcIiA9IDIsIFwibWFyXCIgPSAzLCBcImFwclwiID0gNCwgIFwibWF5XCIgPSA1LCBcImp1blwiID0gNiwgXCJqdWxcIiA9IDcsIFwiYXVnXCIgPSA4LCBcInNlcFwiID0gOSwgXCJvY3RcIiA9IDEwLCBcIm5vdlwiID0gMTEsIFwiZGVjXCIgPSAxMilcblxuZGZfdGVzdGQgPC0gZHVtbXlfY29scyhkZl90ZXN0ZCxyZW1vdmVfc2VsZWN0ZWRfY29sdW1ucyA9IFQsIHNlbGVjdF9jb2x1bW5zID0gYyhcImpvYlwiLCBcIm1hcml0YWxcIiwgXCJlZHVjYXRpb25cIiwgXCJjb250YWN0XCIsIFwicG91dGNvbWVcIikpXG5gYGAifQ== -->

```r
#convertir variables categóricas en numéricas para datos de prueba
df_testd <- df_test
df_testd$default <- ifelse(df_testd$default == "yes",1,0)
df_testd$housing <- ifelse(df_testd$housing == "yes",1,0)
df_testd$loan <- ifelse(df_testd$loan == "yes",1,0)

df_testd$month <- recode(df_testd$month, "jan" = 1, "feb" = 2, "mar" = 3, "apr" = 4,  "may" = 5, "jun" = 6, "jul" = 7, "aug" = 8, "sep" = 9, "oct" = 10, "nov" = 11, "dec" = 12)

df_testd <- dummy_cols(df_testd,remove_selected_columns = T, select_columns = c("job", "marital", "education", "contact", "poutcome"))
```

<!-- rnb-source-end -->

<!-- rnb-chunk-end -->


<!-- rnb-text-begin -->


Ahora se va a aplicar el algoritmo, pero para eso hace falta elegir con qué valor de "k" (= número de vecinos más cercanos) se va a aplicar el algoritmo.

No se puede saber de antemano cuál es el mejor valor para k, por lo tanto se va a aplicar el algoritmo con varios valores de k y elegir el valor que da los mejores resultados. (Como se entrenaron varios clasificadores es normal si la ejecución del siguiente código lleva algunos minutos)


<!-- rnb-text-end -->


<!-- rnb-chunk-begin -->


<!-- rnb-source-begin eyJkYXRhIjoiYGBgclxuIyAjIGRlc2NvbWVudGFyIGxhIHNpZ3VpZW50ZSBsw61uZWEgc2kgeWEgbm8gZXN0w6EgaW5zdGFsYWRvIGVsIHBhY2thZ2UgXCJjbGFzc1wiXG4jIGluc3RhbGwucGFja2FnZXMoXCJjbGFzc1wiKVxubGlicmFyeShjbGFzcylcblxuIyBzZSB2YSBhIGFwbGljYXIgZWwgYWxnb3JpdG1vIGNvbiB2YWxvcmVzIGsgZGUgMiBhIDEwXG5yYW5nZSA8LSAyOjEwXG5hY2NzIDwtIHJlcCgwLCBsZW5ndGgocmFuZ2UpKVxuXG5mb3IgKGsgaW4gcmFuZ2UpIHtcbiAgIyBzZSBlbnRyZW5hIGVsIGNsYXNpZmljYWRvclxuICBjbGFzaWZpY2Fkb3IgPC0ga25uKHRyYWluID0gZGZfdHJhaW5kWywtYygxMildLFxuICAgICAgICAgICAgICAgICAgICAgIHRlc3QgPSBkZl90ZXN0ZFssIC1jKDEyKV0sXG4gICAgICAgICAgICAgICAgICAgICAgY2wgPSBkZl90cmFpbmQkeSwgayA9IGspXG5cbiAgIyBzZSBjYWxjdWxhIGxhIG1hdHJpeiBkZSBjb25mdXNpw7NuXG4gIG1hdHJpel9jb25mdXNpb24gPC0gdGFibGUoZGZfdGVzdGQkeSwgY2xhc2lmaWNhZG9yKVxuXG4gICMgc2UgY2FsY3VsYSBsYSBwcmVjaXNpw7NuXG4gIGFjY3Nbay0xXSA8LSBzdW0oZGlhZyhtYXRyaXpfY29uZnVzaW9uKSkgLyBzdW0obWF0cml6X2NvbmZ1c2lvbilcbn1cblxuIyBTZSB2aXN1YWxpemEgbGEgcHJlY2lzacOzbiBwYXJhIGNhZGEgdmFsb3IgZGUga1xucGxvdChyYW5nZSwgYWNjcywgeGxhYiA9IFwia1wiKVxuYGBgIn0= -->

```r
# # descomentar la siguiente línea si ya no está instalado el package "class"
# install.packages("class")
library(class)

# se va a aplicar el algoritmo con valores k de 2 a 10
range <- 2:10
accs <- rep(0, length(range))

for (k in range) {
  # se entrena el clasificador
  clasificador <- knn(train = df_traind[,-c(12)],
                      test = df_testd[, -c(12)],
                      cl = df_traind$y, k = k)

  # se calcula la matriz de confusión
  matriz_confusion <- table(df_testd$y, clasificador)

  # se calcula la precisión
  accs[k-1] <- sum(diag(matriz_confusion)) / sum(matriz_confusion)
}

# Se visualiza la precisión para cada valor de k
plot(range, accs, xlab = "k")
```

<!-- rnb-source-end -->

<!-- rnb-plot-begin eyJoZWlnaHQiOjQzMi42MzI5LCJ3aWR0aCI6NzAwLCJzaXplX2JlaGF2aW9yIjowLCJjb25kaXRpb25zIjpbXX0= -->

<img src="data:image/png;base64,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" />

<!-- rnb-plot-end -->

<!-- rnb-chunk-end -->


<!-- rnb-text-begin -->

Se ve en el gráfico que hay buenos resultados (precisión superior al 90%) con todos los valores de k, y hay una precisión de más de 92% con k=2 y k=3. Se va a calcular con más detalle la precisión que se obtiene con el mejor k.


<!-- rnb-text-end -->


<!-- rnb-chunk-begin -->


<!-- rnb-source-begin eyJkYXRhIjoiYGBgclxua19iZXN0ID0gd2hpY2gubWF4KGFjY3MpICsgMVxucHJlY2lzaW9uX2Jlc3QgPSBhY2NzW3doaWNoLm1heChhY2NzKV1cbnByaW50KHBhc3RlKFwiRWwgbWVqb3IgbsO6bWVybyBkZSB2ZWNpbm9zIGVzIGsgPVwiLCBrX2Jlc3QsXCJ5IHRlbmVtb3MgdW5hIHByZWNpc2nDs24gZGUgXCIscHJlY2lzaW9uX2Jlc3QqMTAwLFwiJS5cIiApKVxuYGBgIn0= -->

```r
k_best = which.max(accs) + 1
precision_best = accs[which.max(accs)]
print(paste("El mejor número de vecinos es k =", k_best,"y tenemos una precisión de ",precision_best*100,"%." ))
```

<!-- rnb-source-end -->

<!-- rnb-output-begin eyJkYXRhIjoiWzFdIFwiRWwgbWVqb3IgbsO6bWVybyBkZSB2ZWNpbm9zIGVzIGsgPSAyIHkgdGVuZW1vcyB1bmEgcHJlY2lzacOzbiBkZSAgOTMuMDEwMzk1OTMwMTA0ICUuXCJcbiJ9 -->

```
[1] "El mejor número de vecinos es k = 2 y tenemos una precisión de  93.010395930104 %."
```



<!-- rnb-output-end -->

<!-- rnb-chunk-end -->


<!-- rnb-text-begin -->


Dado que el rendimiento del clasificador KNN es más alto que el del árbol de decisión, el clasificador knn se generaliza y se ajusta bien a los datos y funciona mejor que el árbol de decisión y se puede utilizar para predicciones futuras.

### 5) Aplicación de algoritmos de clustering

Para terminar, se van a aplicar varios algoritmos de clustering para ver si el conjunto de clientes se puede dividir en varios subconjuntos con clientes que se parecen, y comparar los resultados de estos algoritmos de clustering.

#### 5.1) Kmeans Clustering

Primero se va a utilizar el algoritmo KMeans visto en clase. No se puede saber de antemano cuál es el número óptimo de clusters, así que se va a intentar hacer el clustering con varios números de clusters (se va a hacerlo para k = 2 a 7) y elegir lo mejor.

Para hacer eso, se va a calcular para cada valor de k el WSS (Within cluster Sum of Square). WWS es una métrica que calcula si los datos que pertenecen a un mismo cluster están cerca, por lo tanto el objetivo es tener un valor lo más pequeño posible para WWS. Cuando se aumenta el número de clusters, el WWS siempre baja, pero no queremos un número de clusters igual que el número de datos, por lo tanto lo que se hace para elegir el número de clusters óptimo es visualizar en un gráfico el valor de WWS para varios valores de k, y elegir el número de cluster que corresponde a un "codo" en el gráfico. En efecto este valor coresponde al nivel en lo que aumentar el número de clusters no aporta mucho.


<!-- rnb-text-end -->


<!-- rnb-chunk-begin -->


<!-- rnb-source-begin eyJkYXRhIjoiYGBgclxuXG4jIFNlIGluaXRpYWxpemEgZWwgV1NTIHF1ZSBzZSB2YSBhIGNhbGN1bGFyXG53c3M8LTBcblxuXG4jIFNlIGFwbGljYSBlbCBhbGdvcmltdG8gcGFyYSBrIGRlIDIgYSA3XG5mb3IoayBpbiAyOjcpe1xuICBzZXQuc2VlZCgxKVxuICBrbSA8LSBrbWVhbnMoZGZfdHJhaW5kWywtYygxMildLCBjZW50ZXJzID0gaywgbnN0YXJ0ID0gMjUpXG4gIHdzc1trLTFdIDwtIGttJHRvdC53aXRoaW5zc1xufVxuYGBgIn0= -->

```r

# Se initializa el WSS que se va a calcular
wss<-0


# Se aplica el algorimto para k de 2 a 7
for(k in 2:7){
  set.seed(1)
  km <- kmeans(df_traind[,-c(12)], centers = k, nstart = 25)
  wss[k-1] <- km$tot.withinss
}
```

<!-- rnb-source-end -->

<!-- rnb-chunk-end -->


<!-- rnb-text-begin -->



<!-- rnb-text-end -->


<!-- rnb-chunk-begin -->


<!-- rnb-source-begin eyJkYXRhIjoiYGBgclxuXG4jIFNlIGNvbnN0cnV5ZSBsYSB2ZW50YW5hIGVuIGxhIHF1ZSBzZSB2YSBhIHZpc3VhbGl6YXIgbG9zIHJlc3VsdGFkb3NcbnBhcihtZnJvdyA9IGMoMSwxKSlcblxuIyBTZSB2aXN1YWxpemEgbG9zIHZhbG9yZXMgZGUgV1dTIHBhcmEgbG9zIGRpc3RpbnRvcyB2YWxvcmVzIGRlIGtcbnBsb3QoMjo3LCB3c3MsIHR5cGUgPSBcImJcIiwgXG4gICAgIHhsYWIgPSBcIk51bWVybyBkZSBjbHVzdGVyc1wiLFxuICAgICB5bGFiID0gXCJXV1NcIilcbmBgYCJ9 -->

```r

# Se construye la ventana en la que se va a visualizar los resultados
par(mfrow = c(1,1))

# Se visualiza los valores de WWS para los distintos valores de k
plot(2:7, wss, type = "b", 
     xlab = "Numero de clusters",
     ylab = "WWS")
```

<!-- rnb-source-end -->

<!-- rnb-plot-begin eyJoZWlnaHQiOjQzMi42MzI5LCJ3aWR0aCI6NzAwLCJzaXplX2JlaGF2aW9yIjowLCJjb25kaXRpb25zIjpbXX0= -->

<img src="data:image/png;base64,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" />

<!-- rnb-plot-end -->

<!-- rnb-chunk-end -->


<!-- rnb-text-begin -->

Se puede ver un pequeño codo para k=3, aunque no es muy pronunciado. Por lo tanto el mejor número de cluster es 3.


#### 5.2) Cluseting jerárquico


Se va a aplicar un clustering jerárquico con un número de cluster k = 3 y se va a visualizar el resultado con un dendrograma.


<!-- rnb-text-end -->


<!-- rnb-chunk-begin -->


<!-- rnb-source-begin eyJkYXRhIjoiYGBgclxuIyBTZSBkaWNlIHF1ZSBzZSB2YSBhIHV0aWxpemFyIGxhIGRpc3RhbmNpYSBldWNsaWRpZW5hIHBhcmEgY2FsY3VsYXIgbGEgZGlzdGFuY2lhIGVudHJlIGxvcyBkYXRvc1xuZGlzTWF0IDwtIGRpc3QoRGF0b3MsIG1ldGhvZCA9IFwiZXVjbGlkZWFuXCIpXG5gYGAifQ== -->

```r
# Se dice que se va a utilizar la distancia euclidiena para calcular la distancia entre los datos
disMat <- dist(Datos, method = "euclidean")
```

<!-- rnb-source-end -->

<!-- rnb-output-begin eyJkYXRhIjoiV2FybmluZyBpbiBkaXN0KERhdG9zLCBtZXRob2QgPSBcImV1Y2xpZGVhblwiKSA6XG4gIE5BcyBpbnRyb2R1Y2VkIGJ5IGNvZXJjaW9uXG4ifQ== -->

```
Warning in dist(Datos, method = "euclidean") :
  NAs introduced by coercion
```



<!-- rnb-output-end -->

<!-- rnb-source-begin eyJkYXRhIjoiYGBgclxuIyBTZSB1dGlsaWNlIGVsIGFsZ29yaXRtbyB5IHNlIGluZGljYSBxdWUgc2UgY2FsY3VsYSBsYSBkaXN0YW5jaWEgZW50cmUgbG9zIGNsdXN0ZXJzIGNvbiBXYXJkJ3MgbWV0aG9kXG5cbm1vZGVsbyA8LSBoY2x1c3QoZGlzTWF0LCBtZXRob2QgPSBcIndhcmQuRDJcIilcbnBsb3QobW9kZWxvLCBjZXggPSAwLjYsIGhhbmcgPSAtMSlcbnJlY3QuaGNsdXN0KG1vZGVsbywgayA9IDMsIGJvcmRlciA9IFwibWFnZW50YVwiKVxuYGBgIn0= -->

```r
# Se utilice el algoritmo y se indica que se calcula la distancia entre los clusters con Ward's method

modelo <- hclust(disMat, method = "ward.D2")
plot(modelo, cex = 0.6, hang = -1)
rect.hclust(modelo, k = 3, border = "magenta")
```

<!-- rnb-source-end -->

<!-- rnb-plot-begin eyJoZWlnaHQiOjQzMi42MzI5LCJ3aWR0aCI6NzAwLCJzaXplX2JlaGF2aW9yIjowLCJjb25kaXRpb25zIjpbXX0= -->

<img src="data:image/png;base64,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" />

<!-- rnb-plot-end -->

<!-- rnb-chunk-end -->


<!-- rnb-text-begin -->



<!-- rnb-text-end -->

