---
layout: default
title: Animation Curves y LERP
permalink: /curves-esp/
description: Como usar AC y LERP en mi editor de niveles
---

# Introducción

He decidido usar **Animation Curves** y **Lerp** en nuestro Editor de Niveles.
<br/>El problema es que, no todo el mundo sabe como usarlo, pero intentaré explicarlo en este documento.
<br/><br/>
Un **uso** de las Animation Curves es describir algo que **varí­a a travez del tiempo**
<br/>Vayamos a un ejemplo

# Intensidad con cambio lineal

En mi Editor de Niveles, puedes describir como quieres que varí­e la intensidad de una luz a travez del tiempo.
<br/>Si dibujas una curva que, **horizontalmente**, va de 0 hasta 1, la variación de intensidad **durará un segundo**.  
<br/>El comportamiento después del primer segundo va a depender de la configuración Post Wrap (hablaremos de eso mas adelante).
<br/><br/>
Entonces, ya sabes que es lo que pasa con la curva horizontalmente (tiempo en segundos).
Pero... ¿Qué significa el **eje vertical**? O... ¿Cómo la **forma** de la l­í­nea de la curva afecta los usos de Animation Curve?
<br/>Bueno, empezemos interpretandolo como la intensidad de una luz.  
<br/>Si el primer punto de la lí­nea coí­ncide verticalmente con el valor 0, significa que la luz estará **apagada**. Y el valor 1 significa que estará prendida con una **intensidad fuerte**.
<br/><br/>Si dibujas una lí­nea recta desde el punto (0,0) hasta el punto (1,1), entonces la luz **empezará apagada**, y **gradualmente** y **uniformemente** irá subiendo su intensidad hasta alcanzar, en un segundo, la intensidad de valor 1, finalmente.
<br/>![First Curve](../curves/curve1.png "Primer ejemplo")

<br/><br/>LLendo mas allá, ahora si la linea recta va desde (0,0) hasta (2,1), la luz también irá de 0 a 1, pero esta vez tardará 2 segundos, porque el valor del eje **horizontal** del segundo punto es 2.
<br/>![Second Curve](../curves/curve2.png "Segundo ejemplo")

<br/><br/>Entonces, si por ejemplo quisieras una variación que comienze con la luz iluminando a medias, que uniformemente disminuya hasta un cuarto de iluminacion, y empieze a los 0.5 segundos y termine a los 1.5 segundos... entonces harí­as una lí­nea recta que vaya desde el punto (0.5,0.5) hasta el punto (1.5,0.25) 
<br/>![Third Curve](../curves/curve3.png "Tercer ejemplo")

<br/><br/>¿Se entiende por qué? Presta atención a los numeros de **cada punto**. Recuerda, el **primer** numero es **tiempo**, el **segundo** es la **variable de animación** (intensidad de la luz en este caso).
<br/>En este caso, los segundos no empiezan desde cero, entonces es cuando el **pre wrap** entra en acción. (Explicaré en corto como funciona) 
<br/>LLendo mas allá, podemos hacer mas de dos puntos, y crear diferentes transiciones a travez del tiempo. 

# Pre and Post Wrap

Nos enfocaremos en el post wrap y el pre wrap. ¿Que pasa con la animación fuera de los limites de la curva? Puede haber tres comportamientos **clamp, loop y ping-pong**

**Clamp** significa que tomará el valor del último punto y lo usará por toda la eternidad.
<br/>Si tomamos el primer ejemplo (desde (0,0) hasta (1,1)) y configuramos el post wrap como clamp, luego de pasar el limite, la curva valerá 1 verticalmente durante todos los segundos posteriores.
<br/>Y, en el tercer ejemplo ((0.5,0.5) to (1.5, 0.25)), la luz comenzará con intensidad 0.5 desde el segundo cero hasta el segundo 0.5, ya que esto estaba fuera del limite inicial. Esto serí­a un ejemplo de pre wrap clamp. 

Ahora, veremos como funciona el commportamiento **Loop**. Esto simplemente repite infinitamente el mismo patrón de la curva que hicimos durante toda la eternidad. Si la curva empieza en 0 verticalmente, y termina en 1, entonces luego de eso, volverá a empezar en 0, y terminará en 1, describiendo la misma forma de curva que habí­amos hecho. Y así­ sucesivamente. 
Lo mismo pasa con el pre wrap, si empezamos en un tiempo mayor a cero, lo anterior a esto sera una replica de la misma curva precediendo la misma. Antes del limite izquierdo, tomará el ultimo valor de la curva, y retrocederá dibujando ls misma curva hasta llegar hasta el tiempo 0.

<br/>![Loop example](../curves/loop.gif "Loop")

Finalmente, queda explicar **Ping Pong**. Es similar a loop, pero cada vez que repite la curva, la espeja. Por ejemplo, si la curva va desde (0,0) hasta (1,1), entonces luego irá desde (1,1) hasta (0,0) describiendo la curva original pero espejada. Luego de eso, la vuelve a espejar, por lo que queda la curva original. Luego espejada otra vez, y luego original otra vez. Así­ eternamente.

<br/>![PingPong example](../curves/pingpong.gif "PingPong")

