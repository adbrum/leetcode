# 1) Two Pointers (Dois Ponteiros)
**Quando usar:**

* Arrays/strings **ordenados**.
* Quando é necessário comparar elementos de duas extremidades (Exemplos: soma alvo em array ordenado, remoção *in-place*, verificação de palíndromos).

## Problema de Exemplo: [Two Sum II - Input Ordenado](https://leetcode.com/problems/two-sum-ii-input-array-is-sorted/)

* **Entrada:** `numbers = [2,7,11,15]`, `target = 9`
* **Saída:** `[1,2]` (O LeetCode pede índices *1-based* neste problema.)

## Solução (O(n) / O(1))

```python
def two_sum_sorted(numbers, target):
    l, r = 0, len(numbers) - 1
    while l < r:
        s = numbers[l] + numbers[r]
        if s == target:
            return [l+1, r+1]  # Índices 1-based
        if s < target:
            l += 1
        else:
            r -= 1
    return [-1, -1]

```

## Complexidade:

* **Tempo:** `O(n)`
* **Espaço:** `O(1)`

---

## Passo a passo:

1.  Mantém dois ponteiros, **`l`** (esquerda) e **`r`** (direita), nas extremidades do array.
2.  Calcula a soma: `s = numbers[l] + numbers[r]`.
3.  **Se `s == target`**: Encontrado. Retorna os índices (ajustados para *1-based*).
4.  **Se `s < target`**: A soma é muito pequena. Desloca **`l`** para a direita (`l += 1`) para incluir um número maior na próxima soma.
5.  **Se `s > target`**: A soma é muito grande. Desloca **`r`** para a esquerda (`r -= 1`) para incluir um número menor na próxima soma.
6.  Repetir até que os ponteiros se cruzem (`l < r`) ou o alvo seja encontrado.

---

## 🎯 Outros Problemas Típicos

| Problema | Dificuldade | Link |
|----------|-------------|------|
| [3Sum](https://leetcode.com/problems/3sum/) | Média | [Link](https://leetcode.com/problems/3sum/) |
| [Container With Most Water](https://leetcode.com/problems/container-with-most-water/) | Média | [Link](https://leetcode.com/problems/container-with-most-water/) |
| [Valid Palindrome](https://leetcode.com/problems/valid-palindrome/) | Fácil | [Link](https://leetcode.com/problems/valid-palindrome/) |
| [Remove Duplicates from Sorted Array](https://leetcode.com/problems/remove-duplicates-from-sorted-array/) | Fácil | [Link](https://leetcode.com/problems/remove-duplicates-from-sorted-array/) |
| [Sort Colors](https://leetcode.com/problems/sort-colors/) | Média | [Link](https://leetcode.com/problems/sort-colors/) |