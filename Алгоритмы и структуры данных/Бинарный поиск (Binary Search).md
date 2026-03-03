# Документация: Решение задач методом Бинарного поиска (Easy & Доступный Medium)

## Суть метода

Бинарный (двоичный) поиск — это алгоритм поиска элемента в **отсортированном** массиве (или множестве со свойством монотонности). Вместо линейного просмотра каждого элемента, алгоритм работает, сокращая пространство поиска вдвое на каждом шаге.

**Базовый принцип работы (итеративно или рекурсивно):**
1. Определяем границы поиска (левый `L` и правый `R` индексы).
2. Пока границы не сомкнулись (`L <= R`), находим середину `mid = L + (R - L) / 2`.
3. Сравниваем `nums[mid]` с целью (`target`).
   - Если `nums[mid] == target`: **нашли** (базовый случай).
   - Если `nums[mid] < target`: значит цель справа, смещаем левую границу `L = mid + 1`.
   - Если `nums[mid] > target`: значит цель слева, смещаем правую границу `R = mid - 1`.

**Обязательные условия применимости:**
1. **Монотонность:** Данные должны быть отсортированы (по возрастанию или убыванию) либо обладать свойством, которое можно представить как монотонную функцию.
2. **Произвольный доступ:** Мы должны иметь возможность быстро обратиться к любому элементу по индексу (массивы подходят идеально).

---

## Ключевые паттерны для распознавания

1. **"Поиск в отсортированном массиве"** → Нужно найти число или проверить наличие.
2. **"Поиск границы (First/Last Position)"** → Ищем не любое вхождение, а самое левое (первое) или самое правое (последнее).
3. **"Поиск в почти отсортированном массиве"** → Массив изначально отсортирован, но затем сдвинут (ротирован).
4. **"Поиск ответа (Binary Search on Answer)"** → Мы **подбираем ответ** (число), проверяя, выполняется ли некоторое условие.
5. **"Поиск пика (Peak)"** → Поиск элемента, который больше своих соседей.

---

### 🎯 "Классический поиск (Classic)" — точное значение

**Суть подхода:** У нас есть отсортированный массив и цель. Нужно либо вернуть индекс цели, либо сказать, что её нет. [citation:6]