Notar que, en Loop, la intensidad de la luz va desde 0 a 1, y despues repentinamente cambia a 0, para ir a 1 de vuelta.
En cambio, en Ping Pong, la luz tiene mas continuidad, ya que va desde 0 a 1, luego de 1 a 0, luego de 0 a 1, y asi sucesivamente.
A veces PingPong es una solución mas elegante.
Pero si diseñas una curva que empieza y termina con la misma intensidad, entonces capaz sea mejor usar Loop.

# Intensidad con un cambio no lineal

Por ahora, hemos hablado de lineas rectas, ¿Pero qué pasa con las lineas curvas?
<br/>Esta es la parte interesante, porque aquí­ comienza tu creatividad, ya que es es una herramienta que dará movimmientos originales, suaves, o muy rapidos, o en un principio suaves y luego rápidos, la posibilidad de formas es infinita. 
<br/><br/>
Por ejemplo, imaginemos una curva que va desde (0,0) a (1,1) pero con esta forma: 
<br/>![complex example curve](../curves/curve4.png "NoLineal1")
<br/>Esto significa que los valores iniciales van a variar ligeramente, suave. Pero hacia el final va a cambiar con un monton de velocidad. ¿Entiendes esto en la forma de la curva? Una linea que tiende a ser horizontal, implica cambios suaves, mientras que una linea tendiendo a forma vertical implica cambios bruscos en el tiempo. Entonces la variacion no es mas lineal, ahora tiene movimientos mas naturales.
<br/><br/>Por ejemplo, puedes hacer una luz una luz que se prende suavemente, pero cuando alcanza la mitad empieza a disminuir hacia un cuarto, luego que vaya rapidamente hacia la máxima intensidad, entonces abruptamente va a 0 y se queda ahí­ por un tiempo, luego que haga todo lo mismo pero espejado con el post wrap ping pong. Entonces tendrás una salvaje e impredecible luz. 

# Otras animaciones

Ok, ya estamos listos para ir al siguiente nivel, LERP.
<br/>Lerp transforma valores que van de 0 a 1, en valores que van de un valor **mí­nimo** a un valor **máximo**, o dicho de otra form de un valor 0 hasta un valor 1. Prefiero llamarlo asi en vezx de minimo o maximo, porque no siemnpre va de un valor chico a un valor grande, pero en cambio siempre va a variar desde el valor 0 del eje vertical de la curva hasta el valor 1 del mismo eje. 
<br/><br/>
Entonces, imagina que tenemos la escala vertical de una pared, y necesitamos que varí­e desde 1 a 5. Por alguna razón, la herramienta de curvas tiene dificultades para poner valores verticales mayores a 2, por esa razon se usa LERP. Simplemente hacemos una curva que varí­e verticalmente entre 0 y 1, y en las propiedades de la animación configuramos 1 para el valor 0 y 5 para el valor 1.
Entonces ya lo tienes, simplemente dibujar una curva entre (0,0) y (1,1) y el tamaño variará de 1 a 5, y tardará 1 segundo. Todo gracias a LERP. 
<br/><br/>LERP asigna los valores de forma lineal, eso signfica que el valor 1 va a transformarse en 5, el 0.5 en 2.5 y el valor 2 en 10 (solo como ejemplo, ya que en realidad solo llegaremos hasta 1). 
<br/>Lo repito, con esto puedes imaginar lo que quieras. Puedes disminuir el tamaño, cambiando suavamente o bruscamente. Puedes variar el tamaño con mas de dos puntos, mover los puntos y rotar las lineas como quieras. Tu creatividad es el lí­mite.

# Animación de rotación

Usando la idea de LERP, podemos hacer variaciones en la rotación también. Solo debes pensar que el valor 0 será un ángulo inicial, y el valor 1 un ángulo final.
<br/>Por ejemplo, para rotar continuamente 360 grados, tenes que configurar el valor 0 como angulo 0, y el valor 1 como angulo 360. Y en la forma de la curva hacer una linea recta que vaya desde (0,0) hasta (1,1), si quieres por ejemplo que complete toda la rotación en 1 segundo. 
<br/>Puedes poner otro angulo, y tampoco es necesario que el angulo del valor 0 sea menor al angulo del valor 1, esto no le importa al LERP. Puedes ir suavemente desde (0,0) hasta (1.25,0.5) (desde el valor 0 hasta el valor 1 en 1.25 segundos). Entonces esperar 3 segundos con el mismo valor (una linea completamente horizontal, que termine en el punto (4.25, 0.5)), después ir hasta (6,0.75) (rotar hasta el 75% del angulo del valor 1 en 1.75 segundos) rápidamente, y así­ sucesivamente.

Con movimientos complejos puedes hacer animaciones que confundan al jugadaor, o hacerlo mas facil de jugar también, es una herramienta muy poderosa. Por eso decidí­ usarla, afrontando la curva de aprendizaje que tiene.

# Ejemplo de animación compleja

En este ejemplo verás una animacion de rotación. Con el valor 0 puesto como 0 grados, y el valor 1 como 90 grados. Tiene un comienzo suave y una finalización brusca, usando tres puntos. Y usando ping pong como end wrap. A continuación la curva que quedarí­a y una animación de como girarí­a dicha columna.
<br/>![complex example curve](../curves/curve4.png "Complex curve")
<br/>![complex example gif](../curves/rotation.gif "Complex animation")

