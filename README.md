# Castro Mejia Jonatan Alejandro
### Análsis de Algoritmos.
#### Tarea 03: Justificación de Algoritmos 

```markdown
1. Considera el algoritmo denominado V, mostrado abajo.
    a) Indicar qué hace el algoritmo V
    b) Demuestrar que es correcto, con respecto a las condiciones dadas (precondición y postcondición).
```
~~~
    Procedure V (A:Array ; a, b: entero)
    // PreCond: a ≤ b y x ∈ A[a..b]
    var i : enteros;
    Begin
        i ← a ;
        While x != A[i] do i ← i + 1;
        Return i
    End
    // PostCond: a ≤ i ≤ b y b ∉ A[a..i − 1] y x = A[i]
~~~

```markdown
a) El algoritmo incrementa el valor de la copia de uno de los elementos de A, e incrementa su valor en 1 si no encuentra el mismo valor.

b) Demostración. Induccion sobre la longitud de A (n).

* Base inductiva: n = 0
  
  n = 0 significa que el arreglo A es vacío entonces, asignamos el valor de a, a i.
  Pero como A no tiene en donde recorrer entonces no podemos comparar el valor de A[i] con x, 
  por lo que el algoritmo regresa el valor de i.

* Hipóteis de inducción: 

  V(A, a',b') regresa la cuenta del número de elementos entre a' y x', con n = longitud de A , y n > 0.
  
  Por demostrar que V(A, a',b') regresa la cuenta de elementos entre a' y x'.
  Como n > 0 entonces tendremos elementos para recorrer en A, entramos al While y preguntamos si x' != A[i] si este se cumple, 
  aumentamos el valor de i en 1, y si esto no ocurre, regesamos el valor de i o la cuenta del número de elementos entre a' y x' (Hip Ind) 
  
  Por lo que a ≤ i ≤ b y x = A[i]
```

```markdown
2. Problema Φ: Frecuencias. Dado un arreglo finito X de n enteros, no necesariamente distintos, determinar la frecuencia de los elementos en X.

    a) Proporciona un algoritmo (código) iterativo que solucione el problema Φ, indicando PreCondiciones y PostCondiciones
    b) Demuestra, formalmente, que el algoritmo dado es correcto, usando la Técnica del Invariante del ciclo.
    c) Proporciona un algoritmo (código) recursivo que solucione Φ.
    d) Demuestra que el algoritmo dado es correcto usando inducción matemática.
```

```java
a) 
public static void countFreq(int arr[]){

//PreC: arr[a...b] un Arreglo de entreros (ordenado).

        boolean visto[] = new boolean[arr.length];

        for (int i = 0; i < visto.length; i++) {
            if (visto[i] == true)
                continue;
            int frecuencia = 1;
            for (int j = i + 1; j < visto.length; j++) {
                if (arr[i] == arr[j]) {
                    visto[j] = true;
                    frecuencia++;
                }
            }
            System.out.println(arr[i] + " " + frecuencia);
        }
    }
//PostC : Se encontró la frecuencia de cada elemento en arr[a...b] y arr[a...b] no sufrio cambios.
```


```markdown
b) 


```


```java
c) 
public static void countFreq2(int arr[], int inicio, int fin, int[] contador){
    if (arr[inicio] == arr[fin]) {
		contador[arr[inicio]] += fin - inicio + 1;
	}
	else {
		countFreq2(arr, inicio, (inicio + fin) / 2, contador);
		countFreq2(arr, ((inicio + fin) / 2 )+ 1, fin, contador);
	}
}
```
```markdown
d) 

Demostración por inducción sobre el tamaño del arreglo arr (n) 

* Base inductiva: 

Si n = 1, el arreglo contador tendra un tamaño igual al valor obtenido por arr[arr.length-1]+1, inicio = 0  y fin = n - 1.
Por lo que inicio = fin, y la expresion logica arr[inicio]==arr[fin] es verdadera por lo que se asignara el valor de 
fin-inicio +1 -> 0-0+1 en contador[arr[inicio]] -> contador[arr[0]]. ahora el valor de contador en la posicion [arr[0]] será 1. 

* Hipótesis inductiva: 

Por demostrar que countFreq2(arr[a...b], inicio', fin', contador) regresa en contador la frecuencia de cada elemento en arr[a...b]

Ahora como fin > inicio entonces la pregunta lógica arr[inicio] == arr[fin] no se cumple por lo que pasamos al else, y hacemos
recursion por la derecha y por la izquierda de inicio a la mitad y de la mitad + 1 al fin. 

Es decir: 

countFreq2(arr[a...b], inicio', (inicio + fin)/2 , contador') y countFrec2(arr[a...b], (inicio + fin)/2 +1, fin', contador').

Por lo que los valores de inicio y fin cambiaran cuando partamos por la mitad dandonos 2 llamadas recursivas de la siguiente 
manera countFrec2(arr[a...b], inicio', fin', contador') por lo que por Hipótesis de inducción asignará en contador' 
la frecuencia de cada elemento en arr[a...b].


```
```markdown
3. Problema Evaluación de Polinomios.
    El Algoritmo Horner evalua, en el punto x = xo, el polinomio Pn
    * Demuestre que el algoritmo dado es correcto, usando la Técnica del Invariante del ciclo.
```

