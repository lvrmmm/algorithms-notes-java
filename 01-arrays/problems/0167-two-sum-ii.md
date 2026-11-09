# 167. Two Sum II — Input Array Is Sorted

- Сложность: Medium
- Темы: отсортированный массив, два указателя
- Ссылка: https://leetcode.com/problems/two-sum-ii-input-array-is-sorted/

## Условие

В отсортированном массиве нужно найти два разных элемента, сумма которых равна `target`. Ответ содержит позиции с нумерацией от единицы. По условию решение существует.

## Решение

```java
class Solution {
    public int[] twoSum(int[] numbers, int target) {
        int left = 0;
        int right = numbers.length - 1;

        while (left < right) {
            int sum = numbers[left] + numbers[right];

            if (sum == target) {
                return new int[]{left + 1, right + 1};
            } else if (sum > target) {
                right--;
            } else {
                left++;
            }
        }

        return new int[]{-1, -1};
    }
}
```

## Почему можно двигать указатели

Если сумма слишком мала, даже самый большой доступный элемент не образует нужную пару с `numbers[left]`. Левый индекс можно исключить.

Если сумма слишком велика, даже самый маленький доступный элемент не образует нужную пару с `numbers[right]`. Правый индекс можно исключить.

Условие `left < right` гарантирует использование двух разных элементов.

## Сложность

- Время: `O(n)`.
- Дополнительная память: `O(1)`.
