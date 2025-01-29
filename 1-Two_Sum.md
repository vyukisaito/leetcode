# 🧩 Entendendo o Problema  
O problema **Two Sum** pede que encontremos dois números dentro de uma lista (`nums`) que, quando somados, resultam em um valor `target`. Devemos retornar os índices desses dois números.  

## 📌 Exemplo:
```python
nums = [2, 7, 11, 15]
target = 9
```
A soma de `2 + 7 = 9`, então a resposta correta é `[0, 1]`, pois `2` está no índice `0` e `7` no índice `1`.  

---

## 🛠 Explicando linha por linha  

### 1️⃣ **Criamos um dicionário (`num_idx`), um hashmap para armazenar os números e seus índices:**
```python
class Solution:
    def twoSum(self, nums: List[int], target: int) -> List[int]:
        num_idx = {}
```
Esse dicionário ajuda a encontrar rapidamente se um número complementar já apareceu antes.  

### 2️⃣ **Iteramos sobre a lista `nums` com `enumerate` para obter o índice e o número:**
```python
class Solution:
    def twoSum(self, nums: List[int], target: int) -> List[int]:
        num_idx = {}

        for i, num in enumerate(nums):
```
O `enumerate` retorna dois valores:
* `i` → O índice do número na lista  
* `num` → O valor do número na posição `i`  

### 3️⃣ **Verificamos se o complemento (`target - num`) já está no dicionário:**
```python
class Solution:
    def twoSum(self, nums: List[int], target: int) -> List[int]:
        num_idx = {}

        for i, num in enumerate(nums):
            if target - num in num_idx:
```
Se `target - num` já estiver no dicionário, significa que já vimos um número que, somado ao atual, resulta no `target`.  
Essa linha verifica se o complemento do número atual (num) já está no dicionário `num_idx`.

Mas o que é esse complemento?

O complemento de `num` é o número que, somado a `num`, resulta no `target`. Em outras palavras:

`complemento = target − num`

Se esse complemento já foi visto antes (ou seja, se ele já está no dicionário `num_idx`), então já temos os dois números necessários para formar a soma desejada.

Exemplo:

target (alvo, objetivo) = 9
num = 2
complemento = 9 - 2
complemento = 7


### 4️⃣ **Se encontramos o complemento, retornamos os índices correspondentes:**
```python
class Solution:
    def twoSum(self, nums: List[int], target: int) -> List[int]:
        num_idx = {}

        for i, num in enumerate(nums):
            if target - num in num_idx:
                return [i, num_idx[target - num]]
```
Nesta etapa, encontramos um número que, somado ao número atual (`num`), resulta no `target`. 

- `target - num in num_idx`: Verifica se o número complementar já foi visto antes e está armazenado no dicionário `num_idx`.
- `return [i, num_idx[target - num]]`: Como encontramos a solução, retornamos imediatamente uma lista contendo:
  - `i`: O índice do número atual.
  - `num_idx[target - num]`: O índice do número complementar, que já foi armazenado anteriormente no dicionário.

Isso garante que a solução seja encontrada de maneira eficiente, sem precisar percorrer a lista novamente.


### 5️⃣ **Se não encontramos o complemento, armazenamos o número e seu índice no dicionário:**
```python
class Solution:
    def twoSum(self, nums: List[int], target: int) -> List[int]:
        num_idx = {}

        for i, num in enumerate(nums):
            if target - num in num_idx:
                return [i, num_idx[target - num]]
            num_idx[num] = i
```
Isso garante que o número estará disponível para futuras verificações.  

---

## 🔎 Exemplo Passo a Passo  

### 📌 Entrada:
```python
nums = [2, 7, 11, 15]
target = 9
```

### 🔎 Iterações:

| `i`  | `num` | `target - num` | `num_idx` antes  | Encontrado? | `num_idx` depois |
|------|------|---------------|--------------|------------|---------------|
| 0    | 2    | 7             | `{}`          | ❌ Não     | `{2: 0}`       |
| 1    | 7    | 2             | `{2: 0}`      | ✅ Sim     | Retorna `[1, 0]` |

Quando chegamos no número `7` (`i = 1`), percebemos que `target - num = 9 - 7 = 2`, e `2` já estava no dicionário! Então retornamos `[1, 0]`.  

---

## ⏳ Análise de Complexidade  

| Operação | Complexidade |
|----------|-------------|
| Percorrer a lista (`for`) | **O(n)** |
| Buscar um elemento no dicionário (`in num_idx`) | **O(1)** |
| Inserir um elemento no dicionário | **O(1)** |
| **Complexidade Total** | **O(n)** |

Esse código é eficiente porque usa um **dicionário (hashmap)** para buscas rápidas (`O(1)`). Se tivéssemos usado dois loops aninhados, a solução teria **O(n²)** de complexidade, o que seria muito mais lento.  

---

## ⚡ Comparação com um Algoritmo com força bruta  

Um algoritmo com dois loops (`O(n²)`), seria algo assim:
```python
for i in range(len(nums)):  # Primeiro número
    for j in range(i + 1, len(nums)):  # Segundo número
        if nums[i] + nums[j] == target:
            return [i, j]
```
Aqui, estamos comparando **todos os pares possíveis**, o que é lento (`O(n²)`).  

Nosso código evita isso armazenando números no dicionário (`O(1)`) e resolvendo o problema em apenas uma passagem (`O(n)`).  

---

