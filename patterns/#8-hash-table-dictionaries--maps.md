# 8) Hash Table (Dicionários / Mapas)

**Quando usar:**

* Para busca de **complementos** (como no Two Sum).
* Para contagem de **frequências** de elementos.
* Para checagem de **existência** ou acesso a dados numa complexidade de `O(1)` (tempo constante).

## Problema de Exemplo: [Two Sum — Índices em Qualquer Ordem](https://leetcode.com/problems/two-sum/)

* **Entrada:** `nums = [2,7,11,15]`, `target = 9`
* **Saída:** `[0,1]`

## Solução (O(n) / O(n))

```python
def two_sum(nums, target):
    seen = {}  # Mapeia: valor -> índice
    for i, x in enumerate(nums):
        want = target - x  # Calcula o complemento necessário
        
        # 1. Verifica se o complemento já foi visto
        if want in seen:
            return [seen[want], i]
        
        # 2. Se não, guarda o elemento atual e o seu índice para futuras verificações
        seen[x] = i
        
    # Deve sempre haver uma solução, conforme a premissa do problema LeetCode
    raise ValueError("No solution")
```

## Complexidade:

* **Tempo:** `O(n)` (Apenas uma passagem sobre o array, onde a busca e a inserção no *hash table* são `O(1)` em média.)
* **Espaço:** `O(n)` (No pior caso, o *hash table* armazena todos os `n` elementos do array.)

---

## Passo a passo:

1.  Cria um **Hash Table (`seen`)** para armazenar os valores já vistos e os seus respetivos índices.
2.  Percorre o array `nums` uma única vez.
3.  Para cada elemento **`x`** no índice **`i`**, calcula o **complemento** necessário: `want = target - x`.
4.  Verifica se esse **`want`** já existe no `seen`.
5.  **Se sim:** Significa que o par foi encontrado. Devolve `[seen[want], i]`.
6.  **Se não:** Guarda o elemento atual (`x`) e o seu índice (`i`) no *Hash Table* para ser usado como complemento em iterações futuras.

---

## 🎯 Outros Problemas Típicos

| Problema | Dificuldade | Link |
|----------|-------------|------|
| [Group Anagrams](https://leetcode.com/problems/group-anagrams/) | Média | [Link](https://leetcode.com/problems/group-anagrams/) |
| [Contains Duplicate](https://leetcode.com/problems/contains-duplicate/) | Fácil | [Link](https://leetcode.com/problems/contains-duplicate/) |
| [Logger Rate Limiter](https://leetcode.com/problems/logger-rate-limiter/) | Fácil | [Link](https://leetcode.com/problems/logger-rate-limiter/) |
| [Subarray Sum Equals K](https://leetcode.com/problems/subarray-sum-equals-k/) | Média | [Link](https://leetcode.com/problems/subarray-sum-equals-k/) |
| [Top K Frequent Elements](https://leetcode.com/problems/top-k-frequent-elements/) | Média | [Link](https://leetcode.com/problems/top-k-frequent-elements/) |