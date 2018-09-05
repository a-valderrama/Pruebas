### Tarea 2

**1.1**  Checando en el ambiente (pila de ejecución) si existe la variable, es decir si esta definida, con su valor. Bien sea una evaluación estática o dinámica.

**1.2**  Demostración : Por ***subst*** hacemos una sustitución por cada invocación, entonces para sustituir todas las variables,  vamos a tener algo como :
$$
(subst \, \, \; (subst \, \, \; (subst \; ....)\, \; a_{n-1} \, \; v_{n-1})\, \; a_{n} \, \; v_{n})
$$
y observamos ya tiene una forma más compacta, es decir, arriba ya es el mejor caso.  Notamos que la primera sustitución nos toma ***n***,  y la segunda sustitución tomara**n - 1**, así decreciendo, entonces lo que tenemos es una suma geométrica. Entonces, esto es de orden $  {O(n^{2})} $.

 **1.3**  Tres snippets :

- Shell

  ```shell
  #!/bin/bash
  a=0
  b=1
  c=`expr $b / $a`
  d=`expr $b + $a`
  echo $d
  ```


- Python

  ```python
  #!/usr/bin/env python3
  # -*- coding: utf-8 -*-
  a = 0
  b = 1
  c = b / a
  d = b + a
  print(d)
  ```

- Ruby

  ```ruby
  #!/usr/bin/ruby
  a = 0
  b = 1
  c = b / a
  d = b + a
  puts d		
  ```

Después hacer las pruebas con cada archivo, se debe descubrir que los tres lenguajes son glotones, anque suelen tener algunos "truquitos" o comandos que se realizar con evaluacion perezosa.

**1.4**  Investigaciones :

- ***delay***  y  ***force***  son dos funciones que soportan evaluación perezosa explícitamente, donde delay recibe una expresión sin evaluarla, hasta cuando se usa force para evaluarla, como los siguientes códigos :

  ```scheme
  ;;The multiplication is saved but not executed
  (define my-promise (delay (* 5 6 7 8 9)))

  ;;Again, saved but not executed
  (define another-promise (delay (sqrt 9)))

  ;;Forces the multiplication to execute.  Saves and returns the value
  (display (force my-promise))
  (newline)

  ;;This time, the multiplication doesn't have to execute.  It just returns
  ;;the value that was previously saved.
  (display (force my-promise))
  (newline)

  ;;This produces an error, because the promise must be forced to be used
  (display (+ my-promise (force another-promise)))
  ```

  > https://www.ibm.com/developerworks/cn/linux/l-lazyprog.html

- Como vimos en la tarea pasada ***thunk***, es una manera de implementar una evaluación perezosa en este régimen de evaluación glotona.  
Pero, por ejemplo, también podemos pensar en la tarea opuesta. Para un régimen que no es perezoso, en Haskell, se usa ***Graph Reduction*** para implementar evaluación glotona.

**1.5.1**  *Demostración* :
Sean $P_1$ el primer programa  y $P_2$ es el segundo. Es claro que OUTPUT( $P_1$ )  =  6 =  OUTPUT( $P_2$ ), pues la única diferencia entre ambos es el tipo de evaluación, pero ya sabemos que eso no afecta el output.
Ahora supongamos que  ***f*** es un "compilador", y lo que hace los programas que están escritos en primer lenguaje $L_1$ al segundo lenguaje $L_2$ . Además sabemos que  este compilador trabaja con siguiente reglas :

1. Se agrega un "***:***" en el final de la primera linea de un nuevo bloque.
2. Cuando encuentre un token "***end***" ,  lo elimina junto con la linea que este.

Observamos que ***f*** es una función, y es claro que   ***f*** ( $P_2$ ) = $P_1$ .Por lo tanto,  $P_1$  $\equiv$  $P_2$      $\Box$

**1.5.2**  Vamos a demostrarlo por contradicón :  
Supongamos que no existe $E^{''}$,  por hipótesis, $L^{'}$ y  $L^{''}$ son Turing completos, es decir, para cualquiera expresión $E^{'}$ (en el lenguaje $L^{'}$). Por la definición de Turing completo, tiene que existir una maquina de Turing $M$ con una cadena **$\omega$**  tal que  $E^{'}$ $\equiv$  $\omega$ ,  y también tiene que existir una expresión $E^{''}$ en el lenguaje $L^{''}$ tal que  $\omega$ $\equiv$ $E^{''}$ , pues resulta que $E^{'}$ $\equiv$  $E^{''}$ , esto es una contradicción.
Por lo tanto  $E^{''}$ existe.     $\Box$

**1.5.3**  Si se puede ver afectado por el tipo de evaluación.  Por ejemplo cuando hay una división entre cero, un lenguaje perezoso no nos manda un error si no se tiene que evaluar, pero en un lenguaje glotón mandará un error en tiempo de ejecución, sin importar que en la mayoría de los casos no se use.

Fuera de este tipo de errores, el tipo de evaluación (glotona o perezosa) que tenga un lenguaje de programación no afectará el resultado. Ya que, como hemos visto, el tipo de evaluación sólo afecta a la modificación de la pila, ambiente, más no los valores de la evaluación; pues sencillamente acarrean las evaluaciones que no son necesarias hacer hasta un punto estricto.

##### Grupo RacketRun

- Yuguo Xie | [yuguoxie123@gmail.com](mailto:yuguoxie123@gmail.com)
- Anastassia Egido Knyazeva | [anastassia@ciencias.unam.mx](mailto:anastassia@ciencias.unam.mx)
- Alejandro Valderrama Silva | [at.valderrama@ciencias.unam.mx](mailto:at.valderrama@ciencias.unam.mx)
