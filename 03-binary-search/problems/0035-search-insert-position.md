# 35. Search Insert Position

- Сложность: Easy
- Темы: массив, бинарный поиск
- Ссылка: https://leetcode.com/problems/search-insert-position/

## Условие

В отсортированном массиве уникальных чисел нужно найти индекс `target`. Если значения нет, вернуть индекс, на который его следовало бы вставить.

## Решение

```java
class Solution {
    public int searchInsert(int[] nums, int target) {
        int left = 0;
        int right = nums.length - 1;

        while (left <= right) {
            int mid = left + (right - left) / 2;

            if (nums[mid] == target) {
                return mid;
            } else if (nums[mid] > target) {
                right = mid - 1;
            } else {
                left = mid + 1;
            }
        }

        return left;
    }
}
```

После завершения поиска все элементы левее `left` меньше цели, а все элементы правее `right` больше цели. Пустой интервал удовлетворяет равенству `left == right + 1`, поэтому вернуть можно как `left`, так и `right + 1`.

Границы не обязаны сначала совпасть. Для `[1, 3]` и цели `0` правый индекс сразу станет `-1`, а левый останется равным нулю.

## Сложность

- Время: `O(log n)`.
- Дополнительная память: `O(1)`.
