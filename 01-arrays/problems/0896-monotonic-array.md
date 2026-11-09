# 896. Monotonic Array

- Сложность: Easy
- Темы: массив
- Ссылка: https://leetcode.com/problems/monotonic-array/

## Условие

Нужно определить, является ли массив неубывающим или невозрастающим. Равные соседние значения разрешены.

## Решение

До начала проверки возможны оба направления. Строгое увеличение исключает невозрастающий порядок, а строгое уменьшение исключает неубывающий.

```java
class Solution {
    public boolean isMonotonic(int[] nums) {
        boolean monotoneIncreasing = true;
        boolean monotoneDecreasing = true;

        for (int i = 1; i < nums.length; i++) {
            if (nums[i - 1] < nums[i]) {
                monotoneDecreasing = false;
            } else if (nums[i - 1] > nums[i]) {
                monotoneIncreasing = false;
            }

            if (!monotoneIncreasing && !monotoneDecreasing) {
                return false;
            }
        }

        return true;
    }
}
```

## Важные наблюдения

По первым двум элементам нельзя всегда определить направление. В массивах `[4, 4, 2]` и `[4, 4, 5]` первые элементы равны, а направление задаётся позже.

Даже первая неравная пара определяет только возможное направление. Остальные пары всё равно нужно проверить. Например, `[4, 5, 3]` меняет направление.

## Сложность

- Время: `O(n)`.
- Дополнительная память: `O(1)`.
