# 12) Trie (Prefix Tree / Árvore de Prefixo)

**Quando usar:**

* **Buscas por prefixos** (ex.: encontrar todas as palavras que começam com "ap").
* Sistemas de **autocomplete** e sugestões de palavras.
* Construção de dicionários de palavras e problemas como *Word Search II* otimizado.

## Problema de Exemplo: [Implement Trie](https://leetcode.com/problems/implement-trie-prefix-tree/)

Implementar as três operações principais de uma Trie:

* `insert("apple")`
* `search("apple")` `\rightarrow` `True`
* `startsWith("app")` `\rightarrow` `True`

## Solução (O(m) por operação, onde m é o tamanho da palavra)

```python
class TrieNode:
    def __init__(self):
        # Dicionário mapeia caractere para o próximo TrieNode
        self.children = {}
        # Indica se este nó finaliza uma palavra válida
        self.is_word = False

class Trie:
    def __init__(self):
        self.root = TrieNode()

    def insert(self, word: str) -> None:
        node = self.root
        for ch in word:
            # Se o caractere não existir, cria um novo nó; senão, move para o nó existente
            node = node.children.setdefault(ch, TrieNode())
        # Marca o último nó como o fim de uma palavra
        node.is_word = True

    def search(self, word: str) -> bool:
        node = self.root
        for ch in word:
            if ch not in node.children: 
                return False
            node = node.children[ch]
        # A palavra só existe se chegarmos ao final E o nó estiver marcado como is_word=True
        return node.is_word

    def startsWith(self, prefix: str) -> bool:
        node = self.root
        for ch in prefix:
            if ch not in node.children: 
                return False
            node = node.children[ch]
        # O prefixo existe se chegarmos ao final, independentemente de is_word
        return True
```

## Complexidade:

* **Tempo:** `O(m)` por operação, onde `m` é o comprimento da palavra/prefixo. (A complexidade não depende do número total de palavras `N`).
* **Espaço:** `O(\text{total de caracteres distintos})` (Para armazenar todos os caracteres de todas as palavras).

---

## Passo a passo:

1.  **Estrutura:** Cada **`TrieNode`** contém um mapa (`children`) para os seus filhos (os próximos caracteres possíveis) e um *flag* booleano (`is_word`).
2.  **`insert`:**
    * Percorre a palavra caractere a caractere, começando pela `root`.
    * Para cada caractere, move para o nó correspondente. Se o nó não existir, ele é **criado**.
    * Após processar o último caractere, o *flag* **`is_word`** é definido como `True` nesse nó final.
3.  **`search`:**
    * Percorre a palavra. Se, a qualquer momento, um caractere **não for encontrado** no `children` do nó atual, a palavra não existe: retorna `False`.
    * Se chegar ao fim, retorna o *status* do *flag* **`is_word`** do nó final.
4.  **`startsWith`:**
    * Funciona como `search`, mas se chegar ao fim do prefixo sem encontrar caracteres ausentes, retorna **`True`** (não precisa verificar o *flag* `is_word`).

---

## 🎯 Outros Problemas Típicos

| Problema | Dificuldade | Link |
|----------|-------------|------|
| [Word Search II](https://leetcode.com/problems/word-search-ii/) | Difícil | [Link](https://leetcode.com/problems/word-search-ii/) |
| [Design Add and Search Words Data Structure](https://leetcode.com/problems/design-add-and-search-words-data-structure/) | Média | [Link](https://leetcode.com/problems/design-add-and-search-words-data-structure/) |
| [Maximum XOR of Two Numbers in an Array](https://leetcode.com/problems/maximum-xor-of-two-numbers-in-an-array/) | Média | [Link](https://leetcode.com/problems/maximum-xor-of-two-numbers-in-an-array/) |
| [Replace Words](https://leetcode.com/problems/replace-words/) | Média | [Link](https://leetcode.com/problems/replace-words/) |
| [Palindrome Pairs](https://leetcode.com/problems/palindrome-pairs/) | Difícil | [Link](https://leetcode.com/problems/palindrome-pairs/) |