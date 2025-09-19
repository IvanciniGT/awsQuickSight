
# Quicksight

La herramienta de BI de AWS.

## BI?  Business Intelligence?

Aplicar técnicas estadísticas (descriptivas) y de análisis de datos para mejorar la toma de decisiones en la empresa.
Y para ello nos ayudamos de distintos programas informáticos que nos facilitan el trabajo.

Lo que vamos a estar es manejando datos.
Estos programas clasifican los datos de acuerdo a su tipo: 
- Texto
- Números
- Fecha
- ...

Esto esta guay... desde un punto de vista de computación. Desde un punto de vista estadístico/de análisis de los datos es una RUINA!

Qué es eso de que un dato sea de tipo TEXTO o NUMERO? Esto tiene que ver con cómo la computadora va a gestionar/almacenar ese dato.
Las computadoras guardan textos? en su HDD? NO
Guardan números? NO
Guardan fechas? NO
Decimos que las computadoras hablan en lenguaje binario (0s y 1s). Esto es una patraña.
Entienden de estados duales. PUNTO PELOTA. Nosotros habitualmente los representamos con 0s y 1s. A efectos prácticos nos apañamos... con esa representación.

La mínima cantidad de información que se puede almacenar en un sistema que trabaja con estados duales es un BIT (Binary Digit).
En un bit cuantos datos puedo guardar? 1 dato. Que puede tener uno de 2 valores (0 o 1).
Qué significa el 0? La computadora no tiene ni idea... ni le interesa. Para mi, lo que me de la real gana.
Lo que pasa es que en muchos casos, queremos guardar datos que pueden tomar más de 2 valores posibles.
Entonces empezamos a juntar bits para tener formas de guardar datos que puedan tomar más valores diferentes.

1 bytes = 8 bits = 2^8 = 256 valores diferentes 

            ¿Qué significan?

            COLOR       Marca de coche  Número Entero   Número entero con signo     Caracter    Otra codificación
00000000    rojo        Toyota          0                   -128                        a           a
00000001    verde       Honda           1                   -127                        b           A
00000010    amarillo    Ford            2                   -126                        c           b  
00000011    azul        Chevrolet       3                   -125                        d           B
00000100    negro       BMW
...
11111111                                255                  127

El tipo de dato, lo que me ayuda es a explicitar el significado que quiero dar a cada uno de esos valores.
En el casos de los textos, puedo tener muchos JUEGOS DE CARACTERES. Muchos mapeos diferentes entre una representación binaria y un carácter. JUEGOS DE CARACTERES HABITUALES:
- ANSI: Usaba en total 7 bits para representar caracteres, lo que permitía 128 caracteres diferentes.
- ASCII: Utiliza 8 bits para representar caracteres, lo que permite 256 caracteres diferentes.
- ISO-8859-1: Utiliza 8 bits para representar caracteres, permitiendo 256 caracteres diferentes, incluyendo caracteres especiales de idiomas europeos.

Cuantos ocupa un carácter al guardarlo en un sistema informático? Depende del juego de caracteres.
Para juegos de caracteres que tengan un máximo de 256 caracteres: 1 byte.
Esos juegos de caracteres están limitados... Cuántos caracteres usa la humanidad? Están tabulados: > 160.000 caracteres diferentes. Se recogen en un estándar.. que va por versión 17: UNICODE
Ahora bien... tal cantidad de caracteres, puedo representarla con 1 byte? NO... solo 256 caracteres.
En 2 bytes? 2^16 = 256 * 256 = 65.536 caracteres... NO
En 4 bytes? 2^32 = 4.294.967.296 caracteres...      SÍ

Y existen distintas formas de codificar ese juego de caracteres llamado unicode... que es el que todo el mundo usa a día de hoy!
UTF-8       Usa entre 1 y 4 bytes por carácter. Es el más usado en internet.
UTF-16      Usa entre 2 y 4 bytes por carácter.
UTF-32      Usa 4 bytes por carácter.

