# 6) BFS (Breadth-First Search)

**Quando usar:**

* Grafos e Árvores para processamento por **camadas** ou **níveis**.
* Encontrar os **caminhos mais curtos** em grafos não ponderados.
* Travessia de Árvores por Níveis (*Level Order Traversal*).

## Problema de Exemplo: Binary Tree Level Order Traversal

* **Entrada (Árvore):** `[3,9,20,null,null,15,7]` (Representação em array)
* **Saída:** `[[3],[9,20],[15,7]]`

## Solução (O(n) / O(n))

```python
from collections import deque

class TreeNode:
    def __init__(self, val=0, left=None, right=None):
        self.val = val
        self.left = left
        self.right = right

def levelOrder(root):
    if not root: return []
    
    q = deque([root])
    res = []
    
    while q:
        level = []
        # Processa todos os nós do nível atual (len(q))
        for _ in range(len(q)):
            node = q.popleft()
            level.append(node.val)
            
            # Adiciona filhos à fila para o próximo nível
            if node.left: q.append(node.left)
            if node.right: q.append(node.right)
            
        res.append(level)
    return res
```

## Complexidade:

* **Tempo:** `O(n)` (Cada nó é visitado e processado exatamente uma vez.)
* **Espaço:** `O(n)` (A fila pode conter até `O(n)` nós no caso de uma árvore completa.)

---

## Passo a passo:

1.  Usa uma **fila (`deque`)** para armazenar os nós a serem visitados.
2.  Inicia a fila com o nó raiz.
3.  O *loop* `while q:` continua enquanto houver nós a processar.
4.  Dentro do *loop* principal, usa `for _ in range(len(q))` para garantir que apenas os nós do **nível atual** sejam processados nesta iteração.
5.  A cada nó processado, adiciona os seus filhos à fila para serem processados no **próximo nível**.
6.  O resultado de cada nível é armazenado na lista `res`.