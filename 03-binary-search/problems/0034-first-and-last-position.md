# 34. Find First and Last Position of Element in Sorted Array

- Сложность: Medium
- Темы: массив, бинарный поиск
- Ссылка: https://leetcode.com/problems/find-first-and-last-position-of-element-in-sorted-array/

## Условие

В отсортированном массиве нужно найти первое и последнее вхождение `target`. Если значения нет, вернуть `[-1, -1]`. Требуемое время — `O(log n)`.

## Первая версия

Сначала можно найти любое совпадение бинарным поиском, а затем пройти влево и вправо по равным элементам. Ответ будет правильным, но при массиве из одинаковых значений дополнительные циклы займут `O(n)`.

## Решение двумя бинарными поисками

```java
class Solution {
    public int[] searchRange(int[] nums, int target) {
        int[] result = {-1, -1};

        int left = 0;
        int right = nums.length - 1;

        while (left <= right) {
            int mid = left + (right - left) / 2;

            if (nums[mid] == target) {
                result[0] = mid;
                right = mid - 1;
            } else if (nums[mid] < target) {
                left = mid + 1;
            } else {
                right = mid - 1;
            }
        }

        left = 0;
        right = nums.length - 1;

        while (left <= right) {
            int mid = left + (right - left) / 2;

            if (nums[mid] == target) {
                result[1] = mid;
                left = mid + 1;
            } else if (nums[mid] < target) {
                left = mid + 1;
            } else {
                right = mid - 1;
            }
        }

        return result;
    }
}
```

## Обнаруженные ошибки

Перед вторым поиском необходимо восстановить границы. После первого цикла `left > right`, поэтому повторный цикл со старыми значениями не запустится.

Ветки должны быть связаны через `if / else if / else`. При отдельных `if` после равенства может выполниться ещё один `else` и сдвинуть противоположную границу.

## Сложность

- Время: `O(log n)`.
- Дополнительная память: `O(1)` без учёта возвращаемого массива.
