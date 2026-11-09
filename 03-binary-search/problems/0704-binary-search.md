# 704. Binary Search

- Сложность: Easy
- Темы: массив, бинарный поиск
- Ссылка: https://leetcode.com/problems/binary-search/

## Условие

В отсортированном по возрастанию массиве нужно найти `target`. Если значение присутствует, вернуть его индекс. Иначе вернуть `-1`.

## Решение

```java
class Solution {
    public int search(int[] nums, int target) {
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

        return -1;
    }
}
```

## Инвариант

Если искомый элемент существует, он находится в закрытом интервале `[left, right]`.

При `nums[mid] > target` середина и правая часть исключаются. При `nums[mid] < target` исключаются середина и левая часть.

## Почему используется `left <= right`

Когда `left == right`, остаётся один кандидат, который ещё нужно проверить. Например, при поиске `7` в `[0, 1, 2, 3, 4, 5, 6, 7]` границы в конце становятся равны семи. Условие `left < right` завершило бы цикл до проверки последнего элемента.

## Сложность

- Время: `O(log n)`.
- Дополнительная память: `O(1)`.
