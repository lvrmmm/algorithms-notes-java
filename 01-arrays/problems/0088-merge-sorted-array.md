# 88. Merge Sorted Array

- Сложность: Easy
- Темы: массив, два указателя, сортировка
- Ссылка: https://leetcode.com/problems/merge-sorted-array/

## Условие

Даны два массива в неубывающем порядке. В `nums1` первые `m` значений являются данными, а последние `n` позиций зарезервированы. Нужно поместить объединённый результат в `nums1`.

## Решение

```java
class Solution {
    public void merge(int[] nums1, int m, int[] nums2, int n) {
        int write = m + n - 1;
        int first = m - 1;
        int second = n - 1;

        while (first >= 0 && second >= 0) {
            if (nums1[first] > nums2[second]) {
                nums1[write] = nums1[first];
                first--;
            } else {
                nums1[write] = nums2[second];
                second--;
            }
            write--;
        }

        while (second >= 0) {
            nums1[write] = nums2[second];
            second--;
            write--;
        }
    }
}
```

## Почему заполнение начинается с конца

При записи слева можно уничтожить ещё не прочитанные элементы `nums1`. Свободное пространство расположено справа, поэтому туда безопасно записывать наибольший из двух текущих элементов.

Если `nums2` закончился первым, оставшиеся элементы `nums1` уже стоят правильно. Если первым закончился `nums1`, остаток `nums2` нужно скопировать.

## Сложность

- Время: `O(m + n)`.
- Дополнительная память: `O(1)`.
