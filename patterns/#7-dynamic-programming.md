# 7) Dynamic Programming (Programação Dinâmica - DP)

**Quando usar:**

* Problemas que apresentam **subestrutura ótima** (a solução ótima é construída a partir de soluções ótimas de subproblemas) e **subproblemas sobrepostos** (os mesmos subproblemas são resolvidos repetidamente).
* Exemplos: Otimização sequencial (como este), subsequências, caminhos mínimos/máximos, somas alvo, problemas de mochila.

## Problema de Exemplo: House Robber

O objetivo é maximizar a quantia roubada sem roubar casas adjacentes.

* **Entrada:** `nums = [1,2,3,1]`
* **Saída:** `4` (Roubar `1 + 3`)

## Solução Ótima (O(n) / O(1)) - Otimização de Espaço

```python
def rob(nums):
    prev = 0   # max_money roubado até a casa i-2
    curr = 0   # max_money roubado até a casa i-1
    
    for num in nums:
        # Novo curr (max_money até a casa i):
        # Opção 1: Não roubar a casa atual (num), então o max é o max anterior (curr).
        # Opção 2: Roubar a casa atual (num), então o max é (prev + num).
        
        # Atualiza o 'prev' para ser o antigo 'curr' antes de calcular o novo 'curr'
        prev, curr = curr, max(curr, prev + num)
        
    return curr
```

## Complexidade:

* **Tempo:** `O(n)` (Cada casa é visitada exatamente uma vez.)
* **Espaço:** `O(1)` (Usamos apenas duas variáveis auxiliares, `prev` e `curr`.)

---

## Passo a passo (Otimização de Espaço):

1.  **`curr`** guarda a melhor solução (máximo dinheiro roubado) até a **casa anterior** (`i-1`).
2.  **`prev`** guarda a melhor solução (máximo dinheiro roubado) até a **casa anterior à anterior** (`i-2`).
3.  Para cada casa (`num`) na iteração, decidimos se a roubamos ou não:
    * **Não Roubar:** O resultado é `curr` (o máximo até a casa anterior).
    * **Roubar:** O resultado é `prev + num` (o máximo até a casa `i-2` mais o valor da casa atual, porque não podemos roubar a casa `i-1`).
4.  O novo máximo (`max(curr, prev + num)`) torna-se o **novo `curr`**, e o antigo `curr` é promovido a **novo `prev`**.