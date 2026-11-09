# 1051. Height Checker

- Сложность: Easy
- Темы: массив, сортировка
- Ссылка: https://leetcode.com/problems/height-checker/

## Условие

Дан массив ростов учеников в текущем порядке. Нужно узнать, сколько позиций отличаются от порядка, полученного после сортировки по неубыванию.

Исходный массив сохраняется для сравнения, а его копия сортируется вручную.

## Решение 1. Пузырьковая сортировка

```java
class Solution {
    public int heightChecker(int[] heights) {
        int[] expected = Arrays.copyOf(heights, heights.length);
        int n = heights.length;

        for (int i = 0; i < n - 1; i++) {
            boolean swapped = false;

            for (int j = 0; j < n - i - 1; j++) {
                if (expected[j] > expected[j + 1]) {
                    int temp = expected[j];
                    expected[j] = expected[j + 1];
                    expected[j + 1] = temp;
                    swapped = true;
                }
            }

            if (!swapped) {
                break;
            }
        }

        return countMismatches(heights, expected);
    }

    private int countMismatches(int[] heights, int[] expected) {
        int mismatches = 0;

        for (int i = 0; i < heights.length; i++) {
            if (heights[i] != expected[i]) {
                mismatches++;
            }
        }

        return mismatches;
    }
}
```

- Лучший случай: `O(n)`.
- Худший случай: `O(n²)`.
- Дополнительная память: `O(n)` из-за копии.

## Решение 2. Сортировка выбором

```java
class Solution {
    public int heightChecker(int[] heights) {
        int[] expected = Arrays.copyOf(heights, heights.length);
        int n = heights.length;

        for (int i = 0; i < n - 1; i++) {
            int minIndex = i;

            for (int j = i + 1; j < n; j++) {
                if (expected[j] < expected[minIndex]) {
                    minIndex = j;
                }
            }

            int temp = expected[i];
            expected[i] = expected[minIndex];
            expected[minIndex] = temp;
        }

        int mismatches = 0;
        for (int i = 0; i < n; i++) {
            if (heights[i] != expected[i]) {
                mismatches++;
            }
        }

        return mismatches;
    }
}
```

- Лучший и худший случаи: `O(n²)`.
- Дополнительная память: `O(n)`.

Если минимум уже находится на позиции `i`, можно пропустить обмен с самим собой. Завершать всю сортировку нельзя. Например, в `[1, 3, 2]` первый элемент уже минимальный, но оставшаяся часть ещё не отсортирована.

## Решение 3. Сортировка вставками

```java
class Solution {
    public int heightChecker(int[] heights) {
        int[] expected = Arrays.copyOf(heights, heights.length);
        int n = heights.length;

        for (int i = 1; i < n; i++) {
            int key = expected[i];
            int j = i - 1;

            while (j >= 0 && expected[j] > key) {
                expected[j + 1] = expected[j];
                j--;
            }

            expected[j + 1] = key;
        }

        int mismatches = 0;
        for (int i = 0; i < n; i++) {
            if (heights[i] != expected[i]) {
                mismatches++;
            }
        }

        return mismatches;
    }
}
```

- Лучший случай: `O(n)`.
- Худший случай: `O(n²)`.
- Дополнительная память: `O(n)`.

Строгое сравнение `expected[j] > key` сохраняет порядок равных элементов и избегает лишних сдвигов. При `>=` результат останется отсортированным, но сортировка потеряет устойчивость.

## Общий вывод

Сами сортировки работают с `O(1)` дополнительной памятью. Всё решение использует `O(n)`, потому что для сравнения требуется копия исходного массива.
