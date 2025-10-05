# 4) Binary Search (Busca Binária)

**Quando usar:**

* Pesquisa em **arrays ordenados**.
* Quando a resposta/solução tem uma propriedade **monotónica** (ou seja, se a resposta é verdadeira/possível para `x`, também é para todos os valores maiores/menores que `x`). Ajuda a encontrar o limite mínimo/máximo que satisfaz um *predicado* `P(x)`.

## Problema de Exemplo: Find First and Last Position of Element in Sorted Array

* **Entrada:** `nums = [5,7,7,8,8,10]`, `target = 8`
* **Saída:** `[3,4]` (Índices *0-based*)

## Solução (O(log n) / O(1))

```python
def searchRange(nums, target):
    
    # Função auxiliar para encontrar a primeira ocorrência (índice mais à esquerda)
    def findLeft():
        l, r = 0, len(nums) - 1
        idx = -1
        while l <= r:
            mid = (l + r) // 2
            if nums[mid] < target:
                l = mid + 1
            elif nums[mid] > target:
                r = mid - 1
            else:
                idx = mid  # Guarda o potencial resultado
                r = mid - 1  # Continua a buscar à esquerda para encontrar a primeira ocorrência
        return idx

    # Função auxiliar para encontrar a última ocorrência (índice mais à direita)
    def findRight():
        l, r = 0, len(nums) - 1
        idx = -1
        while l <= r:
            mid = (l + r) // 2
            if nums[mid] < target:
                l = mid + 1
            elif nums[mid] > target:
                r = mid - 1
            else:
                idx = mid  # Guarda o potencial resultado
                l = mid + 1  # Continua a buscar à direita para encontrar a última ocorrência
        return idx

    return [findLeft(), findRight()]
```

## Complexidade:

* **Tempo:** `O(\log n)` (Devido à divisão repetida do espaço de pesquisa.)
* **Espaço:** `O(1)`

---

## Passo a passo:

1.  O problema é resolvido através de **duas buscas binárias independentes**.
2.  **Busca para a Primeira Ocorrência (`findLeft`):**
    * Quando `nums[mid] == target`, guarda o índice como potencial resposta, mas move o ponteiro direito (`r = mid - 1`) para continuar a procurar o alvo na sub-array esquerda.
3.  **Busca para a Última Ocorrência (`findRight`):**
    * Quando `nums[mid] == target`, guarda o índice como potencial resposta, mas move o ponteiro esquerdo (`l = mid + 1`) para continuar a procurar o alvo na sub-array direita.