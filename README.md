<table>
	<tr>
		<th colspan="2" style="text-align:center">
			<img src="http://www.usb.ve/conocer/corporativa/archivos/logos/logo/logo.gif" width="64" height="43"><br/>
			Universidad Sim&oacute;n Bol&iacute;var<br/>
			Departamento de Computaci&oacute;n y Tecnolog&iacute;a de la Informaci&oacute;n<br/>
			Laboratorio de Algoritmos y Estructuras de Datos II (CI 2692)
	</tr>
	<tr>
		<th scope="row">Asignaci&oacute;n:</th>
		<td style="text-align:right">Proyecto 3</td>
	</tr>
	<tr>
		<th scope="row">Modalidad:</th>
		<td style="text-align:right">Parejas</td>
	</tr>
	<tr>
		<th scope="row">Ponderación:</th>
		<td style="text-align:right">20%</td>
	</tr>
	<tr>
		<th scope="row">Asignado:</th>
		<td style="text-align:right">Jueves, 21 de junio de 2018 (sem 9)</td>
	</tr>
	<tr>
		<th scope="row">Entrega:</th>
		<td style="text-align:right">Jueves, 12 de julio de 2018 (sem 12)</td>
	</tr>
</table>

Objetivos:
* Ejercitar su manejo de estructuras de datos.
* Trabajar la especificación, implementación y uso de un tipo abstracto de datos (TAD).

Cada grupo debe entregar el c&oacute;digo implementado y un informe haciendo commit en el repositorio.

# Agenda
## Introducci&oacute;n
El tipo con el que trabajaremos lo llamaremos *Agenda* y tiene como finalidad organizar las activi­dades de una persona. Una agenda almacena a lo sumo *MAX* actividades, este número es fijo para cada agenda. Para cada actividad que se registra, se almacena la fecha y la hora, su duración, su prioridad y nombre de la actividad.

Cada actividad se identificar&aacute; por su fecha y hora, almacenando estos datos en un *String* `"aaaammddhhmm"`. donde `aaaa` corresponde al año (entre 2018 y 9999), `mm` al mes (esto es, entre 01 y 12), `dd` al d&iacute;a (esto es, entre 0 y 31), `hh` a la hora (en formato 00 a 23) y `mm` a los minutos (esto es, entre 00 y 59). La duración de la actividad se representa con un entero positivo; el horario en que se puede programar una actividad es de 6am (0600) a 10pm (2200), por tanto la duración de una actividad debe ser tal que ninguna actividad termine luego de las 10pm.

Los nombres de las actividades se almacenan utilizando un *String* no vacío. La prioridad de una actividad se representa con un entero entre 0 y 5, ambos inclusive, siendo la prioridad 0 la prioridad de la actividad más importante y 5 la de la menos importante.

## Especificaci&oacute;n del TAD *Agenda*
A continuación se presenta una especificación del TAD *Agenda*. En ésta, se modela la organización de las actividades mediante 3 funciones parciales, que comparten el mismo dominio; el dominio de las funciones son los Strinqs que representan una fecha-hora v&aacute;lida para una actividad, el rango de la primera función corresponde a los *Strings* no nulos que representan nombres de actividades, el rango de la segunda función corresponde a los enteros positivos que representan duraciones válidas y el rango de la tercera función corresponde a los enteros entre 0 y 5 que representan prioridades. En primer lugar se presentan las operaciones más importantes del TAD:
1. *nuevaAgenda*, la cual crea una agenda en la cual no se ha programado ninguna actividad
2. *agregarActividad*, la cual permite incluir una nueva actividad en la planificación de actividades de la agenda;
3. *eliminarActividad*, la cual permite cancelar una actividad programada previamente en la aenda;
4. *listarActividades*, la cual lista todas las actividades programadas para un día dado, ordenadas segun su horario;
5. *buscarActividad*, la cual, dada una fecha-hora de una actividad, permite ver el nombre de la actividad programada;
6. *incluirActividades*, la cual, dada otra agenda, incluye todas las actividades programadas en esa otra agenda como actividades de la agenda actual.

### Modelo de Representación
```
const MAX : int 
var nombre: String → String
var duración: String → int
var prioridad: String → int 
```

### Invariante de Representación 
El siguiente invariante se debe cumplir sobre su estructura de datos en todo momento. Debe verificar que se cumplir&aacute; luego de cada operaci&oacute;n. En caso contrario, debe imprimir un error, y la operaci&oacute;n no se har&aacute; efectiva. *El programa debe seguir en funcionamiento luego de producirse el error.*


> dom(*nombre*) = dom(*duración*) = dom(*prioridad*) <br/>

