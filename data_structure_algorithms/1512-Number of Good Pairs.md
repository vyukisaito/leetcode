# LeetCode 1512 - Number of Good Pairs

O problema **Number of Good Pairs** pede que encontremos o número de pares "bons" dentro de uma lista.  
Esses pares devem seguir a seguinte regra:
- `nums[i] == nums[j]`  
- `i < j`  

### 📌 Exemplo
```python
nums = [1, 2, 3, 1, 1, 3]
```
Os pares bons são:
- `(0, 3) → nums[0] == nums[3] (1 == 1)`
- `(0, 4) → nums[0] == nums[4] (1 == 1)`
- `(2, 5) → nums[2] == nums[5] (3 == 3)`
- `(3, 4) → nums[3] == nums[4] (1 == 1)`

Total: **4 pares bons**.

---

## 🚀 Solução Otimizada - Usando um Dicionário (**O(n)**)
Podemos contar a frequência dos números usando um **dicionário (hashmap)** para evitar comparações desnecessárias.

```python
class Solution:
    def numIdenticalPairs(self, nums: List[int]) -> int:
        count = Counter(nums)
        good_pairs = 0

        for c in count.values():
            good_pairs += (c * (c - 1)) // 2

        return good_pairs
```

### 🔎 Explicação
1️⃣ **Usamos `Counter` para contar quantas vezes cada número aparece na lista.**  
   - O `Counter(nums)` cria um **dicionário** onde as **chaves** são os números e os **valores** são suas frequências.  
   - Exemplo:
     ```python
     nums = [1, 2, 3, 1, 1, 3]
     Counter(nums)  # Saída: {1: 3, 3: 2, 2: 1}
     ```
   - Ou seja temos três 1, dois 3 e um 2.

2️⃣ **Iteramos pelos valores do `Counter`, que representam as quantidades de cada número.**  
   - Para cada número em `c`, calculamos quantos pares podem ser formados.
   ```python
   nums = [1, 2, 3, 1, 1, 3]
   count = Counter(nums)
   print(count.values()) # Saída: dict_values([3, 1, 2])
   ```
   
3️⃣ **Usamos a fórmula de combinação:**  
   
   Se um número aparece `n` vezes, podemos formar pares escolhendo dois índices distintos:
   
   \[
   C(n, 2) = \frac{n(n - 1)}{2}
   \]
   
   - Exemplo: Se o número `1` aparece 3 vezes (`1,1,1`), os pares possíveis são:
     ```
     (0,1), (0,2), (1,2)
     ```
     O que equivale a \( \frac{3(3-1)}{2} = \frac{3 \times 2}{2} = 3 \).

🔹 **Complexidade:** **O(n)**, pois percorremos a lista apenas duas vezes: uma para contar os números e outra para calcular os pares.

---

## 🐌 Solução Ineficiente - Força Bruta (**O(n²)**)
Uma solução mais simples, mas menos eficiente, seria usar dois loops para comparar todos os pares:

```python
class Solution:
    def numIdenticalPairs(self, nums: List[int]) -> int:
        count = 0
        for i in range(len(nums)):
            for j in range(i + 1, len(nums)):
                if nums[i] == nums[j]:
                    count += 1
        return count
```

🔹 **Complexidade:** **O(n²)**, pois comparamos todos os pares possíveis.

---

## ⚡ Comparação das Soluções

| Método | Complexidade |
|--------|-------------|
| **Força Bruta (2 loops)** | O(n²) |
| **Dicionário (hashmap)** | O(n) |

---

## 🎯 Conclusão
✅ **Se a lista for grande**, a abordagem com **dicionário** é a melhor opção, pois é **O(n)**.  
✅ **Se a lista for pequena**, a abordagem **ingênua** pode ser usada sem problemas.  

