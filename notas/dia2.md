
# Tipos de datos

## Desde el punto de vista computacional: 

Textos, números, fechas...

Tienen impacto grande en los tiempos de procesamiento, espacio de almacenamiento... ---> €€€€

## Desde el punto de vista estadístico:

- Cualitativos
  - Nominales                           Clasificarlos
  - Ordinales                           Clasificarlos + Ordenarlos
- Cuantitativos (unidad de medida)      Clasificarlos + Ordenarlos + Operaciones aritméticas

# La estadística

Ciencia que nos ayuda a capturar, estructurar, procesar, analizar e interpretar datos.

## Estadística descriptiva

### Análisis univariable

Nos ayuda a RESUMIR LOS DATOS para poder entenderlos: TENER LOS DATOS NO ES LO MISMO QUE ENTENDERLOS!

- Tablas de frecuencias NOMINALES, ORDINALES, CUANTITATIVOS (DISCRETOS, con pocos valores posibles)
  A su vez las puedo representar como GRÁFICOS DE BARRAS (Barras separadas) o GRÁFICOS CIRCULARES
- Gráficos para variables cuantitativas 
  - Histogramas
  - Boxplot (Gráfico de cajas y bigotes)
- Estadísticos
  - Medidas de tendencia central: Media, mediana, moda
  - Medidas de dispersión: Desviación típica, Rango semi-intercuartílico
  - ...

## Análisis multivariado

Buscar relaciones entre variables (correlaciones, asociaciones...) . No podemos dar causa-efecto.
Desde el punto de vista de negocio si puedo buscar esas causalidades... En ocasiones lo hago.. en otras me da igual!

No perdamos de vista una cosa! Estamos jugando a predecir el futuro! De eso va BI... no la estadística.. pero si BI.
BI: Aportar datos para la toma de decisiones: DECISIONES INFORMADAS
DECISIONES sobre el futuro. No tomo decisiones sobre lo que ya ha pasado! Tomo decisiones sobre el futuro, basándome en los datos del pasado!

Esto básicamente es jugar a ser adivinos!
Hay varias formas de anticiparme al futuro:
- Bolita de crital
- Lectura de manos
- Tarot
- Lectura de posos del café (té)...
- Estadística

Más o menos están al mismo nivel!

Tengo miles de miles de millones de datos! Soy la empresa con más datos del mundo.
Tengo toda la información de lo que hace una persona desde que se levanta hasta que se acuesta. Tengo todos los datos pasados de esa persona... su genoma... TODO!
Quiero saber si esa persona el próximo año me da a dar un parte en el seguro médico que tiene contratado conmigo.
ES POSIBLE ACERTAR ESO? SOY CAPAZ YO DE PREDECIR que es persona ha resbalado en el suelo con una cascara de plátano que ha tirado un niño y se ha partido la pierna?

La única diferencia con la estadística.. y no es poca es que me ayuda a cuantificar la PROBABILIDAD NO DE ACERTAR, SINO DE EQUIVOCARME! Por que me da igual saber si Menchu se va a partir la pierna (pobre Menchu!).
Lo que me importa es tasar la probabilidad de equivocarme... Saber en cuantas de esas decisiones me voy a equivocar...
Si soy un seguro, el gasto de esas equivocaciones, lo reparto entre todos mis clientes... y sigo ganando pasta!

La primera suposición GIGANTE que hacemos es que el mundo va a seguir funcionando TAL Y COMO HA FUNCIONADO HASTA AHORA! Y Esto... es mucho suponer... pero.. bueno. Confiemos en que es así.

Lo que haremos será conociendo ciertos datos, intentar predecir otros datos.
- Ante ciertos eventos en el mercado, tendencias... perfiles de mis clientes... intentar predecir su comportamiento futuro.
  Como esta persona nueva que entra en la tienda... tiene tal rango de edad... y como las personas de ese rango de esas edades han comprado en el pasado... que es lo que va a comprar esta persona nueva?
A veces la cuenta es más simple:
Como el año pasado y el anterior y el anterior no he vendido gafas de sol en diciembre... asumo, tomo la decisión de creer que este año tampoco voy a vender gafas de sol en diciembre. (1 variable)


