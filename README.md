# REPORTE
## PUNTO 1: FUNCIONES UTILES:
Para esta actividad era necesario crear dos funciones, una que eliminara elementos de una lista por fuera de un intervalo, y otra que ordene flotantes en orden descendiente.

### Eliminar elementos:

Para eliminar elementos, se decidió que el programa tomara la lista inicial, y creara otra lista con los elementos que cumplieran con la condición de que fueran menores que el límite superior, y mayores que el límite inferior.
Para conseguir esto se crearon dos funciones; la primera, llamada miFilter(se nombró así para que el programa no se confunda con la función filter, que ya está establecida en Haskell), recibe una función que devuelve un booleano y una lista de tipo float, y devuelve una lista del mismo tipo. Esta función revisa si el primer elemento de la lista al aplicársele la función booleana devuelve verdadero, si si, entonces este elemento se convierte en el primer elemento de la lista de salida, y el cuerpo de la lista llama recursivamente la función, añadiendo elemento por elemento hasta vaciar la lista, lo cual es la condición de stop que regresa una lista vacía. En caso de que la función booleana devuelva falso, el elemento x no se incluye en la salida, sino que se llama otra vez a la función directamente.
La segunda función simplemente toma la lista, un límite inferior y un límite superior; y simplemente usa la función de filtro tomando como parámetro la función  (\x -> x >= lower && x <= upper), que revisa si x es mayor que lower(límite inferior) y menor que upper(límite superior).

### Ordenar lista:

Para ordenar una lista en orden descendiente, se creó una función llamada "insertDesc" que toma un número y una lista ya ordenada, y revisa si el elemento individual es mayor al primer elemento de la lista(que, al estar ya ordenada, es el mayor), si este es mayor, se pone al inicio, y si no, se llama recursivamente a la función con el cuerpo de la lista, hasta que sea mayor a algún elemento.
Luego en la función de ordenDesc, se toma el primer elemento de una lista de flotantes que se pasa como argumento y se usa el inserDesc con resultado del cuerpo de la lista al pasar por la misma ordenDesc llamada recursivamente hasta vaciar la lista, de modo que se usa el inserDesc con todos los elementos.

### Resultados de las pruebas:

a remData se le pasaron [1,9,3,7,2,6,4,8,5,10], 2 y 6 como argumentos, y el programa devolvió [3.0,2.0,6.0,4.0,5.0]; y a orderDesc la lista de flotantes [3.8,1.2,5.1,2.7,5.4], y devolvió [5.4,5.1,3.8,2.7,1.2].

### Dificultades y soluciones:
En primer lugar, como no teníamos experiencia en usar funciones que tomen otras funciones como argumento, por lo cual se vio este video https://www.youtube.com/watch?v=7JK6qtpKLoQ&t=107s, en el cual aprendimos sobre las funciones como argumento y sobre la notación lambda, que fueron usados en nuestro código. Luego de esto no experimentamos más dificultades. Un problema que estábamos teniendo era con los condicionales, que originalmente hicimos usando |, como se explicó en la clase, no obstante, por motivos que después aprendimos que eran por identación, el código no nos estaba funcionando, por lo que decidimos hacerlo con "if", "then" y "else".

## Punto 2: Métodos numéricos
Se tenía que hacer funciones para aproximar la función exponencial, el coseno y el logaritmo natural.
En las 3 se tuvo que crear una función factorial, que multiplica recursivamente un numero por su anterior, hasta llegar a 0 donde es igual a 1. También las 3 usaron la función de error porcentual, que reemplaza en la fórmula de error porcentual los valores de nuestras funciones como el valor experimental, y el valor de las funciones de haskell como el teórico.

### Función exponencial:

La función exponencial toma un número que es el que se quiere tomar como x, que en la función se llama m, y otro que es la precisión del cálculo.
Se usa una función recursiva donde se aplica la formula dada a m tomando la precisión dada como N, después se suma recursivamente con la misma fórmula tomando a N-1, hasta llegar a N=0, donde la formula siempre es igual a 1. Luego se toma el resultado y se usa en la función de error porcentual.

