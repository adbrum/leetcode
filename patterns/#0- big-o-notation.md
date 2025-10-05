# 📘 Big O Notation

## 🔹 O(1) – Tempo Constante

**Definição:** O tempo de execução **não depende** do tamanho da entrada (`n`).

**Exemplo:**

```python
def get_first_element(arr):
    return arr[0]  # sempre retorna o primeiro elemento
```
**Análise:**

* Não importa se `arr` tem 10 ou 10 milhões de elementos. A operação de aceder ao índice `[0]` leva o **mesmo tempo**.

**Complexidade:** `O(1)`

## 🔹 O(`\log n`) – Tempo Logarítmico

**Definição:** O algoritmo reduz o problema pela **metade** a cada passo.

**Uso Comum:** Muito comum em algoritmos de **busca binária** (*binary search*) e estruturas de dados baseadas em árvores.

**Exemplo:**

```python
def binary_search(arr, target):
    l, r = 0, len(arr) - 1
    while l <= r:
        mid = (l + r) // 2
        if arr[mid] == target:
            return mid
        elif arr[mid] < target:
            l = mid + 1
        else:
            r = mid - 1
    return -1
```
**Análise:**

* A cada iteração, o intervalo de pesquisa diminui pela **metade**.
* Para `n = 1.000.000`, são necessários no máximo `\approx 20` passos (`\log_2 1.000.000 \approx 19.9`). O crescimento é extremamente lento e eficiente.

**Complexidade:** `O(\log n)`

## 🔹 O(`n`) – Tempo Linear

**Definição:** O tempo de execução é diretamente proporcional ao tamanho da entrada (`n`). O algoritmo percorre todos os elementos da entrada **exatamente uma vez**.

**Exemplo:**

```python
def find_max(arr):
    maximum = arr[0]
    for num in arr:
        if num > maximum:
            maximum = num
    return maximum
```
**Análise:**

* Para encontrar o valor máximo, o algoritmo **precisa olhar cada elemento** do *array* uma única vez.
* Se a entrada dobrar de tamanho (de `n` para `2n`), o tempo de execução também dobra.

**Complexidade:** `O(n)`

## 🔹 O(`n \log n`) – Tempo Quase Linear

**Definição:** O algoritmo geralmente envolve dividir o problema em subproblemas (o fator `\log n`) e depois fazer um trabalho linear (`n`) para combiná-los ou resolvê-los.

**Uso Comum:** Comum em algoritmos de **ordenação eficiente** como *Merge Sort*, *Quick Sort* (caso médio) ou *Heap Sort*.

**Exemplo (Merge Sort simplificado):**

```python
def merge_sort(arr):
    if len(arr) <= 1:
        return arr
    mid = len(arr) // 2
    left = merge_sort(arr[:mid])
    right = merge_sort(arr[mid:])
    return merge(left, right)

def merge(left, right):
    result = []
    while left and right:
        if left[0] < right[0]:
            result.append(left.pop(0))
        else:
            result.append(right.pop(0))
    return result + left + right
```
**Análise (Merge Sort):**

* **Divisão (`\log n`):** O processo de dividir o *array* recursivamente em metades resulta em `\log n` **níveis** de recursão (semelhante ao *binary search*).
* **Combinação (`n`):** Em cada nível da recursão, o processo de **`merge` (combinar)** todos os elementos das sub-listas leva um tempo total de `O(n)`.
* **Total:** `(\text{Trabalho por Nível}) \times (\text{Níveis}) = n \times \log n`.

**Complexidade:** `O(n \log n)`

## 🔹 O(`n^2`) – Tempo Quadrático

**Definição:** O tempo de execução cresce proporcionalmente ao **quadrado** do tamanho da entrada (`n`).

**Uso Comum:** Algoritmos com **dois *loops* aninhados**, comuns em problemas de comparação de todos os pares de elementos.

**Exemplo:**

```python
def has_duplicates(arr):
    for i in range(len(arr)):
        for j in range(i+1, len(arr)):
            if arr[i] == arr[j]:
                return True
    return False
```
**Análise:**