| Название задачи | Уровень | Ссылка на LeetCode | Почему подходит |
|----------------|---------|--------------------|-----------------|
| **704. Binary Search** | 🟢 Easy | [ссылка](https://leetcode.com/problems/binary-search/) | Самая базовая реализация алгоритма [citation:7]. |
| **35. Search Insert Position** | 🟢 Easy | [ссылка](https://leetcode.com/problems/search-insert-position/) | Найти индекс цели или место для вставки [citation:7]. |
| **367. Valid Perfect Square** | 🟢 Easy | [ссылка](https://leetcode.com/problems/valid-perfect-square/) | Бинарный поиск по числам, чтобы найти `x*x == num` [citation:7]. |
| **374. Guess Number Higher or Lower** | 🟢 Easy | [ссылка](https://leetcode.com/problems/guess-number-higher-or-lower/) | Отгадываем число по подсказкам [citation:7]. |
| **441. Arranging Coins** | 🟢 Easy | [ссылка](https://leetcode.com/problems/arranging-coins/) | Найти максимальное `k` для лесенки из монет [citation:7]. |
| **69. Sqrt(x)** | 🟢 Easy | [ссылка](https://leetcode.com/problems/sqrtx/) | Целая часть квадратного корня [citation:7]. |
| **744. Find Smallest Letter Greater Than Target** | 🟢 Easy | [ссылка](https://leetcode.com/problems/find-smallest-letter-greater-than-target/) | Первый элемент больше цели [citation:7]. |

---

### 🎯 "Поиск границ (Boundary Search)" — первое и последнее вхождение

**Суть подхода:** В массиве могут быть дубликаты. Нужно найти левую границу (первое вхождение) или правую границу (последнее вхождение). [citation:6]

| Название задачи | Уровень | Ссылка на LeetCode | Почему подходит |
|----------------|---------|--------------------|-----------------|
| **34. Find First and Last Position of Element in Sorted Array** | 🟠 Medium | [ссылка](https://leetcode.com/problems/find-first-and-last-position-of-element-in-sorted-array/) | Эталонная задача. Два отдельных бинарных поиска для левой и правой границы [citation:2][citation:8]. |
| **278. First Bad Version** | 🟢 Easy | [ссылка](https://leetcode.com/problems/first-bad-version/) | Классический поиск первой "плохой" версии [citation:7]. |
| **1539. Kth Missing Positive Number** | 🟢 Easy | [ссылка](https://leetcode.com/problems/kth-missing-positive-number/) | Поиск k-го пропущенного числа [citation:7]. |
| **1608. Special Array With X Elements Greater Than or Equal X** | 🟢 Easy | [ссылка](https://leetcode.com/problems/special-array-with-x-elements-greater-than-or-equal-x/) | Бинпоиск по `x` с проверкой условия. |

---

### 🎯 "Поиск в ротированном массиве (Rotated Array)" — отсортирован, но со сдвигом

**Суть подхода:** Массив был отсортирован, но затем "сломан" в какой-то точке и части переставлены местами. Одна половина массива всё ещё отсортирована. [citation:6]

| Название задачи | Уровень | Ссылка на LeetCode | Почему подходит |
|----------------|---------|--------------------|-----------------|
| **153. Find Minimum in Rotated Sorted Array** | 🟠 Medium | [ссылка](https://leetcode.com/problems/find-minimum-in-rotated-sorted-array/) | Ищем точку разрыва (минимум) [citation:7]. |
| **33. Search in Rotated Sorted Array** | 🟠 Medium | [ссылка](https://leetcode.com/problems/search-in-rotated-sorted-array/) | Определяем отсортированную половину и проверяем цель [citation:7]. |

---

### 🎯 "Поиск пика (Peak Finding)" — локальный максимум

**Суть подхода:** Массив не полностью отсортирован, но нужно найти пик (элемент больше соседей). [citation:6]

| Название задачи | Уровень | Ссылка на LeetCode | Почему подходит |
|----------------|---------|--------------------|-----------------|
| **162. Find Peak Element** | 🟠 Medium | [ссылка](https://leetcode.com/problems/find-peak-element/) | Ищем любой пик. Логика: если `mid < mid+1`, пик справа [citation:4]. |
| **852. Peak Index in a Mountain Array** | 🟠 Medium | [ссылка](https://leetcode.com/problems/peak-index-in-a-mountain-array/) | Упрощенная версия: массив строго возрастает, потом убывает [citation:7][citation:10]. |

---

### 🎯 "Поиск ответа (Binary Search on Answer)" — подбор значения

**Суть подхода:** Мы **угадываем** ответ (потенциальное число) с помощью бинарного поиска, а затем проверяем вспомогательной функцией, возможно ли это. Ключевая подсказка: задача просит найти **минимальное/максимальное** значение, при котором выполняется условие. [citation:5][citation:6]

| Название задачи | Уровень | Ссылка на LeetCode | Почему подходит |
|----------------|---------|--------------------|-----------------|
| **875. Koko Eating Bananas** | 🟠 Medium | [ссылка](https://leetcode.com/problems/koko-eating-bananas/) | **Классика паттерна.** Минимальная скорость поедания [citation:5][citation:7]. |
| **1011. Capacity To Ship Packages Within D Days** | 🟠 Medium | [ссылка](https://leetcode.com/problems/capacity-to-ship-packages-within-d-days/) | Минимальная грузоподъемность корабля [citation:7]. |
| **1283. Find the Smallest Divisor Given a Threshold** | 🟠 Medium | [ссылка](https://leetcode.com/problems/find-the-smallest-divisor-given-a-threshold/) | Минимальный делитель [citation:7]. |
| **1482. Minimum Number of Days to Make m Bouquets** | 🟠 Medium | [ссылка](https://leetcode.com/problems/minimum-number-of-days-to-make-m-bouquets/) | Минимальное количество дней для букетов [citation:7]. |
| **1870. Minimum Speed to Arrive on Time** | 🟠 Medium | [ссылка](https://leetcode.com/problems/minimum-speed-to-arrive-on-time/) | Минимальная скорость поезда [citation:7]. |
| **1552. Magnetic Force Between Two Balls** | 🟠 Medium | [ссылка](https://leetcode.com/problems/magnetic-force-between-two-balls/) | **Максимизировать** минимальную силу [citation:7]. |
| **2064. Minimized Maximum of Products Distributed to Any Store** | 🟠 Medium | [ссылка](https://leetcode.com/problems/minimized-maximum-of-products-distributed-to-any-store/) | Минимизация максимума при распределении. |
| **2616. Minimize the Maximum Difference of Pairs** | 🟠 Medium | [ссылка](https://leetcode.com/problems/minimize-the-maximum-difference-of-pairs/) | Минимизация максимальной разницы в парах. |
| **1760. Minimum Limit of Balls in a Bag** | 🟠 Medium | [ссылка](https://leetcode.com/problems/minimum-limit-of-balls-in-a-bag/) | Минимизация максимального размера кучи. |
| **2187. Minimum Time to Complete Trips** | 🟠 Medium | [ссылка](https://leetcode.com/problems/minimum-time-to-complete-trips/) | Минимальное время для всех поездок. |

---

### 🎯 Бонус: Простые задачи на матрицы и нестандартное применение

| Название задачи | Уровень | Ссылка на LeetCode | Почему подходит |
|----------------|---------|--------------------|-----------------|
| **74. Search a 2D Matrix** | 🟠 Medium | [ссылка](https://leetcode.com/problems/search-a-2d-matrix/) | Матрицу можно представить как один большой массив [citation:7]. |
| **1351. Count Negative Numbers in a Sorted Matrix** | 🟢 Easy | [ссылка](https://leetcode.com/problems/count-negative-numbers-in-a-sorted-matrix/) | Поиск границы отрицательных чисел в каждой строке [citation:7]. |
| **287. Find the Duplicate Number** | 🟠 Medium | [ссылка](https://leetcode.com/problems/find-the-duplicate-number/) | Неочевидное применение: подсчет чисел <= mid [citation:7]. |
| **981. Time Based Key-Value Store** | 🟠 Medium | [ссылка](https://leetcode.com/problems/time-based-key-value-store/) | Бинарный поиск по временным меткам [citation:7]. |

---

### 💡 Рекомендуемый порядок прохождения

1. **Классика (Easy)** — 704, 35, 374 — поймите механизм сужения границ.
2. **Поиск границ (Easy → Medium)** — 278, 1539, 34 — научитесь искать первое/последнее вхождение.
3. **Поиск ответа на простых числах** — 69, 367, 441 — привыкните к идее подбора ответа.
4. **Ротированные массивы (Medium)** — 153, 33 — прокачайте понимание инвариантов.
5. **Поиск пика** — 162, 852 — поймите движение по градиенту.
6. **Главное — поиск ответа** — 875, 1011, 1283, 1552 — это самый важный блок.
