# [1930. Unique Length-3 Palindromic Subsequences](https://leetcode.com/problems/unique-length-3-palindromic-subsequences/)

## Masala sharti
`s` satr berilgan, undagi uzunligi 3 ga teng palindrom bo'lgan `subsequence`-lari (ketma-ketlik) sonini toping.  

Bir xil `subsequence`-larni faqat bir martadan hisoblang!  

Satrdagi belgilarning joylashgan o'rni o'zgartirilmagan holda, ba'zi belgilarni o'chirib tashlab (yoki umuman o'chirmasdan) hosil qilingan yangi satrga `subsequence` deyiladi.   

Misol uchun: `"ace"` - `abcde` ning `subsequence`-si hisoblanadi. 

### Kirish 
- `s = "aabca"`

### Chiqish
- `ans = 3`

### Izoh
- "aba" - "aabca" ning `subsequence`-si
- "aaa" - "aabca" ning `subsequence`-si
- "aca" - "aabca" ning `subsequence`-si

## Kod

```csharp
public class Solution {
    public int CountPalindromicSubsequence(string s) {
        int total = 0;
        for (char c = 'a'; c <= 'z'; c++) {
            int start = s.IndexOf(c);
            int end = s.LastIndexOf(c);
            HashSet<char> set = new();
            for (int i = start + 1; i < end; i++) {
                set.Add(s[i]);
                if (set.Count == 26) break;
            }

            total += set.Count;
        }

        return total;
    }
}
```

### Tushuntirish

1. **Uzunligi 3 ga teng palindrom satrlar:**  
    - Uzunligi 3 ga teng bo'lgan start palindrom bo'lishi uchun 1 chi va 3 chi belgisi bir xil bo'lishi kerak.  
    - O'rtadagi 2 chi belgi har qanday belgi bo'lishi mumkin.  
    - Misol uchun: `aba`, `aza`, `cfc`, ...  

2. **Palindrom satrlarni yasash yo'li:**  
    - `a` dan `z` gacha bo'lgan har bir harfni berilgan satrdagi eng birinchi va eng oxirgi indekslarini topib olamiz.  
    - Har bir uchun shu topilgan birinchi va oxirgi indekslar orasidagi noyob (unique) bo'lgan harflar sonini `total`
      ga yig'ib boramiz.   
    - Noyob harflar sonini topish uchun esa, `Hashset` ma'lumotlar tuzilmasidan foydalanamiz. 
    - Noyob harflar soni eng ko'pi bilan 26 ta (a dan z gacha) bo'lgani uchun, iteratsiyani muddatidan   
      oldin to'xtatsak ham bo'ladi: `if (set.Count == 26) break;`

## Murakkablik tahlili

- **Vaqt murakkabligi:**  
  - O(n)

- **Xotira murakkabligi:**  
  - O(1)