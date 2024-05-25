>[!IMPORTANT] Todo el código mostrado está escrito para c++
#### Planteamientos
1. Supongamos un arreglo $a$ con valores enteros $\infty^- \leq i \leq \infty^+$ y queremos saber la suma de los elementos hasta un índice $b$, una opción es que por cada "*querie*" hagamos un recorrido con un ***for***: 
``` cpp fold title:"Ejemplo 1: Brute Force"
for (int i = 0; i < queries.size(); i++) {
	int sum = 0;
	for (int j = 0; j <= queries[i]; j++) {
		sum += a[j];
		cout << sum << '\n';
	}
}
```

Es fácil darnos cuenta que según las queries que se necesiten será la complejidad de nuestro programa, entonces podríamos decir que nuestro código tiene una complejidad de $O(q*n)$  siendo $q$ la cantidad de queries y $n$ el tamaño de nuestro arreglo.
***
Veamos otra estrategía: #prefix_sum

``` cpp fold title:"Ejemplo 2: Prefix Sum"
unordered_map<int, int> prefix_sum;
for (int i = 1; i < a.size(); i++) {
	prefix_sum[a[i]] +=  prefix_sum[a[i-1]];
}
for (int i = 0; i < queries.size(); i++) {
	int sum = prefix_sum[queries[i]];	
	cout << sum << '\n';
}
```
En este ejemplo es fácil ver qué tendremos una complejidad de $O(n)$ pues cada ***for*** es independiente del otro.
Esta complejidad se logra gracias al hecho de que hacemos un pre computo de la suma de los elementos, ahora bien, ¿qué pasaría si hacemos continuamente cambios al arreglo?
Para más información sobre este enfoque: [[prefix_sum]]
***
#fenwick_tree
2. Ahora además de tener *queries* para consultar la suma hasta cierto índice, consideremos sumas hasta índices pero tambien otras *queries* para cambiar los valores en ciertos índices, ¿como afectará esto a nuestro algoritmo de [[prefix_sum]]? 

Pensemos en el subtema más lindo de este tema,  [[trees]] y en especial el [[fenwick tree]] cómo se verá en ese árticulo con el *Fenwick Tree* tendremos una complejidad de $O(log(n))$ aún cúando cambiemos los valores de cada índice, pues estos cambios modifican todo el árbol.
*** 
##### Súmario #sum_summary
- Debemos evitar a toda costa la fuerza bruta para este tipo de problemas.
- Prefix sum nos funciona muy bien cúando debemos calcular las sumas en arreglos estáticos, pues es fácil y rápido de implementar. 
- El *Fenwick Tree* nos brinda la posibilidad de creación de $O(n)$ y de búsqueda y cambio en $O(log(n))$ pero es más complejo de implementar.
***

