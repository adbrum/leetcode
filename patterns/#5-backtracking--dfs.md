# 5) Backtracking / DFS (Busca em Profundidade)

**Quando usar:**

* Para gerar **combinações, permutações, *subsets***.
* Problemas de escolha/recursão que envolvem **"tentativa e recuo"** (como labirintos, problemas N-Queens ou Sudoku).

## Problema de Exemplo: Subsets

* **Entrada:** `nums = [1,2,3]`
* **Saída:** `[[],[1],[2],[1,2],[3],[1,3],[2,3],[1,2,3]]`

## Solução (O(n * 2^n) tempo, espaço proporcional ao output)

```python
def subsets(nums):
    res = []
    path = []
    
    # 'start' garante que cada elemento seja escolhido apenas uma vez para o subset atual (evita duplicatas e mantém ordem)
    def backtrack(start):
        # 1. Adiciona o subset atual à lista de resultados
        res.append(path.copy())
        
        # 2. Gera novas escolhas (extensões)
        for i in range(start, len(nums)):
            # Escolha (Try): Incluir nums[i]
            path.append(nums[i])
            
            # Recursão: Continua a construir o subset a partir do próximo elemento
            backtrack(i + 1)
            
            # Recuo (Untry): Remove nums[i] para testar outras opções no loop
            path.pop()
            
    backtrack(0)
    return res
```

## Complexidade:

* **Tempo:** `O(n \cdot 2^n)` (Existem `2^n` subsets no total. O custo `O(n)` vem do `path.copy()` para adicionar cada um desses `2^n` subsets ao resultado.)
* **Espaço:** `O(n \cdot 2^n)` para armazenar o resultado final, mais `O(n)` para a profundidade máxima da pilha de recursão.

---

## Passo a passo:

1.  A função `backtrack` é a nossa **Busca em Profundidade (DFS)**.
2.  A cada passo da recursão, o `path` atual (o subset construído até agora) é **adicionado ao resultado**.
3.  O *for* loop itera sobre os elementos disponíveis para serem **incluídos** no subset.
4.  Para cada elemento:
    * É **incluído** (`path.append`).
    * A função `backtrack` é **chamada recursivamente** para construir extensões.
    * O elemento é **removido** (`path.pop`) — o passo de **recuo** — para que a próxima iteração do *for* possa explorar um caminho diferente.