>>  &and; |dom(*nombre*)| &le; MAX &and; (&forall; *y* : *y* &isin; rang(*prioridad*) : 0 &le; *y* &le; 5) <br/>

>>  &and; (&forall; *x* : *x* &isin; dom(*nombre*): duraciónVálida(*x*, duración(*x*))) <br/>

>>  &and; (&forall; *x* : *x* &isin; dom(*nombre*): fechaHoraVálida(*x*)) <br/>

>>  &and; (&forall; *y* : *y* &isin; rang(*nombre*) : *y* &ne; "") <br/>

>>  &and; (&forall; *x* : *x* &isin; dom(*nombre*)

>>>   : &not;(&exist; *y* : y &isin; dom(*nombre*) &and; *x* &ne; *y* : seSolapan(*x*, duración(*x*), *y*, duración(*y*))))

### Operaciones 
A continuaci&oacute;n se presentan pre y post condiciones para cada operaci&oacute;n. Debe verificar que se cumple la precondici&oacute;n antes de realizar la operaci&oacute;n. En caso contrario, debe imprimir un error y no realizar la operaci&oacute;n. Las postcondiciones indican qu&eacute; debe realizar la operaci&oacute;n.

* `fun` *nuevaAgenda*(*m*: `int`) &rarr; *Agenda*

  { `Pre: ` *m* &gt; 0 } 

  { `Post:` *nuevaAgenda*.MAX = *m* &and; *nuevaAgenda*.*nombre* = &empty;
    &and; nuevaAgenda.duraci&oacute;n = &empty; &and; nueaAqenda.prioridad = &empty; } 

* `proc` *agregarActividad*(`in-out` *a* : *Agenda*; `in` *fecha.Hora* : `String` ; in duracion : isit ; in prioridad : int; in nombre : String )

  { `Pre: ` fechaHoraV&aacute;lida(*fechaHora*) &and; duraci&oacute;nV&aacute;lida(*fechaHora*, *duraci&oacute;n*)
    &and; 0 &le; *prioridad* &le; 5 &and; *nombre* &ne; "" &and; |dom(*nombre*)| &lt; MAX
      &and; &not;choca(*a,fechaHora, duraci&oacute;n*) } 

  { `Post:` *a.nombre* = *a*<sub>0</sub>.*nombre* &cup; {(*fechaHora, nombre*)} 
    &and; *a.duraci&oacute;n* = *a*<sub>0</sub>.*duraci&oacute;n* &cup; {(*fechaHora, duracion*)} 
    &and; *a.prioridad* = *a.prioridad* &cup; { (*fechaHora, prioridad*)} } 

