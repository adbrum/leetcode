# 10) Heap / Priority Queue (Fila de Prioridade)

**Quando usar:**

* Selecionar os **top-k** elementos (os `k` mais pequenos/maiores).
* Merge de `k` listas ordenadas.
* Encontrar o **k-ésimo** elemento mais pequeno/maior num conjunto.
* Simulação de eventos em ordem de prioridade.

## Problema de Exemplo: [Kth Largest Element in an Array](https://leetcode.com/problems/kth-largest-element-in-an-array/)

* **Entrada:** `nums = [3,2,1,5,6,4]`, `k = 2`
* **Saída:** `5` (O 2.º maior elemento é 5)

## Solução (O(n log k) / O(k)) - Min-Heap de Tamanho k

```python
import heapq

def findKthLargest(nums, k):
    # 1. Inicializa um min-heap com os primeiros k elementos
    heap = nums[:k]
    heapq.heapify(heap)  # Cria um min-heap com os k maiores vistos até agora (a raiz é o k-ésimo maior)
    
    # 2. Processa o resto dos elementos
    for x in nums[k:]:
        # Se o elemento atual (x) for maior que o menor elemento no heap (heap[0])
        if x > heap[0]:
            # Substitui a raiz (o menor dos k maiores) por x
            heapq.heapreplace(heap, x)
            
    # 3. A raiz do min-heap (heap[0]) é o k-ésimo maior elemento
    return heap[0]
```

## Complexidade:

* **Tempo:** `O(n \log k)`
    * Inicialização do *heap*: `O(k)`.
    * Cada uma das `(n-k)` operações `heapreplace` (inserir + remover) custa `O(\log k)`.
* **Espaço:** `O(k)` (O *heap* mantém no máximo `k` elementos.)

---

## Passo a passo:

1.  O objetivo é manter um **Min-Heap (Heap Mínimo)** de tamanho **`k`**.
2.  Este *min-heap* armazena os `k` **maiores** elementos que foram vistos até ao momento.
3.  A **raiz** do *min-heap* (`heap[0]`) é, por definição, o **menor** dos `k` elementos que lá estão, ou seja, o **k-ésimo maior elemento** do conjunto global.
4.  Ao processar um novo elemento (`x`):
    * Se `x` for **maior** que a raiz do *heap* (`heap[0]`), ele deve pertencer ao conjunto dos `k` maiores.
    * Usa-se `heapq.heapreplace(heap, x)` para remover a raiz (o antigo k-ésimo maior) e inserir `x` em `O(\log k)`, mantendo o *heap* de tamanho `k`.

---

## 🎯 Outros Problemas Típicos

| Problema | Dificuldade | Link |
|----------|-------------|------|
| [Merge k Sorted Lists](https://leetcode.com/problems/merge-k-sorted-lists/) | Difícil | [Link](https://leetcode.com/problems/merge-k-sorted-lists/) |
| [Top K Frequent Elements](https://leetcode.com/problems/top-k-frequent-elements/) | Média | [Link](https://leetcode.com/problems/top-k-frequent-elements/) |
| [Find Median from Data Stream](https://leetcode.com/problems/find-median-from-data-stream/) | Difícil | [Link](https://leetcode.com/problems/find-median-from-data-stream/) |
| [Kth Smallest Element in a Sorted Matrix](https://leetcode.com/problems/kth-smallest-element-in-a-sorted-matrix/) | Média | [Link](https://leetcode.com/problems/kth-smallest-element-in-a-sorted-matrix/) |
| [Meeting Rooms II](https://leetcode.com/problems/meeting-rooms-ii/) | Média | [Link](https://leetcode.com/problems/meeting-rooms-ii/) |