> DNI Español: hasta 8 dígitos + letra.

  Qué tipo de campo necesito para guardarlo en una base de datos? TEXTO(9).
  Cuánto ocupa eso? Con un juego de caracteres como ASCII o ISO-8859-1 o UTF-8 : 1 bytes por carácter * 9 caracteres = 9 bytes.

  Otra alternativa? Número por un lado y la letra por otro
    - El número cuántos bytes necesitaría? 4 bytes.
    - Y la letra?                          1 byte.
    - TOTAL: 5 bytes.
  Acabo de meterle una reducción de tamaño al dato del 44% (de 9 bytes a 5 bytes).

  Hay más opciones... guardo solo el número y la letra la calculo a partir del número.
  El número me ocuparía solo 4 bytes... Y Acabo de reducir el tamaño del dato un 55% (de 9 bytes a 4 bytes).
  Eso si... cuando necesite la letra... he de calcularla.. y eso impacta en el tiempo de uso de CPU... y por ende en el gastos de energía y por ende €€€€.

  Opciones...

  Puede parecer una gilipollez. Pero si tengo 1M de DNIs... 5M de bytes = 5MB

  > Pregunta: El almacenamiento hoy en día es barato o caro?
  En una empresa, dentro del dpto de TI, el almacenamiento es LO MAS CARO QUE HAY.. con mucha diferencia!

    El problema es que para casa... si quiero un HDD de 2Tbs. Me voy al MediaMarkt y me cuesta 60€. WESTERN BLUE
    Un HDD de más calidad me puede incrementar el coste en un x5 - x20 NVME 2Tbs de Oracle -> 3600€
    Pero no es ni el principio del problema.
    El dato es lo más valioso que tiene la empresa! Con mucha diferencia. Y en un entorno de producción al menos hacemos 3 copias de cada dato. Si se jode un HDD, tengo 2 copias más. -> ALTA DISPONIBILIDAD
    Es decir que esos 2 Tbs que necesito, en la empresa se convierten en 3 HDD de 2Tbs.. Discos con un x10 en el precio... x 30 con respecto a lo que me cuesta a mi en casa.
    Pero ni hemos empezao.
    Ahora a esos datos les hacemos COPIAS DE SEGURIDAD -> RECUPERO DE DESASTRES
    Y como poco tendré copias de seguridad de las 2 últimas semanas. Si hago una copia de seguridad diaria, tengo 14 copias de seguridad.Cada una guardada por duplicado. x3 en espacio de almacenamiento x30 x 3 = x90
    Esos 2 Tbs que en casa me cuestan 60€, en la empresa me cuestan 5400€.


    Pero esto... es solo una parte del problema.
    Si los datos me ocupan el doble, además de gastar el doble de pasta en almacenamiento, voy a tardar:
    - El doble en leerlos del disco
    - El doble en transmitirlos por la red
    - El doble en subirlos a la RAM
    - El doble en procesarlos por la CPU
    - El doble en guardarlos en disco
    Y eso solo un dato. Empieza a meter columnas en una tabla... y tablas en una base de datos... y bases de datos en un sistema... y sistemas en un entorno de producción... y entornos de producción en una empresa... y la cosa se va de madre => SE CONVIERTE EN UN DESMADRE!

Pero claro... esto es desde el punto de vista de COMPUTACIÓN (INFORMÁTICO)... y tiene impacto directo en €€€€€ y el tiempo!

Pero desde el punto de vista estadístico... esto me la trae al peiro!

Desde el punto de vista estadístico hablamos de datos:
- CUALITATIVOS
  - Norminales
  - Ordinales
- CUANTITATIVOS (Cantidad) Los datos numéricos son cuantificables? NO NECESARIAMENTE. Para que un dato sea cuantificable necesita tener una UNIDAD DE MEDIDA! Al menos para que esa cuantificación tenga sentido

    CP                                             Portal 17
    21000                                                 23
    19870                                               -----
  + -----                                                 40 De media vivimos en el número 20 de la calle!
    40870  ?? Tiene esto sentido? Ninguno

Nivel de satisfacción de mis clientes: 0-10
Puedo calcularles una media? NO Matemáticamente si... son números.. conceptualmente es un disparate!
Podré calcular una mediana! ESO SI!
0 = Muy insatisfecho
9 = Casi muy satisfecho
10 = Muy satisfecho