<div class="math">
\begin{equation}
Pn(xo) = a_0 + a_1x + a_2 x^2 + ... + a_n x^n
\end{equation}
</div>

~~~java
Procedure Horner (a:Pol ; x0: entero) {
    var i, total : entero;
    total ← 0 ;
    For i = k − 1 to 0 by −1 do
        total ← a[i] + total ∗ x0
    Return total 
}
~~~

```markdown
Demostración
Induccion sobre k (el número de iteraciones)

Base inductiva: 

k = 1 y x = x0, por lo que, total= 0, i = 0 (1-1) 

total = a[0] + 0 * x0 
total = a[0] terminamos y se cumple.

```

#####    Hipótesis de Inducción: 

Al inicio de la k-ésima iteración el algoritmo Horner, se tiene que: 
<div class="math">
\begin{equation}
total = \sum_{i=k-1}^{0} a[i] + total' * x_0 
\end{equation}
</div>




```markdown
4. Problema F: Fórmula del Chicharronero.

    El Algoritmo F-Ch, mostrado abajo, pretende encontrar las raíces reales de una ecuación cuadrática.
    Hay que verificar si el algoritmo dado es correcto.
    * a) Si el Algoritmo F-Ch es correcto, demuestra, usando inducción matemática que, en efecto, es correcto.
    * b) Si el Algoritmo F-Ch resulta no ser correcto...
        b.1) indica por qué no es correcto.
        b.2) proporciona un algoritmo que si calcule las raíces reales de una ecuación cuadrática y demuestra, usando inducción matemática, que el algoritmo propuesto es correcto.
        
```
~~~ 
Algoritmo F-Ch (a,b,c: real; & x1,& x2: real)
Begin
    IF a = 0 Then ERROR("No es cuadratica!")
        Else
            d ← b ∗ b − 4.0 ∗ a ∗ c;
    IF d < 0 Then ERROR("Raiz no real!")
        Else
            d ← sqrt(d)
            x1 ← (−b + d)/a/2.0
            x2 ← (−b − d)/a/2.0
End
~~~

```markdown
    a) Demostración
    
    Induccion sobre a.
    
    Caso Base: 
    * a = 0, b = 1, c = 0, entonces tenemos que la pregunta lógica a==0 es verdadera y regresamos el error "No es cuadratica!" 
      y esto es debido a que en la ecuación ax^2 + bx + c = 0, a = 0 por lo que no tenemos un valor cuadrático.  
    
    * a=1, b=1, c=1, entonces tenemos que la pregunta lógica a==0 es falsa por lo que entramos al Else y calculamos el valor de d. 
    
    Sustituimos los valores para obtener d.
    d <- 1 * 1 - 4.0 * 1 * 1 = 1 - 4.0 = -3 = d, 
    Ahora teniendo el valor de d, la pregunta lógica d < 0 es verdadera por lo que regresamos el error "Raiz no real" 
    y esto es debido a que d tendrá que ser sustituido en una raiz cuadrada, pero las raices cuadradas para números < 0 
    no están definidas (no son reales).
    
    * a=2 b=4 c=1, entonces tenemos que la pregunta lógica a==0 es falsa por lo que pasamos al Else y obtenemos el valor de d:
    d <- 4*4 - 4.0 * 2 * 1 = 8 por lo que ahora la pregunta lógica d < 0 es falsa, entramos al Else y 
    
    d <- sqrt(d) -> d = sqrt(8). 
    x1 <- (-4 + d)/2/2.0
    x2 <- (-4 - d)/2/2.0
    
    por lo que obtendremos valores para x1 y x2, las raíces. 
   
    Por lo que para cualquier valor de a,b y c que cumpla las condiciones a > 0, b > a, b > c y d > 0 se obtendran las raices. 
    
    Por lo tanto el algoritmo es correcto.
    
```