Esto mismo es lo que hacen los modelos de Machine learning... pero con miles de variables y millones de datos.

Aquí ... pues juntamos pocos datos.. y dejamos a nuestro cerebro el trabajo de interpretación... buscar relaciones... y es complejo.

---

# Qué tipo de estudio puedo hacer cuando junto 2 variables, en base a su tipo (desde el punto de vista estadístico)

## Nominal x Nominal

Color de ojos / País de nacimiento

Una tabla de frecuencias donde ponga en filas una variable y en columnas la otra (Tabla de contingencia)

VOY A UN PUEBLO: En ese pueblo, conozco a priori que la mitad de la gente son varones y la otra mitad mujeres.

Y entonces voy a diferentes sitios:

               Hombres     Mujeres     Total
     Bus         25/23        25/27     50       ¿Me es raro? ¿Me sorprende? ¿Me escama? Está bien
     Tren        100/110      100/90    200      ¿Me es raro? ¿Me sorprende? ¿Me escama? Está bien
     Mercado     50/52        50/48     100      ¿Me es raro? ¿Me sorprende? ¿Me escama? Está bien
     Médico      40/1         40/79     80       ¿Me es raro? ¿Me sorprende? ¿Me escama? KA PASAO!!!!¿¿¿???
     ...

Como los datos que. he encontrado no son los que esperaba encontrar.. digo.. AQUÍ PASA ALGO. IDENTIFICADO HALLAZGO!
Cuando los datos a priori NO SE PARECEN A LOS datos reales, digo que hay una relación.
Si los datos a priori SE PARECEN A LOS datos reales, digo que NO hay relación.

Hay una relación entre ir en bus y el sexo de la persona? NO
Hay una relación entre ir en tren y el sexo de la persona? NO
Hay una relación entre ir al mercado y el sexo de la persona? NO
Hay una relación entre ir a ese médico y el sexo de la persona? SI

Aquí el tema se puede volver más oscuro...

     Tren        100/110      100/90         No me sorprende
     Tren        100/120      100/80         No me sorprende
     Tren        100/130      100/70         ??? SI O NO??? AHHH!!
     Tren        100/140      100/60         ???
     Tren        100/150      100/50         ???
     Tren        100/10       100/190        SI ME SORPRENDE

    Las relaciones no se dan o no se dan. Se dan gradualmente. Hay grados de relación.
    Hay más o menos relación. Y necesitamos una forma de cuantificar / Calcular ese grado de relación.
    Sobre todo para que todos lo hagamos de la misma forma y lleguemos a las mismas conclusiones.

    En estos estudios la estadística ofrece un estadístico... para medir el grado de asociación entre 2 variables cuantitativas nominales: Chi-cuadrado... es un poco ruina! 0-> Infinito
    Ese a su vez lo usamos de base para calcular otros: V de Cramer, Coeficiente de contingencia, Phi... Y esos si están guay... están entre 0-1
    0.. NO HAY RELACION
    1.. NO ES QUE HAYA MUCHA RELACION... ES QUE SON LA MISMA VARIABLE! = RUINA!
    Según sube ese número es que hay más relación entre las variables.    
    
A qué preguntas podría intentar responder yo?
- Si hay una prevalencia de un color de ojos en un sexo u otro? Un color de ojos es más común en un sexo u otro?
- Si conozco el color de ojos de una persona... quizás puede esa información ayudarme a predecir su país de nacimiento (con más o menos probabilidad)?

Esa tabla la podemos representar gráficamente: BARRAS (Apiladas o agrupadas) o GRÁFICO DE MOSAICO(maps de calor)

## Nominal x Ordinal

Si uso la variable ordinal como si fuera nominal, puedo hacer el mismo estudio que arriba (NOMINAL x NOMINAL)

    Pais            Sin estudios  Estudios primarios   Estudios secundarios   Estudios universitarios   Total
    España         5/4           20/22               30/28                 45/46                    100
    Francia        10/12         25/23               35/37                 30/28                    100
    Italia         15/14         30/32               25/26                 30/28                    100
    Alemania       20/18         25/50               20/22                 35/33                    100
    Total          50/48         100/104             110/113               140/135                  400   

