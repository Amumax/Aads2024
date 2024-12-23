# Разбор билета: Биномиальная куча

## 1. Биномиальная куча (Биномиальное дерево)

**Биномиальная куча** — это структура данных, представляющая собой коллекцию биномиальных деревьев, которая используется для реализации очередей с приоритетами. Биномиальная куча позволяет эффективно выполнять такие операции, как:
- вставка элемента,
- извлечение минимального элемента,
- уменьшение ключа и другие.

### Свойства биномиальной кучи:
- **Состав куч**: Биномиальная куча состоит из нескольких биномиальных деревьев. Каждое биномиальное дерево Bk в куче — это дерево с **2^k** вершинами, которое является минимальной кучей, и структура этих деревьев следуют следующим правилам:
  - Каждое дерево уровня k имеет точно 2^k вершин.
  - Деревья с разными уровнями могут быть представлены в куче одновременно.

- **Порядок деревьев**: Состав биномиальной кучи соответствует двоичному разложению числа n (общее количество элементов в куче). Например, если в куче 13 элементов, то куча будет состоять из деревьев уровней B0, B1 и B3 (так как 13 = 2^0 + 2^1 + 2^3).

- **Количество вершин**: Если биномиальная куча состоит из n элементов, то количество биномиальных деревьев в куче будет равно числу разрядов в двоичной записи числа n (или уровней, соответствующих деревьям). Таким образом, в худшем случае высота дерева — **O(log n)**.

## 2. Процедуры биномиальной кучи

### 2.1. **SiftDown** (Просеивание вниз)

**Принцип работы**: Процедура `SiftDown` используется для поддержания свойств кучи после того, как минимальный элемент был удален, либо при необходимости перестроить кучу после изменения элемента. Основные шаги:
1. Начинаем с корня дерева.
2. Сравниваем его с двумя детьми (если они существуют).
3. Если родитель больше любого из своих детей, меняем его с меньшим из детей.
4. Повторяем процесс для поддерева, в котором произошел обмен.

**Сложность**: В худшем случае, процедура `SiftDown` будет иметь сложность **O(log n)**, так как операция выполняется до самой глубокой вершины дерева, которая имеет высоту **log n**.

### 2.2. **SiftUp** (Просеивание вверх)

**Принцип работы**: Процедура `SiftUp` применяется при добавлении нового элемента или изменении значения ключа в элементе, чтобы восстановить свойства кучи:
1. Начинаем с измененного элемента.
2. Если ключ этого элемента меньше, чем ключ родителя, то меняем их местами.
3. Повторяем процесс до тех пор, пока свойство кучи не будет восстановлено.

**Сложность**: Процесс `SiftUp` имеет сложность **O(log n)**, так как перемещения происходят по высоте дерева, которая в худшем случае составляет **log n**.

### 2.3. **DecreaseKey** (Уменьшение ключа)

**Принцип работы**: Эта операция используется для уменьшения значения ключа в одном из элементов кучи:
1. Уменьшаем ключ элемента.
2. После изменения ключа вызываем `SiftUp`, чтобы восстановить порядок в куче.

**Сложность**: Операция `DecreaseKey` также имеет сложность **O(log n)**, так как в худшем случае после уменьшения ключа потребуется выполнить `SiftUp` по высоте дерева.

## 3. Слияние биномиальных куч

Одним из важных свойств биномиальных куч является операция слияния двух куч. Слияние двух биномиальных куч выполняется за время **O(log n)**, так как оно сводится к слиянию деревьев одинаковых уровней.

### Принцип работы слияния:
1. Сливаются деревья одинаковых уровней по принципу суммирования их двоичных разрядов (аналогично сложению чисел в двоичной системе).
2. При слиянии двух деревьев уровня k, если они оба существуют, формируется дерево уровня k+1.

## 4. Сложность операций

- **Вставка** элемента: операция вставки требует слияния одного элемента с кучей, что выполняется за **O(log n)**.
- **Удаление минимального элемента**: операция удаления минимального элемента из кучи также выполняется за **O(log n)**, так как после извлечения минимального элемента необходимо восстановить структуру кучи.
- **Извлечение минимального элемента**: сложность извлечения минимального элемента — **O(log n)**, так как необходимо искать минимальный элемент среди всех деревьев.
- **Слияние двух куч**: операция слияния двух куч выполняется за **O(log n)**, как описано выше.

инфу хаваемс как обычно из https://neerc.ifmo.ru/wiki/index.php?title=%D0%91%D0%B8%D0%BD%D0%BE%D0%BC%D0%B8%D0%B0%D0%BB%D1%8C%D0%BD%D0%B0%D1%8F_%D0%BA%D1%83%D1%87%D0%B0