Del 1 al 5 cuanto le duele! Le importa a la enfermera/o mi respuesta? Para darme más o menos medicina?
LE VALE MIERDA !
Lo único que le importa es la diferencia de ese dato con respecto a la siguiente vez que me pregunta... Para saber si siento más o menos dolor que antes. Esa medida es totalmente subjetiva. 

De hecho, desde un punto de vista de computación: "TODO" DEBERIAN SER NUMEROS en un conjunto de datos.
Pero si tengo 2300 sucursales:
Las tendré codificadas, con un número... que me ocupa muy poquito espacio... y lo muevo muy rápido. Al menos mucho más rápido que si fuera un texto.

TODO (lo que tenga sentido) lo ideal es que sea un número. Lo convertiré a números.

MADRID              0
VALENCIA            1
CATALUNYA           2
ANDALUCIA           3
---

Cualitativos 
    Nominales (NOMBRE/CATEGORIAS/MODALIDADES)
        - Sexo: Hombre, Mujer
        - Género: Hombre, Mujer, No binario...
        - País: ESP, FRA, ITA, USA...
        - Color Ojos: Azul, Verde, Marrón...
          > Para que sirve esto? Clasificar datos en grupos.
    Ordinales (ORDEN)
        - Nivel Satisfacción: 0-10
        - Nivel de estudios: Sin estudios, Primarios, Secundarios, Universitarios...
          > Para que sirve esto? Clasificar datos en grupos (ya que una escala ordinal por definición es a su vez nominal) y además establecer un orden entre esos grupos.
Cuantitativos: (Cantidades: 1 hijo, 3 hijos, 14 hijos...)
    Toda escala cuantitativa por definición es ordinal... y a su vez nominal.
    Por ende, estos datos puedo: 
        - Clasificarlos en grupos (Nominal)
        - Ordenarlos (Ordinal)
        - Hacer operaciones matemáticas con ellos (Cuantitativo)
    2 clasificaciones paralelas entre si:
            En base a la representación:
            - Discretos: Valores enteros. No pueden tomar valores intermedios.
               Número de hijos de una familia?
            - Continuos: Valores decimales. Pueden tomar valores intermedios.
               Peso de los conejos de una granja? 
            En base al 0: 
            - De razón: Tienen un 0 absoluto. 
              Número de hijos de una familia?
              2 hijos
              4 hijos
              Puedo decir que entre ambas tiene 6 hijos? SI                 +
              Puedo decir que una tiene 2 hijos menos que la otra? SI       -
              Puedo decir que una tiene el doble de hijos que la otra? SI   *
              O la mitad de hijos que la otra? SI                           /
            - De intervalo: Tienen un 0 arbitrario. El 0 es un simple valor más.
              Temperatura medida en 0ºC
              0º es un valor absoluto? O puede haber temperaturas por debajo de 0º?
              Bilbao: -10ºC
              Sevilla: 20ºC 
              Puedo decir que Sevilla tiene 10ºC más que Bilbao? SI                 
              Puedo decir que Bilbao tiene 10ºC menos que Sevilla? SI               -
              Puedo decir que entre ambas tienen 30ºC? NO ES CORRECTO!              +
              Puedo decir que Sevilla tiene el doble de temperatura que Bilbao? NO ES CORRECTO! * /
    

> Para que leches vale la estadística descriptiva?

Para entender los datos.
Y OJO AQUÍ: TENER LOS DATOS ES MUY DIFERENTE DE ENTENDER LOS DATOS!
5000 nóminas!

La estadística descriptiva nos ofrece técnicas para RESUMIR ESOS DATOS... con el fin de entenderlos mejor.
La forma más básica es con tablas de frecuencias.

                                  Cuántos (FRECUENCIA ABSOLUTA)  Frecuencia Relativa (%)

    Sin estudios                    100                             2%
    Primarios                       500                            10%      
    Secundarios                     2000                      
    Grado                           1500
    Universitarios superiores       800
    Master                          80
    Doctorado                       20
    Total                           5000


    Frecuencia 
                ^
                |
                |                        XX
                |             XX         XX
                |. XX         XX         XX
                |. XX         XX         XX
                +---------------------------------------------------------------------------------- NIVEL DE ESTUDIOS
               Sin estudios Primarios Secundarios Grado Universitarios superiores Master Doctorado


