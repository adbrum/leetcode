# 2) Sliding Window (Janela Deslizante)

**Quando usar:**

* Para procurar **subarrays/substrings contínuos** que satisfazem uma determinada condição (Exemplos: soma máxima/fixa, sem caracteres repetidos, contagem de anagramas).

## Problema de Exemplo: Longest Substring Without Repeating Characters

* **Entrada:** `s = "abcabcbb"`
* **Saída:** `3` (A substring mais longa é `"abc"`)

## Solução (O(n) / O(min(n, charset)))

```python
def length_of_longest_substring(s: str) -> int:
    last = {}      # char -> last index
    start = 0
    best = 0
    for i, ch in enumerate(s):
        # Se o caractere já foi visto e a sua última posição está dentro da janela [start, i)
        if ch in last and last[ch] >= start:
            # Move o início da janela para logo após a última ocorrência do caractere
            start = last[ch] + 1
        
        # Atualiza a última posição do caractere atual
        last[ch] = i
        
        # Atualiza o melhor resultado com o tamanho da janela atual (i - start + 1)
        best = max(best, i - start + 1)
    return best
```

## Complexidade:

* **Tempo:** `O(n)` (Cada caractere é processado uma vez.)
* **Espaço:** `O(\min(n, \text{size\_of\_charset}))` (Armazena no máximo o número de caracteres únicos na string ou o tamanho do alfabeto.)

---

## Passo a passo:

1.  Mantém o índice de **início da janela** (`start`) e um mapa/dicionário (`last`) para registar a **última posição** de cada caractere.
2.  Itera a string, usando o índice **`i`** como o fim da janela.
3.  Ao encontrar um caractere que **já está na janela** (`last[ch] >= start`), move o **`start`** da janela para **depois da última ocorrência** desse caractere repetido.
4.  Atualiza a última posição do caractere atual no mapa.
5.  Atualiza a variável **`best`** com o tamanho atual da janela (`i - start + 1`).