### Función coseno:

De forma similar, toma dos números, m y la precisión n. Después, para cada enero k de 0 a n, se aplica la formula dada tomando m como x y k como n, y se suman todos los resultados para todos los valores de k. Finalmente se usa la función de error porcentual con el resultado obtenido y la función cos de Haskell.

### Función de logaritmo natural:
El proceso fue casi igual al del coseno; la función toma dos números, m y la precisión n. Después, para cada enero k de 0 a n, se aplica la fórmula para el logaritmo natural tomando m como x y k como n, y se suman todos los resultados para todos los valores de k. Finalmente se usa la función de error porcentual con el resultado obtenido y la función log de Haskell.

### Resultados de las pruebas:
Para la función exponencial se hizo 
main :: IO()
main =   do
    print(euler 5 15)
    print(exp(5))
    print(ep 5 15).
Que devolvió 
148.3796
148.4131591025766
2.2618841e-2

Luego se usó 
main :: IO()
main =   do
    print(euler 5 3)
    print(exp(5))
    print(ep 5 3)
Que devolvió 
18.5
148.4131591025766
87.5348.
Con un error porcentual demasiado grande, debido a la baja precisión.
En la función coseno se usó
main :: IO()
main =do
    print(cose (3 ) 25)
    print(cos(3 ))
    print(ep (3 ) 25)
que retornó
-0.9899924966004455
-0.9899924966004454
1.1214458982644546e-14
y después
main :: IO()
main =do
    print(cose (3 ) 2)
    print(cos(3 ))
    print(ep (3 ) 2)
Que retornó
-0.125
-0.9899924966004454
87.37364167615009
También con un error porcentual grande.

Finalmente, el logaritmo natural se probó con
main :: IO()
main =do
    print(logn (0.5 ) 25)
    print(log(0.5 ))
    print(ep (0.5 ) 25)
Que retornó
-0.6931471794534005
-0.6931471805599453
1.5964066157325645e-7

y con 
main :: IO()
main =do
    print(logn (0.5 ) 2)
    print(log(0.5 ))
    print(ep (0.5 ) 2)
Que retornó
-0.625
-0.6931471805599453
9.831559944439784
Que, si bien aún tiene un error porcentual relativamente bajo, es mucho menos precisa que cuando se le da una precisión alta

| Función       | Parámetros (x, n) | Valor aproximado (nuestra función) | Valor real (Haskell) | Error porcentual |
|---------------|------------------|-------------------------------------|----------------------|------------------|
| **Exponencial** | (5, 15) | 148.3796 | 148.4131591025766 | 2.2618841e-2 |
| **Coseno**      | (3, 25) | -0.9899924966004455 | -0.9899924966004454 | 1.1214458982644546e-14 |
| **Logaritmo**   | (0.5, 25) | -0.6931471794534005 | -0.6931471805599453 | 1.5964066157325645e-7 |

### Dificultades y soluciones
Se tardó mucho en hacer la función coseno, pues originalmente se veía
factor:: Float -> Float
factor 0 = 1
factor x = x* factor (x-1)
cose:: Float -> Float -> Float
cose m 0=0
cose m n=(((-1)**(n-1))/(factor (2*(n-1))))*(m**(2*(n-1))) + cose m (n-1)
Lo cual no funcionaba. Tras consultar, la causa del error parece haberse debido a asuntos como las aproximaciones o el tipo de datos. Luego de lo cual se corrigió a:
cose :: Float -> Float -> Float
cose m 0 = 0
cose m n =
    (((-1.0) ** (n - 1)) / factor (2.0 * (n - 1))) *
    (m ** (2.0 * (n - 1))) + cose m (n - 1)
