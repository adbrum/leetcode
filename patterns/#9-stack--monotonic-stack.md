# 9) Stack / Monotonic Stack (Pilha Monotónica)

**Quando usar:**

* **Validação de parênteses** ou expressões.
* Calcular o **próximo maior/menor elemento** (*Next Greater/Smaller Element*).
* Problemas como *Skyline* ou onde é necessário manter uma **ordem estritamente crescente ou decrescente**.
* Conversão entre notações de expressões.

## Problema de Exemplo: Daily Temperatures

O objetivo é retornar quantos dias você deve esperar após um dia para que a temperatura seja mais alta.

* **Entrada:** `T = [73,74,75,71,69,72,76,73]`
* **Saída:** `[1,1,4,2,1,1,0,0]`

## Solução (O(n) / O(n)) - Monotonic Stack

```python
def dailyTemperatures(T):
    n = len(T)
    res = [0] * n
    stack = []  # O stack guarda **índices** das temperaturas, mantendo-as em ordem decrescente (Monotonic Decreasing Stack)
    
    for i, t in enumerate(T):
        # Enquanto o stack não estiver vazio E a temperatura no topo do stack (T[stack[-1]]) for menor que a atual (t)
        while stack and T[stack[-1]] < t:
            # Encontrámos o "Next Greater Element" para o índice no topo
            idx = stack.pop()
            
            # O resultado é a diferença entre o índice atual (i) e o índice resolvido (idx)
            res[idx] = i - idx
            
        # Adiciona o índice atual ao stack. O stack agora mantém a monotonicidade.
        stack.append(i)
        
    return res
```

## Complexidade:

* **Tempo:** `O(n)` (Cada índice é empurrado para o *stack* no máximo uma vez e retirado no máximo uma vez, resultando em `O(2n)` operações.)
* **Espaço:** `O(n)` (No pior caso, o *stack* pode armazenar todos os `n` índices, como numa sequência decrescente.)

---

## Passo a passo:

1.  Usa um **Monotonic Decreasing Stack** que armazena os **índices** das temperaturas que ainda não encontraram a sua "próxima temperatura mais alta".
2.  Percorre as temperaturas de **`T`** do início ao fim.
3.  Para a temperatura atual (`t` no índice `i`):
    * Enquanto o *stack* não estiver vazio e a temperatura no topo (`T[stack[-1]]`) for **menor** que a atual (`t`), isso significa que `t` é a "próxima maior" para o índice no topo.
    * Retira (`pop`) esse índice resolvido (`idx`) do *stack* e calcula o resultado: `res[idx] = i - idx`.
4.  Após resolver todos os elementos mais pequenos, o índice atual (`i`) é adicionado ao *stack* para manter a ordem decrescente.
5.  Os elementos que permanecem no *stack* no final nunca encontram uma temperatura maior, pelo que o seu resultado permanece `0`.