Esto mismo lo podría hacer con los salarios? Poder podría... pero sería un disparate...
Cuántas filas iba a tener esa tabla? Cerca de 5000 filas... cada persona tiene un salario diferentes.. pocos se repiten. Me ayuda esto a entender mejor los datos? NO

Una cosa que podría hacer es calcular una variable nueva a partir de la variable salario:
NIVEL SALARIAL/ RANGO SALARIAL

    Rango Salarial                Frecuencia Absoluta       Frecuencia Relativa (%)     ACUMULADOS
    0-1000                              500                           10%                500    10%
    1001-2000                           1500                          30%               2000    40%
    2001-3000                           2000                          40%               4000    80%
    3001-4000                           700                           14%               4700    94%
    4001-5000                           200                           4%
    5001-6000                           50                            1%
    6001-7000                           30                            0.6%
    7001-8000                           15                            0.3%
    8001-9000                           5                             0.1%
    9001-10000
    >10000

     ^^^^
     ORDINAL


     Los acumulados solo tienen sentido si hay un ORDEN en los datos!

    Comunidad autónoma
                        Sucursales          Acumulado
        País Vasco          700                 40% 40%
        Madrid              500                 30% 70%
        Cataluña            400                 25% 95%  <<<< Entre las 3 comunidades 
        Andalucía           300                                 en las que tengo más sucursales 
        Murcia              100                                 suman el 95% de las sucursales

    Esto es lo más básico... esas tablas las puedo representar como gráficos:
    - Barras                En lugar de pintar la barra entera... unir las puntas con una linea (GRÁFICO DE LINEAS)
      - Medidas absolutas           Puedo hacer eso mismo y colorear lo de abajo... (GRÁFICO DE ÁREAS)
      - Medidas relativas
    - Sectores  
      - Medidas relativas

A una variable cualitativa le puedo dibujar gráficos de barras o sectores.
Las tablas de frecuencias las calculo usando el poder clasificatorio de las variables nominales (y que heredan las ordinales y cuantitativas).

Cómo represento una variable cuantitativa?
- Histograma (Se parece al de barras.. pero tienen su diferencia)

            FRECUENCIA
            ^
            |
            |.     XXXXXXXXXXXXX
            |.    XXXXXXXXXXXXXXXX
            |.   XXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXX
            |.  XXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXX. XXX.    X
            +---|-------|-------|--------|-----------------------|---|---|----> SALARIO
            0  1000    2000    3000    4000    5000    6000    7000    8000    9000   10000

- Boxplot (Diagrama de caja y bigotes)
  - Histograma + Boxplot = Violin Plot

Este es un primer resumen que nos ofrece la estadística.

