# 🧩 Entendendo o Problema

O problema **LeetCode 3289 - The Two Sneaky Numbers of Digitville** requer que identifiquemos dois números que aparecem duas vezes em uma lista de inteiros que originalmente continha números de `0` a `n-1`, cada um aparecendo exatamente uma vez. Basicamente precisamos encontrar números iguais


## 📌 Exemplo

```python
nums = [0, 1, 2, 3, 2, 4, 5, 3]
```

- **Entrada:** `nums = [0, 1, 2, 3, 2, 4, 5, 3]`
- **Saída:** `[2, 3]`

**Explicação:** Os números `2` e `3` aparecem duas vezes na lista.

---

## 🛠 Abordagem

Para resolver este problema, podemos utilizar um dicionário para armazenar as contagens de cada número. Em seguida, identificamos os números que aparecem mais de uma vez.

### 1️⃣ **Contando Frequências com um Dicionário**

Percorremos a lista `nums` e utilizamos um dicionário para registrar o número de ocorrências de cada elemento.

```python
def findSneakyNumbers(nums):
    frequency = {}  # Inicializamos um dicionário vazio para armazenar as contagens de cada número
    for num in nums:
        if num in frequency:
            frequency[num] += 1  # Se o número já estiver no dicionário, incrementamos sua contagem
        else:
            frequency[num] = 1  # Se for a primeira vez que vemos esse número, adicionamos com contagem 1
    return frequency
```

### 2️⃣ **Identificando os Números Duplicados**

Após contar os números, percorremos o dicionário para encontrar os números que aparecem duas vezes.

```python
def findSneakyNumbers(nums):
    frequency = {}  # Criamos um dicionário para armazenar a contagem de cada número
    for num in nums:
        if num in frequency:
            frequency[num] += 1  # Incrementamos a contagem se o número já estiver presente
        else:
            frequency[num] = 1  # Se for a primeira vez, adicionamos ao dicionário

    sneaky_numbers = [num for num, count in frequency.items() if count == 2]  # Filtramos os números que aparecem exatamente duas vezes
    return sneaky_numbers
```

### 3️⃣ **Função Completa**

```python
def findSneakyNumbers(nums):
    frequency = {}  # Criamos um dicionário para armazenar a contagem de cada número
    for num in nums:
        if num in frequency:
            frequency[num] += 1  # Se o número já foi visto antes, incrementamos a contagem
        else:
            frequency[num] = 1  # Se for a primeira vez, armazenamos com contagem 1

    sneaky_numbers = [num for num, count in frequency.items() if count == 2]  # Identificamos os números com contagem igual a 2
    return sneaky_numbers

# Exemplo de uso
nums = [0, 1, 2, 3, 2, 4, 5, 3]
print(findSneakyNumbers(nums))  # Saída: [2, 3]
```

---

## 🔍 Análise de Complexidade

| Operação | Complexidade |
|----------|-------------|
| Percorrer a lista (`for`) | **O(n)** |
| Buscar um elemento no dicionário (`in frequency`) | **O(1)** |
| Inserir um elemento no dicionário | **O(1)** |
| **Complexidade Total** | **O(n)** |

Esse código é eficiente porque usa um **dicionário (hashmap)** para buscas rápidas (`O(1)`). Se tivéssemos usado dois loops aninhados, a solução teria **O(n²)** de complexidade, o que seria muito mais lento.

---

## 🧠 Explicação Detalhada Linha por Linha

1️⃣ **Criamos um dicionário vazio chamado `frequency` para armazenar a contagem de cada número.**
2️⃣ **Percorremos a lista `nums` e verificamos se cada número já está no dicionário.**
   - Se o número já estiver presente, incrementamos sua contagem.
   - Se for a primeira vez que encontramos o número, adicionamos ao dicionário com valor `1`.
3️⃣ **Após percorrer a lista, usamos uma list comprehension para encontrar os números que aparecem exatamente duas vezes.**
4️⃣ **Retornamos a lista contendo os dois números duplicados.**

---
