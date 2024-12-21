## Условие
Задача. Даны два отсортированных массива $a_1$ ≤ . . . ≤ $a_N$ и
$b_1$ ≤ . . . ≤ $b_M$. Надо слить их в один отсортированный за $O(N + M)$ времени и доппамяти.

## Классический вариант 
1. Заведем указатели на первые элементы массивов $i$ и $j$ .
2. По индексу $i$ + $j$ выпишем меньший из $a_i$ и $b_j$ и сдвинем cоответствующий указатель на один вперед.
3. Так делаем, пока `$i$ < $n$ && $j$  < $m$`.
4. Оставшийся хвост одного из массивов дописываем в конец.

## Случай $N >> M$
тогда нет смысла в классическом алгоритме, так как выгоднее сделать $M$ бинпоисков за $O(\log{N})$ времени каждый.

## Нижняя оценка $Merge$
Нижние оценки доказываются в модели решающих деревьев. В каждом узле вопрос: $(A[i] < B[j])$?. 
- Если да, то элемент $A[i]$ должен получить в итоговом массиве меньший индекс, чем элемент $B[j]$.
- Если нет, то наоборот 

Сколько листьев у такого дерева? Их $C_{N+M}^M$, тогда глубина этого дерева $\log_2{C_{N+M} ^ M}$

### Формула Стирлинга (б/д)
$N! ∼ \sqrt{2\pi N}(\frac{N}{e})^N$

### Нижняя оценка Merge: $\Omega\left(M \log_2 \left(1 + \frac{N}{M}\right)\right)$
Рассмотрим высоту решающего дерева и найдем на нее ограничение снизу. Это и будет нижней оценкой Merge

$ \log_2 C_{M+N}^N \sim \log_2 \frac{\sqrt{2\pi (M+N)} \left(\frac{M+N}{e}\right)^{M+N}}{\sqrt{2\pi N} \left(\frac{N}{e}\right)^N \cdot \sqrt{2\pi M} \left(\frac{M}{e}\right)^M} = \frac{1}{2} \log_2 \frac{M+N}{2\pi MN} + \log_2 \frac{(M+N)^{M+N}}{M^M N^N} = \frac{1}{2} \log_2 \frac{M+N}{2\pi MN} + \log_2 \left(\frac{M+N}{M}\right)^M + \log_2 \left(\frac{M+N}{N}\right)^N = \frac{1}{2} \log_2 \frac{M+N}{2\pi MN} + \log_2 \left(1 + \frac{N}{M}\right)^M + \log_2 \left(1 + \frac{M}{N}\right)^N = \frac{1}{2} \log_2 \frac{M+N}{2\pi MN} + M \log_2 \left(1 + \frac{N}{M}\right) + N \log_2 \left(1 + \frac{M}{N}\right)\\$

$
\log_2 C_{M+N}^N \sim \frac{1}{2} \log_2 \frac{M+N}{2\pi MN} + M \log_2 \left(1 + \frac{N}{M}\right) + N \log_2 \left(1 + \frac{M}{N}\right)
$


Будем считать, что $N > 2M$.
#### Докажем, что $M \log_2 \left(1 + \frac{N}{M}\right) > N \log_2 \left(1 + \frac{M}{N}\right)$

$ M \log_2 \left(\frac{M+N}{M}\right) - N \log_2 \left(\frac{M+N}{N}\right) >  M \log_2 \left(\frac{M+N}{M}\right) - 2M \log_2 \left(\frac{M+N}{N}\right) = M \left( \log_2 \left( \frac{(M+N)N^2}{M(M+N)^2}\right) \right) = M \log_2 \left( \frac{N^2}{M(M+N)}\right) > \log_2 \left( \frac{N^2}{M(M+N)}\right) \\$

- $N > 2M \implies M < \frac{N}{2}$

$(M+N)M < \left( \frac{N}{2} + N  \right) \frac{N}{2} = \frac{3}{4} N^2 < N^2 \implies  \frac{N^2}{M(M+N)} > 1 \implies \log_2 \left( \frac{N^2}{M(M+N)}\right) > 0 \implies M \log_2 \left(\frac{M+N}{M}\right) - N \log_2 \left(\frac{M+N}{N}\right) > 0 \implies M \log_2 \left(\frac{M+N}{M}\right) > N \log_2 \left(\frac{M+N}{N}\right)$

Получили, что $M \log_2 \left(1 + \frac{N}{M}\right) > N \log_2 \left(1 + \frac{M}{N}\right)$ $\implies N \log_2 \left(1 + \frac{M}{N}\right) = O \left( M \log_2 \left(1 + \frac{N}{M}\right)\right)$

Вернемся к высоте решающего дерева. При $N > 2M$ первое слагаемое стремится к нулю с ростом N, M.

$
\log_2 C_{M+N}^N \sim \frac{1}{2} \log_2 \frac{M+N}{2\pi MN} + M \log_2 \left(1 + \frac{N}{M}\right) + N \log_2 \left(1 + \frac{M}{N}\right) = O \left( M \log_2 \left(1 + \frac{N}{M}\right)\right) + M \log_2 \left(1 + \frac{N}{M}\right) = \Omega\left(M \log_2 \left(1 + \frac{N}{M}\right)\right)
$