La estadística descriptiva nos ofrece herramientas para resumir aún más la información:
Podemos llegar a resumir toda la información de una variable en un único número/dato: INDICADOR / ESTADÍSTICO 
- Medidas de tendencia central: "Me informan de por donde va los tiros" "En torno a qué valor se concentran los datos"
    - Moda: Es el valor que más se repite... el que está de "moda".
            Además, podemos calcular la moda desde la tabla de frecuencias.
            Podemos calcular una moda a cualquier tipo de variable.
            Una peculiaridad es que una variable puede tener varias modas, varios valores que se repiten con la misma frecuencia máxima (o parecidas)
    - Mediana: Atiende a un concepto más sencillo. Es el valor que divide en 2 grupos del mismo tamaño (más o menos.. lo mejor que se pueda) al conjunto de datos.
              Para calcularla, primero ordeno los datos de menor a mayor y luego tomar el que valor que está en el medio.

                    IMPAR: Salarios:
                                ****
                    1000, 1200, 1500, 1800, 2000
                    La mediana es 1500
                    En este caso, tengo un grupo con los que ganan menos de 1500 (2)
                    Y los que ganan a partir de 1500 (3)

                    PAR: Salarios:
                                ***********
                    1000, 1200, 1500, 1800, 2000, 2200
                    La mediana es (1500 + 1800) / 2 = 1650 MEDIANA

    - Media: ES MUY COMPLEJA DE INTERPRETAR! Entre otras cosas porque atiende a una definición matemática.
              Sumas todos los valores y los divides entre el número de valores.
              Representa la contribución que haría cada sujeto al total si todos contribuyeran por igual.
              El problema es que cuando vemos una media solemos pensar que todos los sujetos tienen un valor cercano a esa media... y esto no tiene porqué ser cierto. De hecho puede que ningún sujeto tenga un valor ni remotamente cercano a esa media.
              ADEMAS, LA MEDIANA PUEDE SER UNA MENTIROSA! Hay que tener mucho cuidado.


            > Villa arriba de arriba!
                10 vecinos... coches.. Los coches echan diariamente CO2

                10  5    10    15    5    10    15   5  10   15
                ORDENADOS: 5   5    5     10    10   10   10    15   15    15

                    ^
                    |               X
                    |       X       X       X
                    |       X       X       X
                    |       X       X       X
                    +-------------------------------------------------> gCO2/Dia
                    0       5       10      15
                                MEDIANA
                               (^ MEDIA )

                MEDIANA: 10 gCO/Dia
                MEDIA?:  (5+5+5+10+10+10+10+15+15+15) / 10 = 10 gCO2/Dia

                Media y Mediana son iguales.

            > Villa arriba de abajo!

                10 vecinos... pero! Están muy sensibilizados con el medio ambiente.
                Se compraron todos el mismo coche eléctrico... menos Manolo... 

                    5   5    5     5    5    5    5     5    5    1000

                MEDIANA: 5     gCO2/Dia
                MEDIA?:  104,5 gCO2/Dia <- Este dato no es representativo del pueblo.
                                          No me ayuda a entender los datos. OJO ES UN DATO REAL!

                    ^
                    |   x
                    |   X 
                    |   X
                    |   X
                    |   X                                                                  M
                    +--------------------------------------------------------------------------> gCO2/Dia
                    0   5                    104,5                                        1000    
                        ^
                        MEDIANA
                                            (^ MEDIA )

                La media quiere estar con la mediana.. pero los valores extremos tiran mucho de ella

                VAYA DESPARRAME!
                La media es muy muy sensible a la presencia de datos extremos.
                Pero lo cierto es que para determinar si uso una media o una mediana como medida de tendencia central, me fijo no en la presencia de datos extremos, sino en la ASIMETRÍA/SIMETRÍA de la distribución de los datos.
                Cuando tengo datos que se distribuyen de forma simétrica, la media es un buen indicador de tendencia central.
                Cuando tengo datos que se distribuyen de forma asimétrica, la mediana es más representativa del colectivo.

                                                        ^
                                                        |   x
                                                        |   X 
                                                        |   X
                                                        |   X
          G                                             |   X                                             M
        <----------------------------------------------------------------------------------------------------------> gCO2/Dia
         -955                                           0   5                                           1000    
                                                          MEDIANA
                                                   <---- (^ MEDIA ) ---->

    En estadística decimos que la mediana es un indicador ROBUSTO (resistente) puesto que no está muy afectada por la presencia de datos extremos. Por contra decimos que es un indicador NO SUFICIENTE, ya que para su cálculo no se tienen en cuenta todos los datos.

    La MEDIA es un indicador NO ROBUSTO (sensible) ya que está muy afectada por la presencia de datos extremos. Por contra decimos que es un indicador SUFICIENTE, ya que para su cálculo se tienen en cuenta todos los datos.

    En este caso, la decisión es muy clara.. pero el ejemplo era muy extremo!
    En la realidad los datos no se distribuyen de formas tan extremas... y hay que aplicar un poco de sentido común.
    Muchas veces, calculamos las 2.
    Si se diferencian entre si mucho, tiraré de mediana.
    Si no se diferencian mucho, tiraré de media.
    La pregunta puede ser , Cuánto es mucho? Y la respuesta de nuevo sentido común.
    Si estoy hablando de número de hijos... y la media es 2,2 y la mediana 2... no me complico la vida.
    Si estoy hablando del precio de los cliches en las tienda en función del año ... Una diferencia de 5 céntimos puede ser mucho... relativo al precio de lo que es un chicle
    Si estoy hablando de salarios... una diferencia de 5 céntimos... es nada!

