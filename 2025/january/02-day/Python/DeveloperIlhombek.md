# Masala: Unli Harfli Satrlarni Hisoblash

# [Count Vowel Strings in Ranges](https://leetcode.com/problems/count-vowel-strings-in-ranges/)

1. `words`: Satrlardan iborat massiv. Har bir satr bosh va oxirgi harfini tekshirish lozim.
2. `queries`: So'rovlar ro'yxati. Har bir `[li, ri]` oraliqni ko'rsatadi.

**Vazifa**: Har bir so'rov uchun, `words` massivining `[li, ri]` oralig'ida bosh va oxirgi harfi unli bo'lgan satrlar sonini hisoblash.

Unli harflar: `a`, `e`, `i`, `o`, `u`.

---

### Kutilgan Kirish va Chiqish

### Input

- `words = ["aba","bcb","ece","aa","e"]`
- `queries = [[0,2],[1,4],[1,1]]`

### Output

- `ans = [2,3,0]`

## Kod

```python

class Solution:
    def vowelStrings(self, words: list[str], queries: list[list[int]]) -> list[int]:
        # Unli harflarni aniqlash uchun lug'at
        d = {"a": 1, "e": 1, "i": 1, "o": 1, "u": 1}

        # Prefix array orqali oldindan hisoblash
        preProcess = [0] * (len(words) + 1)
        count = 0
        for i in range(len(words)):
            if words[i][0] in d and words[i][-1] in d:
                count += 1
            preProcess[i + 1] = count

        # So'rovlarni ishlash
        ans = []
        for i in range(len(queries)):
            start = queries[i][0]
            end = queries[i][1]
            count = preProcess[end + 1] - preProcess[start]
            ans.append(count)
        return ans
```

### Tushuntirish

1. **Unli harflarni aniqlash**:  
   Unli harflarni aniqlash uchun quyidagi lug'at ishlatiladi:

   ```python
   d = {"a": 1, "e": 1, "i": 1, "o": 1, "u": 1}
   ```

2. **Prefix hisoblash**:

   - `preProcess` massivini yaratamiz, bunda har bir indeks unli bilan boshlanib, unli bilan tugaydigan satrlar sonini o'z ichiga oladi.
   - Misol uchun:
     ```python
     preProcess = [0, 1, 2, 2, 3, 4]
     ```

3. **So'rovlarni ishlash**:

   - Har bir `[li, ri]` so'rovi uchun, quyidagi formula orqali satrlar soni hisoblanadi:
     ```python
     count = preProcess[ri + 1] - preProcess[li]
     ```

4. **Natijani qaytarish**:
   - Har bir so'rov uchun natija `ans` massiviga qo'shiladi va oxirida natija qaytariladi.
