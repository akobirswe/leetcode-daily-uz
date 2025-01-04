# [Unique Length-3 Palindromic Subsequences](https://leetcode.com/problems/unique-length-3-palindromic-subsequences/)

## Masala sharti

Berilgan bir satr `s` bo'lsa, `s` satrining uchta uzunlikdagi takrorlanmas palindromlarining sonini qaytaring.

E'tibor bering, bir xil subsequence'ni olishning bir necha yo'li bo'lsa ham, u faqat bir marta hisoblanadi.

`Palindrom` — bu o'qish bo'yicha oldindan va orqaga bir xil bo'lgan satr.

`Subsequence` — bu asl satrdan ba'zi belgilar (hech bo'lmaganda bitta) o'chirilgan holda yangi satr yaratish bo'lib, qolgan belgilarning nisbati saqlanadi.

Misol uchun, `"ace"` satri `"abcde"` satrining subsequence'idir.

### Kodning ishlash tartibi:

`Right` massivining hisoblanishi:

`Right` massivining maqsadi: Har bir harfning qatorning o‘ng tomonida necha marta uchraganligini saqlash.
Kodda `ord(letter)` - `ord('a')` yordamida harfni indeksga o‘zgartirishadi. Masalan, `'a'` uchun bu 0, `'b'` uchun 1 va hokazo.
`Right` massivini boshlang‘ich qiymatga keltirish uchun, `for letter in s:` orqali satrdagi har bir harfni tekshirib, har bir harfning qatorning o‘ng tomonida nechta borligini hisoblaymiz.
`Left` massivining hisoblanishi:

`Left` massivining maqsadi: Har bir harfning qatorning chap tomonida necha marta uchraganligini saqlash.
Kodda `Left` massivini boshida barcha elementlarni 0 deb boshlaymiz. Har bir harfni tekshirishda, `Left` massiviga o‘zgartirish kiritamiz.
Palindromlarni topish va saqlash:

`Palindrom`: Uchta harfdan iborat palindrom bo‘lishi uchun, ularning birinchi va oxirgi harflari teng bo‘lishi kerak. Shuning uchun t va j indekslari yordamida ularni taqqoslaymiz:
`Left[j] > 0:` Bu shart chapdan (ya'ni, `s[0]`, `s[1]`, ... qismida) j harfi mavjudligini bildiradi.
`Right[j] > 0:` Bu shart o‘ngdan (ya'ni, `s[len(s)-1]`, `s[len(s)-2]`, ... qismida) j harfi mavjudligini bildiradi.
Agar har ikkala shart bajarilsa, unda palindromni topdik va `palindroms.add(26 * t + j)` yordamida palindroms to‘plamiga qo‘shamiz. Bu yerda `26 * t + j` palindromni unikallash uchun ishlatiladi. Bu usulda palindromni yagona identifikator sifatida saqlaymiz.
`Left` massivini yangilash:

Har bir belgi uchun, `Left[t] += 1` orqali chapdan o‘tgan harfni hisoblaymiz.
Natija qaytarish:

Kod oxirida `len(palindroms)` chaqiriladi, bu esa palindromlarning sonini qaytaradi.

### Kod qismi

```Python
class Solution:
    def countPalindromicSubsequence(self, s: str) -> int:
        Right = [0] * 26
        for letter in s:
            Right[ord(letter) - ord('a')] += 1

        Left = [0] * 26
        palindroms = set()

        for i in range(len(s)):
            t = ord(s[i]) - ord('a')
            Right[t] -= 1
            for j in range(26):
                if Left[j] > 0 and Right[j] > 0:
                    palindroms.add(26 * t + j)
            Left[t] += 1
        return len(palindroms)
```

### Masalaning ishlashini tushuntirish:

# Kiritish: `"bbcbaba"`

`Right` massivini boshlang‘ich qiymatlar bilan to‘ldiramiz:
`b: 4`, `c: 1`, `a: 2`
`Left` massivining boshlang‘ich qiymati:
`b: 0`, `c: 0`, `a: 0` (Chap tomondan hech narsa ko‘rilmagan).
1-chi qadam (`i = 0`, `s[0] = b`):

`Right[b] = 3` bo‘ladi.
`Left[b]` oshadi va `1`bo‘ladi.
Palindromlar hozircha mavjud emas, chunki j uchun mos keluvchi o‘ngdagi harflar yo‘q.
Keyingi qadamlar:

Har bir qadamda `Left` va `Right` massivlarida harf soni yangilanadi va palindromlar aniqlanadi.
Natija:

Kod yakunida palindroms to‘plamida 3 ta unik palindromik subsequence bo‘ladi va ular soni qaytariladi.

### Murakkablik: Big O

### Vaqt murakkabligi:

``𝑂(𝑛×26)=𝑂(𝑛)` `O(n×26)=O(n)`, chunki biz har bir harfni bir marta tekshiramiz va harf  
bo‘yicha 26 marta tekshiruvlar amalga oshirilib, palindromlarni aniqlaymiz.

### Xotira murakkabligi:

𝑂(26), chunki `Left` va `Right` massivlari faqat 26 ta elementni saqlaydi (harflar soni). `palindroms` setining o‘lchami esa palindromlar soniga bog‘liq.

### Ikkinchi ishlash yo'li (ammo barcha testcase-lardan muvaffaqqiyatli o'ta olmadi)

```Python
class Solution:
    def countPalindromicSubsequence(self, s: str) -> int:
        palindromes = set()
        n = len(s)

        for j in range(1, n - 1):
            left_chars = set()
            #Chap tomonni tekshiramiz
            for i in range(j - 1, -1, -1):
                left_chars.add(s[i])

            #Chap tomonni tekshiramiz
            for k in range(j + 1, n):
                if s[k] in left_chars:
                    palindromes.add(s[k] + s[j] + s[k])

        return len(palindromes)

```