Dicho esto... NUNCA JAMAS EN LA VIDA pondré / entregaré una MEDIDA DE TENDENCIA CENTRAL sin poner SU MEDIDA DE DISPERSIÓN = CAGADA ! Igual que pegar a un padre con un calcetín sudao! NO SE HACE !
Y esto de nuevo puede inducir a malas interpretaciones.

Por qué?

    PORTAL 1: 4 personas
        165cms 170cms 170cms 175cms
                MEDIA: 170cms
                MEDIANA: 170cms
          -5cm.   0cm.   0cm.  +5cm     Lo que cambian con respecto a la media... Y Si lo quiero mirar groso modo?
                                        Podría calcular la media de esos valores.
                                         RESULTADO = 0cm 
     ABS.  5cm     0cm    0cm  5cm       DESVIACION MEDIA = 2.5cm
     ^2.   25cm2   0cm   0cm  25cm2      VARIANZA = 12.5cm2
                                         RAIZ VARIANZA = 3.54cm = DESVIACION TIPICA
                    1 desv. tipica alrededor de la media:  166.46cm - 173.54cm
    PORTAL 2: 4 personas
        160cms 160cms 180cm  180cm
                MEDIA: 170cms
                MEDIANA: 170cms
        -10cm.  -10cm.  +10cm.  +10cm   
                                         RESULTADO = 0cm
      ABS.  10cm   10cm   10cm  10cm     DESVIACION MEDIA = 10cm
        ^2.   100cm2 100cm2 100cm2 100cm2 VARIANZA = 100cm2
                                         RAIZ VARIANZA = 10cm = DESVIACION TIPICA
                    1 desv. tipica alrededor de la media:  160cm - 180cm
    PORTAL 3: 4 personas
        150cms 155cms 185cm  190cm
                MEDIA: 170cms
                MEDIANA: 170cms
        -20cm.  -15cm.  +15cm.  +20cm   
                                             RESULTADO = 0cm
        ABS.  20cm   15cm   15cm  20cm     DESVIACION MEDIA = 17.5cm
        ^2.   400cm2 225cm2 225cm2 400cm2 VARIANZA = 312.5cm2
                                                RAIZ VARIANZA = 17.68cm = DESVIACION TIPICA
                    1 desv. tipica alrededor de la media:  152.32cm - 187.68cm
    PORTAL 4: 4 personas
        170cm 170cm 170cm 170cm
                MEDIA: 170cms
                MEDIANA: 170cms
        0cm.   0cm.   0cm.   0cm           
                                             RESULTADO = 0cm
        ABS.  0cm    0cm    0cm   0cm      DESVIACION MEDIA = 0cm
        ^2.   0cm2   0cm2   0cm2  0cm2     VARIANZA = 0cm2
                                                RAIZ VARIANZA = 0cm = DESVIACION TIPICA
                    1 desv. tipica alrededor de la media:  170cm - 170cm

    PORTAL 5: 4 personas
        150cm 160cm 180cm 190cm
                MEDIA: 170cms
                MEDIANA: 170cms
        -20cm.  -10cm.  +10cm.  +20cm   
                                             RESULTADO = 0cm
          ABS.  20cm   10cm   10cm  20cm     DESVIACION MEDIA = 15cm                                             
        ^2.   400cm2 100cm2 100cm2 400cm2 VARIANZA = 250cm2
                                                RAIZ VARIANZA = 15.81cm = DESVIACION TIPICA
                    1 desv. tipica alrededor de la media:  154,2cm - 185,8cm
    PORTAL 6: 4 personas
        150cms 170cms 170cm  190cm
                MEDIA: 170cms
                MEDIANA: 170cms
        -20cm.   0cm.   0cm.  +20cm   
                                                RESULTADO = 0cm
       ABS.  20cm   0cm    0cm  20cm     DESVIACION MEDIA = 10cm
        ^2.   400cm2 0cm2   0cm2 400cm2 VARIANZA = 200cm2
                                                RAIZ VARIANZA = 14.14cm = DESVIACION TIPICA
                        1 desv. tipica alrededor de la media:  155,8cm - 184,2cm

