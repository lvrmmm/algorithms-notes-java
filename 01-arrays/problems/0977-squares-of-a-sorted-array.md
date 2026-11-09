# 977. Squares of a Sorted Array

- Сложность: Easy
- Темы: массив, два указателя
- Ссылка: https://leetcode.com/problems/squares-of-a-sorted-array/

## Условие

Дан массив в неубывающем порядке. Нужно вернуть квадраты его элементов также в неубывающем порядке.

После возведения в квадрат отрицательные значения могут нарушить порядок. Например:

```text
[-4, -1, 0, 3, 10]
-> [16, 1, 0, 9, 100]
```

## Решение

Элемент с наибольшим модулем всегда находится на одном из концов отсортированного массива. Больший квадрат записывается в конец результата.

```java
class Solution {
    public int[] sortedSquares(int[] nums) {
        int left = 0;
        int right = nums.length - 1;
        int write = nums.length - 1;
        int[] result = new int[nums.length];

        while (write >= 0) {
            int leftSquare = nums[left] * nums[left];
            int rightSquare = nums[right] * nums[right];

            if (leftSquare > rightSquare) {
                result[write] = leftSquare;
                left++;
            } else {
                result[write] = rightSquare;
                right--;
            }
            write--;
        }

        return result;
    }
}
```

Когда `left == right`, остаются один элемент и одна свободная позиция. При равных квадратах можно выбрать любую сторону.

## Сложность

- Время: `O(n)`.
- Память результата: `O(n)`.
- Вспомогательная память помимо результата: `O(1)`.
