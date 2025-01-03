# Фибоначчиева куча

Фибоначчиева куча — это структура данных, предназначенная для эффективного выполнения операций с приоритетной очередью, с амортизированной сложностью для некоторых операций. Она базируется на коллекции деревьев (почти биномиальных) с поддержанием указателя на минимальный элемент.

---

## Топология узла

Каждый узел фибоначчиевой кучи содержит:
- **`value`** — значение узла.
- **`parent`** — указатель на родителя.
- **`left_brother` и `right_brother`** — указатели на соседей узла в списке детей родительского узла.
- **`children_start` и `children_end`** — указатели на начало и конец списка дочерних узлов.
- **`rank`** — количество детей данного узла.
- **`mark`** — флаг, который указывает, был ли удалён один из детей узла. Если узел теряет второго ребёнка, он вырезается из поддерева родителя и добавляется в список корней.

### Ассимптотика для операций с узлами
Операции добавления, удаления или модификации связей в узлах выполняются за \( O(1) \), так как это манипуляции с указателями.

---

## Структура кучи

Фибоначчиева куча представляет собой двусвязный список деревьев (почти биномиальных). Основные элементы структуры:
- **Список корней:** Все деревья в куче представлены в одном двусвязном списке, где хранится информация о рангах деревьев.
- **Минимальный элемент:** Указатель на минимальный элемент в списке корней.

Каждое дерево в фибоначчиевой куче имеет следующие свойства:
1. Узел может иметь произвольное количество детей, которые упорядочены в двусвязном списке.
2. Каждое дерево имеет свой ранг, равный количеству детей корня.
3. Все деревья удовлетворяют свойству кучи: значение в узле меньше или равно значениям в его дочерних узлах.

---

## Операции

### 1. `Insert` (вставка узла)

**Алгоритм:**
1. Создаётся новый узел, который добавляется в список корней.
2. Если новый узел меньше текущего минимального элемента, обновляется указатель на минимум.

**Временная сложность:**
- Создание нового узла и добавление его в список корней: \( O(1) \).
- Обновление указателя на минимум: \( O(1) \).

**Итого:** \( O(1) \).

**Доказательство:**
- Вставка узла в список корней требует манипуляции с указателями (вставка в начало/конец двусвязного списка), что выполняется за \( O(1) \).
- Обновление минимума — это простое сравнение нового значения с текущим минимумом, что занимает \( O(1) \).

---

### 2. `Merge` (объединение двух куч)

**Алгоритм:**
1. Два списка корней объединяются в один.
2. Если минимальный элемент второй кучи меньше текущего минимального элемента, обновляется указатель на минимум.

**Временная сложность:**
- Слияние списков корней: \( O(1) \).
- Обновление указателя на минимум: \( O(1) \).

**Итого:** \( O(1) \).

**Доказательство:**
- Слияние двух списков корней осуществляется путём манипуляции с указателями на начало и конец списков, что занимает \( O(1) \).
- Обновление минимума требует одного сравнения, выполняемого за \( O(1) \).

---

### 3. `GetMin` (получение минимального элемента)

**Алгоритм:**
1. Возвращается узел, на который указывает указатель на минимум.

**Временная сложность:**
- Операция выполняется за \( O(1) \), так как не требует обхода дерева или списка.

**Доказательство:**
- Минимальный элемент всегда поддерживается указателем, и его получение — это операция доступа к памяти, что выполняется за \( O(1) \).

---

## Итоговая таблица сложностей операций

| Операция   | Алгоритм                     | Сложность     |
|------------|------------------------------|---------------|
| `Insert`   | Добавление нового узла       | \( O(1) \)    |
| `Merge`    | Слияние списков корней       | \( O(1) \)    |
| `GetMin`   | Доступ к минимальному узлу   | \( O(1) \)    |

---

можно похавать информацию из https://neerc.ifmo.ru/wiki/index.php?title=%D0%A4%D0%B8%D0%B1%D0%BE%D0%BD%D0%B0%D1%87%D1%87%D0%B8%D0%B5%D0%B2%D0%B0_%D0%BA%D1%83%D1%87%D0%B0

а еще мне понравилось на https://github.com/Algorithms-and-Data-Structures-2021/semester-work-fibonacci-heap