Por esto no puedo ofrecer solo una medida de tendencia central. SERIA ENGAÑOSO! Y MI OBJETIVO, REPITO es AYUDAR A ENTENDER LOS DATOS!

Medidas de dispersión: Nos ayudan a saber CUANTO CAMBIAN LOS SUJETOS CON RESPECTO A LA MEDIDA DE TENDENCIA CENTRAL QUE ESTEMOS USANDO. Es decir, cuando cambian las cosas con respecto al "por donde van los tiros"


Cómo interpreto una desviación típica?

    Salario de la empresa es de 2780€/mes con una desviación típica de 300€/mes.. Cómo interpreto esto?
    Esto no significa que la gente gana entre 2480 y 3080€/mes. NOOOO!!!!
    Significa que la mayoría están ahí... Y mayoría significa al menos el 50% de los sujetos.
    Además la mayor parte más CENTRADA / REPRESENTATIVA de los sujetos.
    Eso nos lo dice la regla de Chebyshev.

Es guay la desv. típica.
PERO... su cálculo se basa en? LA MEDIA...
Y Si la media no era representativa del colectivo? PUES LLA VARIANZA O LA DESV. TÍPICA TAMPOCO LO SERÁN! = RUINA !
La dev. típica solo la ofrecemos cuando la media es la medida de tendencia central que hemos decidido usar, por ser la más representativa del colectivo.
Pero si en lugar de la media, decido usar la mediana (Q2)... la desviación típica no sirve. En ese caso tenemos otra medida: RANGO SEMIINTERCUARTILICO = (Q3 - Q1) / 2
La interpretación es similar a la de la desviación típica.
Abriendo un rango semintercuartílico alrededor de la mediana, tenemos entorno al 50% de los sujetos más representativos del colectivo.

---

# Medidas de posición

Nos ayudan a saber cuántos sujetos se sitúan por debajo de un valor determinado.
Nos ayudan a saber el valor que deja por debajo a un determinado grupo de sujetos.
Percentiles: Hay 99 percentiles (P1, P2, P3... P99)
             Son los valores que dejan por debajo a un % determinado de sujetos.
            
Deciles: Hay 9 deciles (D1, D2, D3... D9)
        Son los valores que dejan por debajo a un 10% determinado de sujetos.
Quartiles: Hay 3 cuartiles (Q1, Q2, Q3)
          Son los valores que dejan por debajo a un 25% determinado de sujetos.
Mediana:  Deja por debajo al 50% de los sujetos... a la mitad..
    Anda.. entonces la mediana = Q2 = D5 = P50

Los podemos calcular fácil desde las frecuencias acumuladas.

# GRAFICO CAJA Y BIGOTE / BOXPLOT

                                    Q3-Q1 = RANGO INTERCUARTILICO
                                    Contiene al 50% de los sujetos más representativos
                                <------------------------>
                                            ------------->
                                            Rango semiintercuartílico = (Q3-Q1) / 2
            MINIMO                                                                         MAXIMO  
          "razonable"           Q1             Q2       Q3                               "razonable"
    --------V-------------------V--------------V--------V------------------------------------V-----------> VAR.

            |                   +--------------+--------+                                    |
            |                   |              |        |                                    |
            |-------------------+              |   o    +------------------------------------|     xx    x
            |                   |              |  MEDIA |                                    |
            |                   +--------------+--------+                                    |

            <------------------> <-------------><-------><----------------------------------->
              En este intervalo      25%           25%               25%
              de valores tengo 
            un 25% de los sujetos

                                                        <-----------------------------------> = 1.5 veces el RIC

                                                                                                   xx      x

                                                                            Los valores que quedan fuera de ese rango se consideran "atípicos" o "outliers"
                                                                            LOS MANOLOS y LAS GERTRUDIS
