# REPORTE
## PUNTO 1: FUNCIONES UTILES:
Para esta actividad era necesario crear dos funciones, una que eliminara elementos de una lista por fuera de un intervalo, y otra que ordene flotantes en orden desendiente.

### Eliminar elementos:

Para eliminar elementos, se decidió que el programa tomara la lista inicial, y creara otra lista con los elementos que cumplieran con la condición de que fueran menores que el limite superior, y mayores que el limite superior.
Para conseguir esto se crearon dos funciones; la primera, llamada miFilter(se nombró así para que el programa no se confunda con la funcion filter, que ya está establecida en Haskell), recibe una función que devuelve un booleano y una lista de tipo float, y devuelve una lista del mismo tipo. Esta función revisa si el primer elemento de la lista al aplicarsele la función booleana devuelve verdadero, si si, entonces este elemento se convierte en el primer elemento de la lista de salida, y el cuerpo de la lista llama recursivamente la función, añadiendo elemento por elemento hasta vaciar la lista, lo cual es la condición de stop que regresa una lista vacía. En caso de que la función booleana devuelva falso, el elemento x no se incluye en la salida, sino que se llama otra vez a la función directamente.
La segunda función simplemente toma la lista, un limite inferior y un limite superior; y simplemente usa la función de filtro tomando como parametro la función  (\x -> x >= lower && x <= upper), que revisa si x es mayor que lower(limite inferior) y menor que upper(limite superior).

### Ordenar lista:

Para ordenar una lista en orden desendiente, se creo una función llamada "insertDesc" que toma un numero y una lista ya ordenada, y revisa si el elemento individual es mayor al primer elemento de la lista(que al estar ya ordenada, es el mayor), si este es mayor, se pone al inicio, y si no, se llama recursivamente a la función con el cuerpo de la lista, hasta que sea mayor a algun elemento.
Luego en la funcion de ordenDesc, se toma el primer elemento de una lista de flotantes que se pasa como argumento y se usa el inserDesc con resultado del cuerpo de la lista al pasar por la misma ordenDesc llamada recursivamente hasta vaciar la lista, de modo que se usa el inserDesc con todos los elementos.

### resultados de las pruebas:

a remData se le pasarón [1,9,3,7,2,6,4,8,5,10], 2 y 6 como argumentos, y el programa devolvió [3.0,2.0,6.0,4.0,5.0]; y a orderDesc la lista de flotantes [3.8,1.2,5.1,2.7,5.4], y devolvió [5.4,5.1,3.8,2.7,1.2].

### dificultades y soluciones:
En primer lugar, como no teníamos experiencia en usar funcines que tomen otras funciones como argumento, por lo cual se vió este video https://www.youtube.com/watch?v=7JK6qtpKLoQ&t=107s, en el cual aprendimos sobre las funciones como argumento y sobre la notación lambda, que fueron usados para solucionar nuestras dificultades.

## Punto 2: Metodos numericos
Se tenía que hacer funciones para aproximar la función exponencial, el coseno y el logaritmo natural.
En las 3 se tuvo que crear una función factorial, que multiplica recursivamente un numero por su anterior, hasta llegar a 0 donde es igual a 1. También las 3 usaron la función de error porcentual, que reemplaza en la formula de error porcentual los valores de nuestras funciones como el valor experimental, y el valor de las funciones de haskell como el teorico.

### Función exponencial:

La función exponencial toma un numero que es el que se quiere tomar como x, que en la función se llama m, y otro que es la precición del calculo.
Se usa una función recursiva donde se aplica la formula dada a m tomando la precición dada como N, despues se suma recursivamente con la misma formula tomando a N-1, hasta llegar a N=0, donde la formula siempre es igual a 1. Luego se toma el resultado y se usa en la función de error porcentual.

### Función coseno:

De forma similar, toma dos numeros, m y la precición n. Despues, para cada enero k de 0 a n, se aplica la formula dada tomando m como x y k como n, y se suman todos los resultados para todos los valores de k. Finalmente se usa la función de error porcentual con el resulado obtenido y la función cos de Haskell.

### Función de logaritmo natural:
El proceso fue casi igual al del coseno; la función toma dos numeros, m y la precición n. Despues, para cada enero k de 0 a n, se aplica la formula para el logaritmo natural tomando m como x y k como n, y se suman todos los resultados para todos los valores de k. Finalmente se usa la función de error porcentual con el resulado obtenido y la función log de Haskell.

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
Con un error porcentual demasiado grande, debido a la baja precición.
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
y despues
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
Que si bien aun tiene un error porcentual relativamente bajo, es mucho menos precisa que cuando se le da una precición alta

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
Que usaba exclusivamente floats;  no obstante, seguía sin funcionar, por lo cual se decidió estudiar más Haskell, finalmente, llegamos al video de https://www.youtube.com/watch?v=bc3_yZEAC_0, que ofrecía una opción diferente a la recurción para resolver el problema, siendo la compresión de listas (|k<-), y se consultó además sobre varias funciones fundamentales, como sum y fromInteger, y sobre tipos de datos como Float y Double; con lo cual se obtuvo el resultado final. Lo curioso es que, luego de volver a probar las primeras versiones descartadas del código, estas funcionaron sin error alguno, con lo cual no entiendo por que al principio estaban retornando valores incorrectos; sin embargo ya se había construido el código con compresión y sumatoria, que se prefirió por su mayor precisión. el fromIntegral también se añadió en un intento de solucionar los problemas iniciales.
Originalmente tampoco se pudo hacer la función logaritmica, pues en la formula de la guía la sumatoria empieza con n=0, con lo cual da un resultado infinito, por eso es espero a la clase para que el profesor clarificaba que debía empezar con n=1.
También había problemas con el error porcentual, pues con la función coseno abeces daba un resultado negativo, devido a que el coseno de ciertos numeros lo es. Esto se solucionó aplicando valor absoluto a todos los componentes de la división, para que el resultado sea siempre positivo.