Nivel de estudios / País de nacimiento
A qué preguntas podría intentar responder yo?
- Qué país tiene mayor nivel de estudios? Si distintos países tienen distinto nivel de estudios?
- Hay un determinado nivel de estudio que se ve más en unos países que en otros? USA LA CAPACIDAD NOMINAL DE LA VARIABLE NIVEL DE ESTUDIOS
- Si en ciertos países hay un "mayor nivel" de estudios...que en otros. USA LA CAPACIDAD ORDINAL DE LA VARIABLE NIVEL DE ESTUDIOS
Y son 2 estudios / Estrategias distintas que hemos/podemos aplicar al análisis de los datos.
 
Si hago un estudio usando la capacidad NOMINAL de la variable, lo que busco son las CASILLAS QUE ME ESCAMAN. Que pueden ser casillas sueltas!
Pero... también puedo mirar si hay TENDENCIAS! Esto es cuando hablo de MAS NIVEL DE ESTUDIOS O MENOS NIVEL DE ESTUDIOS

    PAIS            Sin estudios < Estudios primarios <  Estudios secundarios < Estudios universitarios   Total
    España             10                20                   15                       5
    OTRO               5                 20                   20                       20 *** ESTE PAIS TIENE MAYOR NIVEL DE ESTUDIOS
    OTRO2              **100**            0                    0                        **25**

Además de ver casillas en esa tabla... que me ayuda a identificar casillas (COMBINACIONES DE MODALIDADES) que me sorprenden.. que no me encaja con lo que esperaba, puedo hacer otra cosa.

Cómo sé si un país tiene o no "mayor nivel de estudios"?
MEDIANA DE NIVEL DE ESTUDIOS DE ESPAÑA: Estudios primarios
MEDIANA DE NIVEL DE ESTUDIOS DE OTRO:   Estudios secundarios
MEDIANA DE NIVEL DE ESTUDIOS DE OTRO2:  Sin estudios

- Estudio de comparación de medianas entre varios grupos.
  De ahí saco que en OTRO hay mayor nivel de estudios que en España. Porque su nivel de estudios mediano es mayor.
  De ahí saco también que en OTRO2 hay menor nivel de estudios que en España. Porque su nivel de estudios mediano es menor.


## Nominal x Cuantitativa

Altura / País de nacimiento

Puedo usar la capacidad NOMINAL de la variable Altura... creando rangos... y hacer un estudio de NOMINAL x NOMINAL
    A ver si alguna casilla me descuadra.
Puedo usar la capacidad ORDINAL de la variable Altura...y hacer un estudio de comparación de medianas entre varios grupos.
Puedo usar la capacidad CUANTITATIVA de la variable Altura...y hacer un estudio de comparación de medias entre varios grupos. ( ESTE LO HARE SI LOS GRUPOS TIENEN DISTRIBUCIONES SIMÉTRICAS)... de lo contrario, la media NO SERA REPRESENTATIVA.... y este estudio una patraña!

Algún gráfico relevante?
- Boxplot (gráfico de cajas y bigotes) por países
- Violin plot por países
- Pirámide poblacional (solo tiene sentido cuando la variable nominal es dicotómica) (son 2 histogramas pegados por el culo)
- En algunos casos, puedo superponer histogramas.. pero se complica la interpretación.


## Ordinal x Ordinal

- Usar las 2 variables como NOMINALES... y hacer su tabla de contingencia.. sus estadísticos de asociación...
  Un diagrama de barras apiladas o agrupadas. BUSCANDO CASILLAS QUE ME SORPRENDAN
- Puedo usar el poder ordinal de una de ellas y hago el estudio de comparación de medianas en base a los grupos generados por la otra variable (que la uso como NOMINAL: CLASIFICAR) 
- Y lo mismo pero al revés... usando la otra variable como ORDINAL y la primera como NOMINAL

## Ordinal x Cuantitativa

- Usar las 2 variables como NOMINALES... y hacer su tabla de contingencia.. sus estadísticos de asociación...
  Un diagrama de barras apiladas o agrupadas. BUSCANDO CASILLAS QUE ME SORPRENDAN