---

BBDD
  Almacén donde vamos guardando datos. Normalmente datos VIVOS, que son gestionados por apps que tenemos 
  en el entorno de producción de nuestra empresa.
  - Relacionales (SQL Server, Oracle, PostgreSQL...)
  - NoSQL (Not Only SQL):
    - Jerárquicos (MongoDB, Couchbase...)
    - Documentales (Alfresco, CouchDB...)
    - Grafos (Neo4j, ArangoDB...)
    - ...
        |
       ETLs (Extract, Transform, Load)
        |           ELT (Extract, Load, Transform)
        |           TETL 
        |           TELT
        V           ...
DataLake               Almacén de datos muertos... en crudo, sin procesar. 
                       Una extracción en bruto de lo que tenía en los entornos de producción.
        |
       ETLs (Extract, Transform, Load)
        |           ELT (Extract, Load, Transform)
        |           TETL 
        |           TELT
        V           ...
DataWarehouse           Almacén de datos muertos procesados y estructurados, optimizados para un uso concreto!
                            - Análisis de datos (Modelos de datos en estrella, Snowflake)

Big Data                Cómo planteo el trabajo con datos cuando las técnicas que hemos estado usando durante décadas
                        han dejado de ser útiles/eficientes/válidas, sea para lo que sea que quiera hacer con los datos:
                          - Analizarlos
                          - Almacenarlos
                          - Transmitirlos
                        Cuando tengo un volumen tan grande de datos
                        o Genero datos tan rápido
                        o Son tan complejos
                        que las técnicas tradicionales ya no son suficientes, BIG DATA es una alternativa.

    > Pregunta 1: Tengo un pincho USB de 16Gbs... vacío... recién sacado del paquete.
    Tengo una película de 5Gbs. Puedo meterla dentro? DEPENDE del formato del pincho USB.
        FAT16: NO. Me permite archivos de 2Gbs máximo.
        NTFS
        ZFS
        EXT4
    Y si tengo un archivo de 7Pbs... y ahora qué?

    > Pregunta 2: Quiero hacer la lista de la compra: Producto/Cantidad
            - 100 cosas:                 Bloc de notas
            - 1000 cosas:                Excel
            - 100000 cosas:              MySQL
            - 10000000 cosas:            SQL Server
            - 1000000000 cosas:          Oracle
            - 100000000000000 cosas:     ???

    > Pregunta 3: Juegos de teléfonos móvil. 2v2
         En un segundo quizás yo hacía unos 2 movimientos -> 6 mensajes/segundo
         Estamos jugando 4 jugadores -> 24 mensajes/segundo
         50.000 partidas simultáneas -> 1.200.000 mensajes/segundo

---

ANÁLISIS DE DATOS (ESTADISTICA)
    - Estadística descriptiva - Entender los datos
    - Estadística inferencial (+ Incorporación de la teoría matemática de la probabilidad)
      - Predecir datos
Business Intelligence
   Aportar información para mejorar la toma de decisiones en la empresa. Toma de decisiones informada.
   Básicamente es aplicar técnicas estadísticas (nivel instituto) sobre colecciones de datos que tengo.
   Está bien... cuando quiero buscar relaciones entre datos... 2... como mucho 3...  y ya no me da el cerebro.
Data Mining             Identificación de relaciones/Patrones complejas (que son descubiertas por computadores)
Machine Learning        Algoritmos que aprenden de los datos y son capaces de hacer predicciones.
    Deep Learning       Con algoritmos complejos de redes neuronales multilayer (muchas capas)


---

Dato / Información.

Peso de una persona: MANOLO "140Kgs" <- DATO
Qué información lleva ese dato?
- Peso
- Estado salud (Probablemente jodido)
- Edad (>15 años)
- Talla de ropa (>4XL )
- Hace deporte (con poca probabilidad)
- Estatura (>1.50m)
