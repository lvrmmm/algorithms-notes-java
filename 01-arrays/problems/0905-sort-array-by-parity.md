# 905. Sort Array By Parity

- Сложность: Easy
- Темы: массив, два указателя
- Ссылка: https://leetcode.com/problems/sort-array-by-parity/

## Условие

Нужно поместить все чётные элементы массива перед нечётными. Порядок элементов внутри групп не задан.

## Решение

```java
class Solution {
    public int[] sortArrayByParity(int[] nums) {
        int left = 0;

        for (int right = 0; right < nums.length; right++) {
            if (nums[right] % 2 == 0) {
                int temp = nums[left];
                nums[left] = nums[right];
                nums[right] = temp;
                left++;
            }
        }

        return nums;
    }
}
```

Перед каждой итерацией `[0, left)` содержит чётные элементы, а `[left, right)` — нечётные. При обнаружении чётного элемента он обменивается с первым элементом нечётной части.

Порядок нечётных элементов может измениться. Для `[1, 3, 2]` результатом станет `[2, 3, 1]`. Условие задачи это разрешает.

## Сложность

- Время: `O(n)`.
- Дополнительная память: `O(1)`.
