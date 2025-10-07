# 3) Fast & Slow Pointers (Ponteiros Rápido/Lento)

**Nome Alternativo:** Floyd’s Cycle-Finding Algorithm

**Quando usar:**

* Detetar **ciclos** em listas ligadas (Linked Lists).
* Encontrar o **nó inicial** do ciclo.
* Também usado para encontrar o **meio** da lista ligada.

## Problema de Exemplo: [Linked List Cycle II — Encontrar Início do Ciclo](https://leetcode.com/problems/linked-list-cycle-ii/)

* **Entrada (Visual):** `head` de uma lista que contém ciclo (Exemplo: `3 → 2 → 0 → -4`, com o nó `-4` a apontar de volta para o nó `2`).
* **Saída:** Nó que começa o ciclo (o nó com valor **`2`** no exemplo) — ou `None` se não houver ciclo.

## Solução (O(n) / O(1))

```python
class ListNode:
    def __init__(self, val=0, next=None):
        self.val = val
        self.next = next

def detectCycle(head):
    slow = fast = head
    
    # Primeira fase: Encontrar o ponto de encontro (se existir um ciclo)
    while fast and fast.next:
        slow = slow.next
        fast = fast.next.next
        
        if slow == fast:
            # Segunda fase: Encontrar o início do ciclo
            ptr = head  # Ponteiro que começa no início da lista
            
            # Ambos avançam um passo de cada vez. Onde se encontrarem é o início do ciclo.
            while ptr != slow:
                ptr = ptr.next
                slow = slow.next
            return ptr
            
    return None

```

## Complexidade:

* **Tempo:** `O(n)`
* **Espaço:** `O(1)`

---

## Passo a passo (Floyd's Algorithm):

1.  Usa dois ponteiros: **`fast`** (avança 2 passos) e **`slow`** (avança 1 passo).
2.  **Se se encontrarem** (`slow == fast`), um ciclo existe.
3.  **Para achar o início do ciclo:**
    * Coloca um novo ponteiro (`ptr`) no **`head`** da lista.
    * Move ambos (`ptr` e `slow` - o ponteiro que estava no encontro) **1 passo de cada vez**.
    * O nó onde se cruzarem é o **nó inicial do ciclo**.

---

## 🎯 Outros Problemas Típicos

| Problema | Dificuldade | Link |
|----------|-------------|------|
| [Middle of the Linked List](https://leetcode.com/problems/middle-of-the-linked-list/) | Fácil | [Link](https://leetcode.com/problems/middle-of-the-linked-list/) |
| [Palindrome Linked List](https://leetcode.com/problems/palindrome-linked-list/) | Fácil | [Link](https://leetcode.com/problems/palindrome-linked-list/) |
| [Remove Nth Node From End of List](https://leetcode.com/problems/remove-nth-node-from-end-of-list/) | Média | [Link](https://leetcode.com/problems/remove-nth-node-from-end-of-list/) |
| [Reorder List](https://leetcode.com/problems/reorder-list/) | Média | [Link](https://leetcode.com/problems/reorder-list/) |
| [Happy Number](https://leetcode.com/problems/happy-number/) | Fácil | [Link](https://leetcode.com/problems/happy-number/) |