Que usaba exclusivamente floats;  no obstante, seguía sin funcionar, por lo cual se decidió estudiar más Haskell, finalmente, llegamos al video de https://www.youtube.com/watch?v=bc3_yZEAC_0, que ofrecía una opción diferente a la recursión para resolver el problema, siendo la compresión de listas (|k<-), y se consultó además sobre varias funciones fundamentales, como sum y fromInteger, y sobre tipos de datos como Float y Double; con lo cual se obtuvo el resultado final. Lo curioso es que, luego de volver a probar las primeras versiones descartadas del código, estas funcionaron sin error alguno, con lo cual no entiendo por qué al principio estaban retornando valores incorrectos; sin embargo, ya se había construido el código con compresión y sumatoria, que se prefirió por su mayor precisión. el fromIntegral también se añadió en un intento de solucionar los problemas iniciales.
Originalmente tampoco se pudo hacer la función logaritmica, pues en la fórmula de la guía la sumatoria empieza con n=0, con lo cual da un resultado infinito, por eso es espero a la clase para que el profesor clarificaba que debía empezar con n=1.
También había problemas con el error porcentual, pues con la función coseno a veces daba un resultado negativo, devido a que el coseno de ciertos números lo es. Esto se solucionó aplicando valor absoluto a todos los componentes de la división, para que el resultado sea siempre positivo.

## Punto 3: transformación discreta de coseno:

Primero se hizo una función para definir el valor de a(k) según se nos dio en la formula, que recibe el valor de k y el tamaño de la lista. Definiendo a(k) según si el valor de k es 0 o no. Luego, se tiene otra función llamada dctK que aplica la formula a cada elemento individual de la lista, recibiendo como entrada la lista y el elemento. Para esto, se crean dos variables, una que es el valor de a(k), y otra que es el resultado del resto de la operación, para después multiplicarse la una con la otra.
La última función toma como entrada la lista, y usa map para pasar todos los elementos por dctK, para así devolver una nueva lista con los resultados de la transformación.

### Resultados de las pruebas:
Se pasó como entrada la lista [1,2,3,4,5,6,7,8,9,10], y el programa devolvió [17.392527130926087,-9.024851126140828,-3.1776437161565094e-15,-0.9666569027727293,-7.944109290391273e-16,-0.3162277660168405,-1.9860273225978185e-15,-0.12787039268579026,2.383232787117382e-15,-3.5857300383882226e-2], que es el resultado que indica el ejemplo de la guía, por lo que podemos asumir que está bien.

### Dificultades y soluciones:
El primer problema al que nos enfrentamos era que necesitábamos tanto el elemento de la lista como su índice. La primera solución que dimos era hacer que, a la hora de hacer la sumatoria, la función pase por cada elemento de la lista, mientras aumente un contador para usar como índice del elemento. Sin embargo, como las funciones en haskell son inmutables, no sabíamos cómo hacer un contador, o si siquiera era posible. Por esto, una segunda solución fue usar el !!, que busca un elemento en una lista en un índice determinado, de modo que la sumatoria puede hacerse iterando por los enteros del 0 a n-1(los índices), y usando el !! para saber qué valor se asocia a cada índice.

# Conclusiones:
Esta práctica nos ayudó a solidificar nuestros saberes de haskell al darnos un espacio en el cual debíamos aplicar todos los conceptos adquiridos en clase, además de consultar y aprender conceptos nuevos sobre el lenguaje. De esta manera, aprendimos a escribir un código que no solo resulta mucho más eficiente, sino más conciso e incluso estético, en comparación a como se haría en lenguajes más tradicionales como java o Python. 
El uso de la programación funcional también nos obligó a pensar los problemas de una forma diferente, no tanto en el paso a paso para resolver un problema, sino en QUE ES el problema que debemos resolver, lo cual consideramos una perspectiva bastante sofisticada que intentaremos aplicar en la medida de lo posible en el futuro a la hora de aplicar problemas matemáticos.
