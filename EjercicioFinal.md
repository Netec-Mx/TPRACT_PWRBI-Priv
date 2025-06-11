# Ejercicio Final

## Objetivo de la práctica:

Al finalizar la práctica, serás capaz de:

- Aplicar los conocimientos adquiridos durante el curso mediante la creación de un mini proyecto que emule un reporte, el cual, actualmente ya es utilizado.

## Duración aproximada:

El tiempo requerido para completar este ejercicio dependerá de la experiencia y familiaridad del usuario con Power BI. Sin embargo, se estima que, para quienes lo utilizan por primera vez, la realización exitosa del ejercicio puede tomar aproximadamente **6 horas**.

## Planteamiento del ejercicio.

> Como parte de sus actividades le piden elaborar el borrador de un reporte de seguimiento de solicitudes de crédito con Power BI Desktop para analizar el desempeño de las solicitudes comparando los resultados mes a mes.  
En dicho análisis le piden hacer un primer borrador de este reporte analizando algunos datos sencillos, como las solicitudes aprobadas, las regiones donde y sucursales donde vienen estas solicitudes entre otros detalles, pero que no son los datos 100% pues es una prueba de concepto.

### Metodología

> La actividad está pensada para hacerse de manera estructurada, como se hizo durante el curso, pero que las instrucciones no son tan detalladas, para reforzar aplicar estos conocimientos sin depender de una guía paso por paso.

### Criterios de evaluación

>Los criterios de evaluación se basan en cumplir con las evidencias solicitadas considerando que lo mostrado por el participante sea igual o al menos similar a la imagen de referencia mostrada. Considerando también que los datos sean congruentes y no muestren anomalías.

### Actividades a realizar.

![Actividades a realizar.](./images/Actividades.png)


Vamos a trabajar sobre distintos archivos, pero comenzaremos usando como base el siguiente archivo ***Datos para Funnel - Abril 2025- SIF+POS*** para partir a la fase del análisis de los datos.

![Archivo Datos para Funnel - Abril 2025](./images/img-1.png)

## Fase de análisis 


Por lo que procede a abrir la aplicación de ***Power BI Desktop*** e importar los datos.

Al momento de importar los posibles datos para el análisis, se da cuenta que la herramienta de ***Power Query*** le muestra varias consultas que puede utilizar para obtener los datos y que superan las hojas originales que tiene el archivo.

Considerando lo anterior, le piden que importe aquellas que realmente le podrían servir para analizar la información y, posteriormente, realice una serie de pasos para poder dejar los datos en un estado correcto para poder realizar el reporte.

![Posibles consultas](./images/img-2.png)

Como nota le mencionan que aquellas que incluyen ***$_FilterTable*** no son necesarias para el estudio pues son parecidas a las otras consultas con nombre similar, considerando esto de las 9 posibles consultas, ahora solo tendrá 5 opciones de consultas para analizar y determinar cuales se usaran para el estudio.

Al final para este primer paso deberá trabajar con una sola consulta.

---

Ahora que sabe cuál es la consulta que utilizará para poder procesar la información, es momento de examinarla para poder determinar si los datos están listos o no para poder ser utilizados.

### ¿Nota algo raro en las columnas que aparecen en la consulta?

- ¿Hay columnas con nombres similares?

- ¿Que vuelve distintas a esas columnas?

- Del resto de las columnas
  - ¿Que puede observar?
  - ¿Hay columnas que no tienen valores?

- ¿Nota valores atípicos dentro de las columnas? Por ejemplo, en la columna ***External reference***.
  - ¿Nota algún valor raro?
  - ¿Logra identificar que representa el valor 1 en esta columna?

- Para la columna ***AA***
  - ¿Que observa?
  - ¿Todas las filas tienen valores?
  - ¿Que valores tienen las columnas? 

- Examine de una forma similar a las columnas ***Bussiness Partner***, ***Nombre del cliente***, ***Plazo***, ***Loan value amount***, ***Buckets monto*** y ***RESULTADO SCORE***.