* `proc` *eliminarActividad* (`in-out` *a* : *Agenda*; `in` *fechaHora* : `String`)

  { `Pre: ` fechaHora &isin; dom(*nombre*) } 
  
  { `Post:` *a.nombre* = *a*<sub>0</sub>.*nombre* &minus; {(*fechaHora*, *a*<sub>0</sub>.*nombre*(*fechaHora*)} 
    &and; *a.duraci&oacute;n* = *a*<sub>0</sub>.*duracion* &minus; {(fechaHora, *a*<sub>0</sub>.*duraci&oacute;n(fechaHora))} 
    &and; *a.prioridad* = *a*<sub>0</sub>.*prioridad* &minus; {(*fechaHora*, *a*<sub>0</sub>.*prioridad*(*fechaHora*))} } 
* proc listarActividades (`in` *a* : *Agenda*; `in` *fecha*: `String`) 

  { `Pre: ` esFechaV&aacute;lida ( `toInt`(*fecha*)) } 

  { `Post:` Está escrita en pantalla la secuencia ordenada sin repeticiones formada por los elementos del conjunto 
  
    {x : x &isin; dom(*nombre*) &and; (*fecha* + "0600") &le; *x* &le; (fecha + "2200") : (*x*, *nombre*(*x*), *duraci&oacute;n*(*x*), *prioridad*(*x*))} }

* `fun` buscarActividad ( *a* : *Agenda*; *fechaHora*: `String`) &rarr; `String`

  { `Pre: ` fechaHoraV&aacute;lida (*fechaHora*) } 

  { `Post:` (*fechaHora* &isin; dom(*nombre*) &and; *buscarActividad* = *nombre*(*fechaHora*) &or; (fechaHora &notin;. dom(*nombre*) &and; *buscarActividad* = "") }

* proc incluirActividades (`in-out` *al* : *Agenda*; `in` *a2* : *Agenda*)

  { `Pre: ` &not;(&exist; *x* &isin; dom(*a1.nombre*): choca(*a2*, *x*, *a1.duraci&oacute;n*(*x*)))
    &and; |dom(*a1.nombre*)| + |dom(*a2.nombre*)| &le; *a1*.MAX }

  { `Post:` *a1.nombre* = *a1*<sub>0</sub>.*nombre* &cup; *a2.nombre* 
    &and; *a1.duraci&oacute;n* = *a1*.duraci&oacute;n &cup; *a2*.duraci&oacute;n 
    &and; *a1*.prioridad* = *a1*<sub>0</sub>.*prioridad* &cup; *a2.prioridad* }
  
  &vellip;
  
  `Fin TAD`

Esta especificación utiliza los predicados auxiliares:
1. duraci&oacute;nValida, que dado un `String` que representa una fecha-hora y un entero que representa una duración, se satisface si la duración permite que la actividad termine en el horario válido;
2. fechaHoraV&aacute;lida, dado un `String`, se satisface si corresponde al formato de una fecha-hora válida;
3. esFechaV&aacute;lida, se satisface si el entero corresponde a una fecha v&aacute;lida; 4. esHoraV&aacute;lida, se satisface si el entero corresponde a una hora valida
5. seSolapan, se satisface si las fechas-horas y duraciones son tales que se solapan, las fechas-horas son dados como St1ing y la duraciones como enteros
6. choca, se satisface si, en la agenda dada como primer argumento, hay alguna actividad tal que se solape con la fecha-hora y duración dadas como segundo y tercer argumento.

A continuación se presentan sus definiciones: 
* duracionV&aacute;lida (*fh*, *d*) = fechaHoraValida(*fh*) &and; d &gt; 0
  &and; (((( obtenerMinutos(*fh*) + *d*) mod 60)+
    ((( obtenerMinutos(*fh*) + d) div 60) + obtenerHora(*fh*)) &times; 100) &le; 2200)
* fechaHora Valida(*fh*) = length(*fh*) = 12 &and; (&forall; *j* : 0 &le; *j* &lt; length(*fh*) : "0" &le; *fh[j]* &le; "9") 
  &and; esHoraV&aacute;lida( `tolnt`( *fh*[8:12]))) 
  &and; esFechaV&aacute;lida( `tolnt`(*fh*[0:8])) 

* esFechaV&aacute;lida(*f*) = 1 &le; f mod 100 &le; 31 &and; 1 &le; (*f* div 100) mod 100 &le; 12 &and; *f* div 10000 &ge; 2018
* esHoraValida(*h*) = (6 &le; *h* div 100 &le; 21 &and; 0 &le; *h* mod 100 &le; 59) &or; (*h* div 100 = 22 &and; *h* mod 100 = 0)
* seSolapan(*fh1*, *d1*, *fh2*, *d2*) = fechaHoraV&aacute;lida(*fh1*) &and; fechaHoraV&aacute;lida(*fh2*) 
  &and; *d1* &gt; 0 &and; *d2* &gt; O 
  &and; ((*fh1* &lt; *fh2* &and; *fh2* &lt; fin(*fh1*, *d1*)) &or; *fh1* = *fh2* 
    &or; (*fh2* &lt; *fh1* &and; *fh1* &lt; fin(*fh2*, *d2*)))
* choca(*a*,*fh*, *d*) = fechaHoraV&aacute;lida(*fh*) &and; *d* &gt; 0 
&and; (&exist;x &isin; dom(*nombre*) : seSolapan(*x*, duraci&oacute;n(*x*), *fh*, *d*))

A continuación se presenta la definición de algunas de las funciones auxiliares que se utilizan en estos predicados:

* obtenerMinutos: recibe como argumento una fecha-hora v&aacute;lida representada con un `String` y retorna el entero correpondiente a los minutos de esa fecha-hora .

  obtenerMinutos(*fh*) = (`tolnt`(*fh*[8:12] mod 100)

* obtenerHora: reciben como argumento una fecha-hora v&aacute;lida representada con un `String` y retorna el entero correspondiente a las horas de esa fecha-hora. 

  obtenerHora(*fh*) = (`tolnt`(*fh*[8:12]) div 100)
  
* fin: recibe como argumentos una fecha-hora v&aacute;lida, representada con un `String`, y un entero positivo que representa la duración; y retorna un `String` correspondiente a la fecha-hora en que termina la actividad. 

  fin(*fh*, *d*) = fh[0:8] 
    +((obtenerHora(*fh*) + ((obtenerMinutos(*fh*) + *d*) div 60)) &lt; l0 ? "0" : "")+
    (( obtenerMinutos(*fh*) + *d*) mod 60) 
      +( obtenerHora(*fh*) + (( obtenerMinutos(*fh*) + *d*) div 60) &times; 100) 

El operador `a ? b : c` corresponde al operador condicional (si `a`, entonces `b`; si no `c`).

Además de las operaciones ya presentadas, se quiere que el TAD provea una variante del procedimiento *listarActividades*: una variación lista solamente las actividades importantes de una fecha dada, entendiendo por actividad importante aquella cuya prioridad es igualo menor a la prioridad dada como argumento; Esta operaci&oacute;n debe preservar el orden relativo a la fecha-hora: deben ser organizadas seg&uacute;n su prioridad y, en caso de existir dos o más actividades con igual prioridad, estas deben ser listadas según su fecha-hora. 

* `proc` *listarActividadeslmportantes* (`in` *a* : *Agenda*; `in` *fecha*: *String*; `in` *prioridad*: `int`)

  {`Pre: ` esFechaV&aacute;lida(`tolnt`(fecha)) &and; O &le; prioridad &le; 5 } 

  { `Post:` Está escrita en pantalla la secuencia ordenada sin repeticiones formada por los elementos del conjunto\
  
    {*x* : *x* &isin; dom(nombre) &and; (fecha + "0600" ) &le; *x* &le; (fecha + "2200")
        &and; *prioridad*(*x*) &le; *prioridad* 
      : (x, *nombre*(*x*) , *duraci&oacute;n*(*x*), *prioridad*(*x*))} } 

### Implementación
Para la implementación se necesita una nueva especificación, esta vez con modelo concreto, siendo esta nueva. especificación un refinamiento de la anterior (la anterior era una especificación con modelo abstracto). El modelo concreto usará matrices (arreglos de dos dimensiones) la idea es representar cada una de las actividades como una fila, de la matriz. Por ejemplo una actividad cuya fecha-hora pertenece al dominio de las funciones nombre, duracion y prioridad, Se representa con la fila *i* de la matriz almacenando en cada una de sus casillas la información correspondiente a su fecha-hora, nombre, duración y prioridad. Luego inicialmente se puede pensar en utilizar una matriz de MAX &times; 4 elementos sin embargo debido a los distintos tipos que tienen los datos de las actividades se hace necesario hacer esta representación con dos matrices de MAX &times; 2 elementos cada una, siendo la primera de String y la segunda de enteros. Adicionalmente se requiere contar con un entero que indique la cantidad de actividades qu se han registrado, para saber cuántas filas de las matrices contienen actividades validas.

Como parte del diseño de la estructura de datos, se decide almacenar las actividades de manera ordenada. Las asignaturas estarán organizadas según su fecha-hora ascendentemente, esto con el fin de permitir realizar algunas de las operaciones del TAD eficientemente.

### Programa Cliente
Una vez que se tiene la implementación del TAD Agenda, se puede utilizar el nuevo tipo en programas; a estos programas se les llama clientes del tipo. Se quiere que Ud. implemente un programa cliente del TAD que permita ejecutar cualquiera de las operaciones del TAD que aparecen en la especificación. Inicialmente, el programa debe solicitar al usuario el número de agendas que desea manejar y sus tamaños (número máximo de actividades que puede registrar el cliente en cada una). Luego ofrecer un menú con 9 opciones:
1. agregarActividad;
2. eliminarActividad;
3. listarActividades;
4. buscarActividad;
5. incluirActividades;
6. listarActividadeslmportantes;
7. cantidadActividades (de la agenda);
8. cantidadActividades (de la agenda. para una fecha dada);
9. salir del sistema.

Este menú debe mostrarse iterativamente al usuario. 

Redacci&oacute;n de Vicente Yriarte, USB

### Informe
El informe debe contener:
* Introducci&oacute;n
* C&oacute;mo correr su programa
* Detalles de implementación
* Un analisis de orden para cada una de las 6 operaciones
  * Mejor caso
  * Caso promedio
  * Peor caso
* Conclusiones

El informe debe reflejar lo implementado en su c&oacute;digo.

### Evaluaci&oacute;n
El proyecto tiene una ponderaci&oacute;n de 20 puntos. Se asignar&aacute;:
* 11 puntos por su Informe (&frac12; punto por cada elemento especificado anteriormente)
* 5 puntos por ejecuci&oacute;n
  * &frac12; punto por cada operaci&oacute;n del men&uacute;
  * &frac12; punto por el men&uacute; en s&iacute;
* 4 puntos por c&oacute;digo
  * &frac12; punto por cada operaci&oacute;n del men&uacute; exceptuando la operaci&oacute;n de salir
  * &frac12; punto por ajustarse a la filosof&iacute;a de Python