* Cada elemento no *array* é comparado com **todos os outros** elementos restantes.
* A cada iteração do *loop* externo, o *loop* interno executa aproximadamente `n` vezes. O número total de operações é `\approx n \times n`.
* Para `n = 1000`, o número de comparações é até `\approx 500.000`. O desempenho deteriora-se rapidamente com o aumento de `n`.

**Complexidade:** `O(n^2)`

## 🔹 O(`2^n`) – Tempo Exponencial

**Definição:** O tempo de execução **dobra** a cada aumento unitário no tamanho da entrada (`n`). É uma complexidade que cresce de forma explosiva.

**Uso Comum:** Típico em algoritmos de **força bruta** (*brute force*), onde todas as **combinações ou *subsets* possíveis** devem ser gerados (por exemplo, o Problema do Caixeiro Viajante, ou a recursão ingénua).

**Exemplo (Fibonacci recursivo sem memoização):**

```python
def fib(n):
    if n <= 1:
        return n
    return fib(n-1) + fib(n-2)
```
**Análise:**

* O algoritmo cria uma **árvore de chamadas binária** onde cada nó (exceto a base) faz duas chamadas recursivas.
* O número de operações cresce **exponencialmente** com `n`.
* Para `n = 40`, já são feitas **`\approx 1` bilhão de chamadas**. Isto torna o algoritmo impraticável para grandes valores de `n`.

**Complexidade:** `O(2^n)`

## 🔹 O(`n!`) – Tempo Fatorial

**Definição:** O tempo de execução cresce de forma **absurdamente rápida** e é a complexidade mais lenta, exceto por `O(n^n)`. O tempo é proporcional ao fatorial do tamanho da entrada (`n`).

**Uso Comum:** Típico em algoritmos que precisam gerar ou processar **todas as permutações possíveis** de um conjunto (exemplo: soluções exatas para o Problema do Caixeiro Viajante).

**Exemplo:**

```python
import itertools

def all_permutations(arr):
    # Gera todas as permutações do array
    return list(itertools.permutations(arr))
```
**Análise:**

* O número de operações é igual ao **número total de permutações** que podem ser formadas com os `n` elementos.
* O crescimento é impraticável mesmo para valores pequenos de `n`.
* Para `n = 10`, já são `10! = 3.628.800` permutações. Para `n = 20`, o número é astronómico.

**Complexidade:** `O(n!)`

# 📉 Resumo da Notação Big O

A Notação Big O descreve o desempenho (tempo ou espaço) de um algoritmo à medida que o tamanho da entrada (`n`) cresce.

---

| Notação | Nome | Descrição | Exemplo Típico |
| :--- | :--- | :--- | :--- |
| **`O(1)`** | Constante | O tempo de execução é **independente** de `n`. | Acesso direto a um índice de array ou *hash map*. |
| **`O(\log n)`** | Logarítmica | O problema é **reduzido pela metade** em cada passo. | Busca Binária (*Binary Search*). |
| **`O(n)`** | Linear | O tempo de execução é **diretamente proporcional** a `n`. | Percorrer um array com um *loop* simples. |
| **`O(n \log n)`** | Quase Linear | Resultado de dividir o problema (`\log n`) e resolvê-lo linearmente (`n`). | Algoritmos de ordenação eficientes: *Merge Sort*, *Quick Sort* (caso médio). |
| **`O(n^2)`** | Quadrática | O tempo cresce com o **quadrado** de `n`. | Dois *loops* aninhados (comparar todos os pares de elementos). |
| **`O(2^n)`** | Exponencial | O tempo **dobra** a cada adição em `n`. | Geração de *subsets* ou Fibonacci recursivo ingénuo. |
| **`O(n!)`** | Fatorial | O tempo cresce de forma **extremamente rápida**. | Geração de todas as permutações. |

---

### Ordem de Eficiência (Melhor para Pior)

``O(1) < O(\log n) < O(n) < O(n \log n) < O(n^2) < O(2^n) < O(n!)``