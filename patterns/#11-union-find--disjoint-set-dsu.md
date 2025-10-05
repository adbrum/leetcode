# 11) Union-Find / Disjoint Set (DSU)

**Quando usar:**

* Para gerir e acompanhar a união de elementos em conjuntos.
* Problemas de **componentes conectados** em grafos não dirigidos.
* **Detetar ciclos** em grafos não dirigidos.
* Problemas que envolvem operações de **fusão/união** (Exemplos: redes, *account merges*).

## Problema de Exemplo: Number of Connected Components in an Undirected Graph

O objetivo é contar o número de componentes conectados num grafo.

* **Entrada:** `n = 5` (nós 0 a 4), `edges = [[0,1],[1,2],[3,4]]`
* **Saída:** `2` (Componentes: `\{0, 1, 2\}` e `\{3, 4\}`)

## Solução (Quase O(n) / O(n))

```python
def countComponents(n, edges):
    parent = list(range(n))
    rank = [0]*n

    # Função FIND: Encontra o representante/raiz do conjunto (com Path Compression)
    def find(x):
        if parent[x] != x:
            # Path Compression: Torna o pai do nó o representante do conjunto
            parent[x] = find(parent[x])
        return parent[x]

    # Função UNION: Une dois conjuntos (com Union by Rank)
    def union(a, b):
        ra, rb = find(a), find(b)
        
        # Se já estiverem no mesmo conjunto, não há união
        if ra == rb:
            return False

        # Union by Rank: Anexa a árvore menor (menor rank) à raiz da árvore maior
        if rank[ra] < rank[rb]:
            parent[ra] = rb
        elif rank[ra] > rank[rb]:
            parent[rb] = ra
        else:
            # Se os ranks forem iguais, escolhe um para ser a nova raiz e aumenta o seu rank
            parent[rb] = ra
            rank[ra] += 1
            
        return True

    count = n # Começa com 'n' componentes (cada nó é um componente)
    for a, b in edges:
        # Se a união for bem-sucedida (os nós estavam em componentes diferentes),
        # o número de componentes diminui em 1.
        if union(a, b):
            count -= 1
            
    return count
```

## Complexidade:

* **Tempo:** `O((n + m) \cdot \alpha(n)) \approx O(n + m)`
    * Onde `n` é o número de nós e `m` o número de arestas. `\alpha(n)` (a função inversa de Ackermann) cresce extremamente devagar, sendo **quase constante**, tornando o tempo de execução praticamente linear.
* **Espaço:** `O(n)` (Para armazenar os arrays `parent` e `rank`.)

---

## Passo a passo (DSU):

1.  **Inicialização:**
    * Cria-se um array **`parent`** onde `parent[i] = i`, tornando cada nó o seu próprio conjunto/componente.
    * O contador de componentes (**`count`**) começa em `n`.
2.  **`FIND(x)` (com *Path Compression*):** Encontra o nó **representante (raiz)** do conjunto de `x`.
3.  **`UNION(a, b)` (com *Union by Rank*):** Tenta fundir os conjuntos de `a` e `b`.
    * Se `FIND(a) == FIND(b)`, estão no mesmo conjunto: retorna `False`.
    * Se forem diferentes, anexa a raiz de *rank* menor à raiz de *rank* maior. Se os *ranks* forem iguais, anexa uma à outra e incrementa o *rank* da nova raiz. Retorna `True`.
4.  **Processamento das Arestas:**
    * Para cada aresta `(a, b)`, chama-se `UNION(a, b)`.
    * Se `UNION` retornar **`True`** (ocorreu uma fusão), significa que dois componentes foram unidos, então `count` é decrementado em 1.