- Para la columna ***Producto***, ¿Distingue el significado de los valores 1, 2, 3?

- Observe las columnas ***Mes de pago*** y ***Mes de solicitud***
  - ¿Que nota de distinto en ellas?
  - ¿Son del mismo tipo de dato?

## Preprocesamiento de los datos.

 Con base a sus observaciones, proceda a modificar la consulta para mejorar el modelo. A continuación, se listan algunas sugerencias de transformaciones que deben aplicarse para lograr el análisis adecuado.

![Columnas a modificar](./images/img-3.1.png)

Para la primer pareja de columnas con el mismo nombre, seleccione alguna de las dos columnas ***Marca*** y elimine la otra, de la columna resultante, aplique los cambios que correspondan para dejarla de la siguiente manera:

- Nombre de la columna: ***Marca***

- Los valores de la columna no deben estar abreviados y todos los posibles valores para una marca deben estar homologados.

- Los valores vacíos no deben ser considerados para este análisis.

- El análisis solo considera los vehículos que pertenecen a grupo Volkswagen, por lo que se omitirán los valores de vehículos que pertenezcan a otras marcas.

![Columna Marca](./images/img-4.png)

Para la segunda pareja de columnas, elimine aquella columna que solamente tiene un valor repetido y renombre la restante como ***Estado de la cotización***.

Para los valores de la columna ***Producto***. Pruebe a reemplazarlos de la siguiente manera:
- 1 -> Leasing
- 2 -> Credit
- 3 -> Finance / Premium credit


Para las columnas de ***Mes de pago*** y ***Mes de solicitud*** de momento no haga cambios en el tipo de dato de ninguna de estas columnas.

Para esta primer parte deberá obtener un resultado similar a los siguientes:

![Resultados Fase análisis 1](./images/img-5.1.png)

![Resultados Fase análisis](./images/img-5.png)

## Ingesta de datos

Si bien ya hemos obtenido los datos para poder comenzar con el modelado de datos, hay que considerar algunas cosas sobre los datos que nos han compartido.

- ¿Es toda la información necesaria para realizar el análisis?

- ¿Necesitamos algún tipo de dato sobre el cliente?

- ¿Necesitamos información de los gerentes de la sucursal?

- ¿Nos interesa obtener información para filtrar por sucursal o por región?

Considerando estos puntos y que el equipo encargado de proporcionarnos los datos eventualmente nos pasará la información pendiente, decidimos ir avanzando en la creación y modelado de los datos, por ejemplo, creando nuestra propia tabla para poder obtener información que nos permita filtrar por región geográfica, por estado y, eventualmente cuando nos pasen la información, por sucursal.

Para ello entonces visitaremos la siguiente liga:  https://es.wikipedia.org/wiki/Regiones_de_M%C3%A9xico

Importaremos y manipularemos los datos de tal forma que la tabla resultante quede con dos columnas; ***Región*** y ***Estado***. Para ello vuelva a ***Power Query*** para importar los nuevos datos.

![Posibles consultas a ingresar](./images/img-6.png)

Pruebe intentando opciones como ***combinar consultas***, ***anexar columnas*** o bien la opción ***Agregar tabla mediante ejemplos***.

La tabla resultante la llamaremos ***Sucursales*** y debe quedar de la siguiente manera:

![Resultado Consulta Sucursales](./images/img-7.png)


Nos comenta el equipo, que nos proporcionará un Excel que contiene la información de que agencias pertenecen a cada estado. Por lo que debemos obtener la información con Power Query y combinar esa nueva consulta con la que ya teníamos anteriormente, a esta nueva consulta la denominaremos agencias.

Quedando como resultado algo similar a lo siguiente.

![Resultado Consulta Agencias](./images/img-8.png)

Al momento de ingerir los datos en Power BI, solamente deben aparecer 2 consultas: ***Agencias*** y ***Datos para Funnel***.

![Resultado Ingesta Datos](./images/img-9.png)

---

