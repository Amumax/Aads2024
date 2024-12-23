# Красно-черное дерево

## Определение

**Красно-черное дерево** — это самобалансирующееся двоичное дерево поиска, в котором каждый узел имеет дополнительный атрибут — цвет, принимающий одно из двух значений: красный или черный. Дерево удовлетворяет следующим свойствам:

1. **Каждый узел либо красный, либо черный.**
2. **Корень дерева всегда черный.**
3. **Все листья (фиктивные узлы) считаются черными.**
4. **Если узел красный, то оба его дочерних узла должны быть черными.**
5. **Все пути от любого узла до его листьев содержат одинаковое количество черных узлов.**

Эти свойства обеспечивают балансировку дерева, гарантируя, что максимальная высота дерева не превышает $2 \log(n + 1)$, где $n$ — количество внутренних узлов. ([neerc.ifmo.ru](https://neerc.ifmo.ru/wiki/index.php?title=%D0%9A%D1%80%D0%B0%D1%81%D0%BD%D0%BE-%D1%87%D0%B5%D1%80%D0%BD%D0%BE%D0%B5_%D0%B4%D0%B5%D1%80%D0%B5%D0%B2%D0%BE&utm_source=chatgpt.com))

---

## Теорема о высоте

**Теорема:** В красно-черном дереве с $n$ внутренними узлами высота дерева не превышает $2 \log(n + 1)$.

### Доказательство:

1. **Черная высота $bh(x)$ :** Определим черную высоту узла $x$ как количество черных узлов на любом пути от $x$ до листа, не включая сам $x$. По свойству 5, все такие пути содержат одинаковое количество черных узлов.

2. **Минимальное количество узлов:** Докажем по индукции, что поддерево с черной высотой $bh$ содержит не менее $2^{bh} - 1$ внутренних узлов.

   - **База индукции:** Для $bh = 0$ поддерево состоит только из одного листа (фиктивного узла), и внутренних узлов нет. Следовательно, $2^0 - 1 = 0$.

   - **Переход:** Предположим, что для черной высоты $k$ поддерево содержит не менее $2^k - 1$ внутренних узлов. Рассмотрим поддерево с черной высотой $k + 1$. Корень этого поддерева может быть либо черным, либо красным. Если корень черный, его дочерние поддеревья имеют черную высоту $k$. По предположению индукции, каждое из них содержит не менее $2^k - 1$ внутренних узлов. Таким образом, общее количество внутренних узлов:

     $1 + 2 \times (2^k - 1) = 1 + 2^{k+1} - 2 = 2^{k+1} - 1$

     Если корень красный, его дочерние поддеревья имеют черную высоту $k + 1$. Однако по свойству 4 красный узел не может иметь красных детей, поэтому его дочерние узлы должны быть черными, и их черная высота будет $k$. Аналогично предыдущему случаю, общее количество внутренних узлов будет не менее $2^{k+1} - 1$.

3. **Связь между черной высотой и общей высотой:** В худшем случае красно-черное дерево чередует красные и черные узлы. Следовательно, если черная высота дерева равна $bh$, то общая высота дерева не превышает $2 \times bh$.

4. **Оценка высоты дерева:** Пусть $h$ — высота дерева, а $bh$ — его черная высота. Тогда:

   $n \geq 2^{bh} - 1$

   Отсюда:

   $bh \leq \log_2(n + 1)$

   Следовательно, высота дерева:

   $h \leq 2 \times bh \leq 2 \times \log_2(n + 1)$

---

### Вывод:
Высота красно-черного дерева с $n$ внутренними узлами не превышает $2 \log_2(n + 1)$, что обеспечивает эффективное выполнение операций поиска, вставки и удаления за время $O(\log n)$. ([neerc.ifmo.ru](https://neerc.ifmo.ru/wiki/index.php?title=%D0%9A%D1%80%D0%B0%D1%81%D0%BD%D0%BE-%D1%87%D0%B5%D1%80%D0%BD%D0%BE%D0%B5_%D0%B4%D0%B5%D1%80%D0%B5%D0%B2%D0%BE&utm_source=chatgpt.com))