- Puedo usar el poder ordinal de una de ellas y hago el estudio de comparación de medianas en base a los grupos generados por la otra variable (que la uso como NOMINAL: CLASIFICAR) 
- Y lo mismo pero al revés... usando la otra variable como ORDINAL y la primera como NOMINAL
- Puedo hacer un estudio de comparación de medias (si aplica... distribuciones simétricas). De las medias de mi variable CUANTITATIVA en base a los grupos generados por la variable ORDINAL (que la uso como NOMINAL: CLASIFICAR)

## Cuantitativa x Cuantitativa

Puedo hacer todo lo anterior.. pero... aquí hay un gráfico adicional y un(2) estadístico adicional.
Scatter plot (diagrama de dispersión... nube de puntos).
En eso diagramas, básicamente representamos a los sujetos (puntos) en base a los valores que tienen en las 2 variables, que representamos en cada uno de los ejes.
Miramos a ver si los puntos dibujan (mirando desde lo lejos y con los ojos entreabiertos) algún tipo de figura... forma... tendencia.
Si vemos alguna figurita.. hay algún tipo de relación.                  \
Si no vemos figurita y solo desparrame de puntos... no hay relación.    / ESTO CON MUCHO CUIDADO
Ese diagrama nos puede mentir! ya que puede haber muchos puntos que se solapen... y no ver la figurita.
Por eso, en paralelo, usamos estadísticos... que si tienen en cuenta TODOS LOS SUJETOS.
- Coeficiente de correlación de Pearson (SE BASA EN LA MEDIA : si las distribuciones son simétricas)
- Coeficiente de correlación de Spearman (USA EL ORDEN DE LOS DATOS... me sirve si las distribuciones son asimétricas)
Ambos están entre -1 y 1
El signo SOLO ME INDICA LA DIRECCION DE LA RELACION:
    Directa: (+) que cuando el valor de una variable sube, el valor de la otra variable también suele subir
    Inversa: (-) que cuando el valor de una variable sube, el valor de la otra variable suele bajar
El valor absoluto (el numerito sin el signo) ME INDICA LA INTENSIDAD DE LA RELACION
    0.. NO HAY RELACION
    1.. ES QUE HAYA MUCHA RELACION... ES QUE SON LA MISMA VARIABLE! = RUINA! 
    Según sube ese número es que hay más relación entre las variables.

Estos estadísticos CUIDA. también. Porque también me pueden engañar.
Person solo busca si hay lineas RECTAS en el diagrama.
Spearman busca si hay monotonía LINEAS (aunque sean curvas) en el diagrama que o siempre suben o siempre bajan.

                                    *****************
              *****************
         *
     *
    *

---

> Fecha de nacimiento de una persona: Cuantitativo... la unidad de medida es DIA!

Es de INTERVALO! No hay 0
Puedo restar fechas? Sí
1-Enero-2000 es doble que el 1-Enero-1000? NO
Puedo calcular una media de fechas? SI

> Si de esa fecha extraigo el AÑO, MES, DIA
De que tipo es cada uno de esos datos?

AÑO: Cuantitativo de RAZÓN.
    - Nace en el año 1990 y se casa en el 2020. Cuantos años han pasado? 30 años.
MES: Nominal / Ordinal

DIA: Nominal / Ordinal


---

Hay una pandemia mundial, Dios no lo quiera!
Y saco una vacuna.
Se la pincho en el culo a 10 personas...
9 se curan. 1 no. < HALLAZGO CIENTIFICO o de NEGOCIO! LO QUE VEO .. y lo que veo es lo que veo!

Cómo lo veis?
LTengo pocos datos.. la muestra NO ES REPRESENTATIVA.. 
Pero... 9 de cada 10 personas se curan! > Tengo confianza en que esos datos vayan a mantenerse cuando pinche a 100.000.000 personas? NO, NI DE COÑA!
Tiro la vacuna entonces??? NI DE COÑA... Es PROMETEDORA !
Qué me hace falta? MAS MUESTRA! MAS DATOS!
HAsta cuando? Cuándo será suficientes datos? 200, 500, 1000??? Eso es lo que me dan las pruebas inferenciales!
Me dicen cuando tengo suficientes datos.

Estas pruebas me hablan de SIGNIFICACION ESTADISTICA.... SI ME LO TRAGO! o no tengo confianza aún... en base a la cantidad de datos que tengo!