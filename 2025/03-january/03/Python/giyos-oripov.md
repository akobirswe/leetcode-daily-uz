# [Number of Ways to Split Array](https://leetcode.com/problems/number-of-ways-to-split-array/description/)

## Masala sharti
Sizga butun sonlardan tashkil topgan `nums` nomli massiv beriladi.
Massivni `i`-chi indeksda bo‘lish `to‘g‘ri bo‘lishi` uchun quyidagi shartlar bajarilishi kerak:
Birinchi `(i+1)` ta element yig‘indisi, oxirgi `(n-i-1)` ta element yig‘indisidan katta yoki teng bo‘lishi kerak.
Indeksning o‘ng tomonida kamida bitta element bo‘lishi kerak, ya’ni: `0 <= i < n-1`.

### Input
- `nums = [10,4,-8,7]`

### Output
- `ans = 2`

### Kod

```python
class Solution:
    def waysToSplitArray(self, nums: List[int]) -> int:
        left = 0  
        right = sum(nums)  
        r = 0 
        for i in nums[:-1]:
            right -= i  
            left += i  
            if left >= right: 
                r += 1  
        return r
```

### Tushuntirish

1. **Yig‘indilarni hisoblash:**  
   - `left` — chap yig‘indi, `right` — umumiy yig‘indi (boshlang‘ich holatda o‘ng qism yig‘indisi).
   - `r` — javobni saqlovchi o‘zgaruvchi.

2. **Massivni aylanish:**
    - Massivni oxirgi elementdan oldingisigacha aylanamiz.
    - Har bir elementni `right`-dan olib tashlaymiz va `left`-ga qo‘shamiz.
    - Agar chap yig‘indi o‘ngdan katta yoki teng bo‘lsa, `r`-ni oshiramiz.

3. **Javob:**
    - Agar chap yig‘indi o‘ngdan katta yoki teng bo‘lsa, `r`-ni oshiramiz.
    - Natijani qaytarish.

### Murakkablik tahlili
- **Vaqt murakkabligi:** Birinchi `sum(nums)` chaqiruvi `O(n)` vaqt talab qiladi, va undan keyin `for sikli` ham `O(n)` vaqt talab qiladi. Shu sababli umumiy vaqt murakkabligi O(n).
- **Xotira murakkabligi:** O(1).
