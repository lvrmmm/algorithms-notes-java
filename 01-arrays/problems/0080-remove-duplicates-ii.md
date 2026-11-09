# 80. Remove Duplicates from Sorted Array II

- Сложность: Medium
- Темы: отсортированный массив, два указателя
- Ссылка: https://leetcode.com/problems/remove-duplicates-from-sorted-array-ii/

## Условие

Нужно изменить отсортированный массив на месте так, чтобы каждое значение встречалось не более двух раз. Метод возвращает логическую длину результата.

## Решение

Первые два элемента можно сохранить. Для каждого следующего значения проверяется элемент, записанный двумя позициями ранее.

```java
class Solution {
    public int removeDuplicates(int[] nums) {
        if (nums.length <= 2) {
            return nums.length;
        }

        int write = 2;

        for (int read = 2; read < nums.length; read++) {
            if (nums[read] != nums[write - 2]) {
                nums[write] = nums[read];
                write++;
            }
        }

        return write;
    }
}
```

Если текущее значение равно `nums[write - 2]`, в сохранённой части уже находятся два таких значения. Добавление ещё одного создало бы третье вхождение.

## Обобщение до `k` повторов

```java
public int removeDuplicates(int[] nums, int k) {
    if (nums.length <= k) {
        return nums.length;
    }

    int write = k;

    for (int read = k; read < nums.length; read++) {
        if (nums[read] != nums[write - k]) {
            nums[write] = nums[read];
            write++;
        }
    }

    return write;
}
```

Параметр `k` предполагается положительным.

## Сложность

- Время: `O(n)`.
- Дополнительная память: `O(1)`.