## Modelado de los Datos
Ahora crearemos una tabla de fechas, para poder realizar cambios en el modelo y, de esta manera poder aprovechar algunas funciones de Time Intelligence.

Para ello dentro de Power BI, cambie a la vista de Tabla para poder generar una nueva tabla calculada, dicha tabla la llamaremos ***Fecha***, para este ejercicio, asumiremos que el calendario fiscal esta alineado con el año natural, es decir el año fiscal termina cuando termina el año.

>Recuerda que para generar un calendario automático puedes usar el método ***CALENDARAUTO()***  
Recuerda que estas tablas especiales para fechas las debemos marcar.

Ahora, dentro de la tabla ***Fecha***, generaremos una nueva columna calculada que se llamará ***Mes de Solicitud***, pero ¿Cuál es la finalidad de esta nueva columna? ¿No tenemos ya esta columna en la tabla original?

> Recuerda que lo que hacemos en este paso es aplicar un "proceso" donde, dependiendo la fecha donde se haya registrado la solicitud de crédito, nosotros simplemente ***formateamos*** este dato con la parte que nos interesa, por ejemplo ***enero-25***. ¿Recuerdas el formato que tiene ***Mes de solicitud*** en la consulta original? Intenta hacerlo mismo para esta nueva columna.

El resultado para esta tabla calculada debe quedar de la siguiente manera:

![Resultado tabla Fecha](./images/img-10.png)

> Recordemos que un agregado de Power BI es poder acceder a las funciones de Time Intelligence, las cuales nos permitirán hacer cálculos bastante interesantes pero que debemos utilizar por ende una columna del tipo de fecha para poder hacer estos cálculos, por ello es por lo que realizamos este paso. 

Como hemos creado nuestra propia columna ***Mes de Solicitud*** ya no es necesario mantenerlo en la consulta principal, por lo que podemos eliminarla de la consulta principal.

Quedándonos los atributos dentro de las tablas de la siguiente manera:

![Resultado tabla Fecha](./images/img-12.png)

Ahora pasando a la Vista de Modelo, establezca una relación entre la consulta principal y la tabla Fecha.

Y haga lo mismo, pero ahora con una relación entre la tabla principal y la tabla Agencias.

Las relaciones deberían quedar de la siguiente manera:

![Resultado tabla Fecha](./images/img-13.png)

Si bien ya tenemos prácticamente todo lo necesario para poder analizar la información y elaborar nuestro reporte, debido a unos requerimientos que nos solicitan, debemos agregar algunas cosas para realizar el análisis de forma correcta.

Considerando lo anterior, en la tabla ***Agencias*** sabemos que nos pedirán hacer investigación a distintos niveles, a nivel regional, a nivel estatal o a nivel sucursal / agencia. Por lo que nos piden elaborar algo que nos permita aplicar estos filtros de forma rápida sin tener que agregar distintos filtros, el resultado lo nombraremos como ***Niveles estudio***.

> Esta descripción suena a una forma de ordenar la información en una especie de ***Jerarquía***.

Ahora, dentro de la tabla principal hay distintos campos que podemos observar que se resumen de forma automática, pero la forma en que lo hacen no consideramos que sean correctas, por lo que modificaremos la forma en la que se resumen estos datos para poderlos resumir de una forma distinta a una mera suma, por ejemplo, probando resumir entre ***Recuento*** y ***Recuento (distintivo)***.

> La vista de datos nos puede ayudar a definir algunos atributos de los datos.

Nos piden analizar la información del estatus de las solicitudes de tal forma que las que tengan un estado de ***APROBADO*** o ***CONTRATO ACTIVO*** se cuenten ambas como solicitudes ***Autorizadas***, las que estén en ***EN PROCESO*** o ***REVISIÓN DOCUMENTOS*** se cuenten como ***Revisión*** y todas las demás como ***Rechazadas***.

> Esta descripción suena a una forma de ***agrupar los datos***. Le llamaremos ***Estatus***

Nos piden elaborar una medida para hacer el seguimiento mes a mes del porcentaje de cambio entre cantidad de solicitudes de un mes a otro.

