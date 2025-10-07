# 13) Bit Manipulation (Operações Bitwise)

**Quando usar:**

* Problemas que envolvem **somas, contagens ou propriedades a nível de bit**.
* Encontrar elementos **únicos** entre duplicados (usando XOR).
* Representar e manipular **estados em *bitmask*** (comum em problemas de DP de *subset*).
* Operações matemáticas rápidas (deslocamento para multiplicação/divisão por potências de 2).

## Problema de Exemplo: [Single Number](https://leetcode.com/problems/single-number/)

Encontrar o único elemento que aparece uma vez, enquanto todos os outros aparecem duas vezes.

* **Entrada:** `nums = [2,2,1]`
* **Saída:** `1`

## Solução (O(n) / O(1))

```python
def singleNumber(nums):
    res = 0
    for x in nums:
        # XOR de todos os números
        res ^= x
    return res
```

## Complexidade:

* **Tempo:** `O(n)` (Cada número é processado uma vez.)
* **Espaço:** `O(1)` (Apenas uma variável auxiliar, `res`, é utilizada.)

---

## Passo a passo:

1.  A chave está na propriedade da operação **XOR (`^`)**:
    * `A \oplus A = 0` (XOR de um número consigo mesmo é zero).
    * `A \oplus 0 = A` (XOR com zero é o próprio número).
    * XOR é **comutativa e associativa** (`A \oplus B \oplus A = (A \oplus A) \oplus B = 0 \oplus B = B`).
2.  Inicializa-se o resultado (**`res`**) a `0`.
3.  Percorre-se o array, aplicando XOR cumulativamente a todos os elementos (`res ^= x`).
4.  No final, todos os pares de números duplicados anulam-se (resultam em `0`), e o único número que não tem par é o que resta no `res`.

---

## 🎯 Outros Problemas Típicos

| Problema | Dificuldade | Link |
|----------|-------------|------|
| [Number of 1 Bits](https://leetcode.com/problems/number-of-1-bits/) | Fácil | [Link](https://leetcode.com/problems/number-of-1-bits/) |
| [Counting Bits](https://leetcode.com/problems/counting-bits/) | Fácil | [Link](https://leetcode.com/problems/counting-bits/) |
| [Reverse Bits](https://leetcode.com/problems/reverse-bits/) | Fácil | [Link](https://leetcode.com/problems/reverse-bits/) |
| [Missing Number](https://leetcode.com/problems/missing-number/) | Fácil | [Link](https://leetcode.com/problems/missing-number/) |
| [Sum of Two Integers](https://leetcode.com/problems/sum-of-two-integers/) | Média | [Link](https://leetcode.com/problems/sum-of-two-integers/) |