Desarrolle esta medida ya sea con una medida explicita o medida rápida.

> Recuerda que las medidas rápidas son mediante medios gráficos y las medidas explicitas es directamente con código.


Hasta este punto deberíamos tener algo parecido a lo siguiente:

![Resultados de modelado de datos](./images/img-14.png)
---

## Elaboración del reporte.

Ahora que ya tenemos algunos datos, vamos a comenzar a diseñar parte del reporte.

Por ejemplo, nos comentan que deben existir distintos filtros visuales para ver la información de acuerdo con: ***Marca***, ***Región***, ***Estado*** y ***Agencia***.

Nos piden adicionalmente tener un gráfico de columnas apiladas para poder identificar el porcentaje de solicitudes por mes, cada mes debe mostrar los valores agrupados las categorías que son Autorizadas o en Revisión, los resultados deben estar ordenados por mes y el porcentaje de cada categoría debe estar basado en el total del mes, no en el total de los datos.

>Considerando lo anterior, algunas pistas o elementos a considerar para lograr esto son los siguientes puntos:  
El eje X se basa en el Mes de la solicitud, pero dependiendo el tipo de dato que le hayamos asignado, será ordenado por orden alfabético o por orden cronológico, siendo quizás necesario crear una columna adicional en la tabla fecha, para que uno sea el que se muestra y el otro el que ordena.  
El eje Y muestra los datos de las solicitudes, pero nosotros queremos mostrar por un promedio, de usar las opciones directas del gráfico, se puede mostrar un porcentaje general, pero nosotros queremos un porcentaje que considere un cierto contexto, por lo tanto, necesitamos una medida.  
Para que la herramienta muestre los colores por estado de la solicitud, es necesario agregar dicho campo, pero recordemos que agregar directamente el campo ***Estado de la cotización*** generara más categorías de las requeridas. Por lo que el grupo que creamos anteriormente es lo que debemos de usar.

![Comparativa de gráficos](./images/img-15.png)

> La imagen de arriba muestra una imagen de referencia de, lo que muy posiblemente obtengamos al momento de intentar lograr la visualización deseada. El objetivo es lograr crear la visualización como se muestra en la parte inferior.

![Datos usados para el grafico](./images/img-16.png)

> ***Mes*** es una nueva columna en la tabla de ***Fecha***, 

> ***Porcentaje por Estatus por Mes*** es una nueva medida:  
Porcentaje por Estatus por Mes = 
DIVIDE(
    CALCULATE(COUNT('Datos para Funnel'[Number of Quotation])),
    CALCULATE(
        COUNT('Datos para Funnel'[Number of Quotation]),
        ALLEXCEPT('Datos para Funnel', 'Fecha'[Mes])
    ),
    0
)


Ahora nos piden un gráfico de embudo para poder mostrar la cantidad de solicitudes. El grafico de embudo debe permitir profundizar el analisis ya sea por mes, por estatus y, en último lugar, Estado de la cotización. Para este gráfico no nos piden muchas modificaciones mas haya de mostrar esta información.

![Datos usados para el gráfico de embudo](./images/img-17.png)


También nos piden mostrar una matriz donde se muestren los datos en crudo para poder ver como van cambiando estos valores. La matriz debe tener el recuento de las solicitudes y el cambio MoM%.

![Datos usados para el gráfico de matríz](./images/img-18.png)

Adicionalmente, nos piden elaborar 3 marcadores para mostrar la información solamente de febrero, marzo y abril y permitir ver esta información usando botones de navegación.


Por último nos piden editar la vista de la primer página del reporte para que sea una hoja de color azul, además de incorporar una imagen con el logo de la empresa en la parte superior izquierda. Quedando algo como la siguiente.

![Resultado final](./images/img-19.png)


Felicidades has terminado este laboratorio, has desarrollado un reporte a partir de instrucciones generales, lo que te permitira poder entender y aplicar estos mismos principios cuando tengas que desarrollar tus propios reportes.
