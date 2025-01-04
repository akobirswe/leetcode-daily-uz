# [1930. Unique Length-3 Palindromic Subsequences](https://leetcode.com/problems/unique-length-3-palindromic-subsequences/description)

## Masala sharti

Berilgan bir satr `s` bo'lsa, `s` satrining uchta uzunlikdagi takrorlanmas palindromlarining sonini qaytaring.

E'tibor bering, bir xil subsequence'ni olishning bir necha yo'li bo'lsa ham, u faqat bir marta hisoblanadi.

`Palindrom` — bu o'qish bo'yicha oldindan va orqaga bir xil bo'lgan satr.

`Subsequence` — bu asl satrdan ba'zi belgilar (hech bo'lmaganda bitta) o'chirilgan holda yangi satr yaratish bo'lib, qolgan belgilarning nisbati saqlanadi.

Misol uchun, `"ace"` satri `"abcde"` satrining subsequence'idir.

---

### Kirish

* `s` satri: `3 <= s.length <= 10^5`

### Chiqish

* `s` satrning `3 uzunlikli` takrorlanmas palindromlari soni

---

## Kod

```go
func countPalindromicSubsequence(s string) int {
    firstIdx := make(map[byte]int, len(s))
    lastIdx := make(map[byte]int, len(s))

    for i:=0; i<len(s); i++{
        if _, ok := firstIdx[s[i]]; !ok {
            firstIdx[s[i]]=i
        }

        lastIdx[s[i]]=i
    }

    count := 0

    for char, start := range firstIdx {
        end := lastIdx[char]
        if start < end {
            uniqueChars := make(map[byte]bool, end-start)
            for i:=start+1; i<end; i++ {
                uniqueChars[s[i]]=true
            }

            count+=len(uniqueChars)
        }
    }

    return count
}
```

## Tushuntirish

1. **Indexlarni topish**
   * `firstIdx, lastIdx` o'zgaruvchilariga belgilarning birinchi va oxirgi indexlarini saqlab ketamiz

2. **Iteratsiya orqali belgilarni tekshirish**
   * `firstIdx`da saqlagan har bir belgini tekshirish uchun `start` va `end` indexlarini aniqlab olamiz.
   * `start` va `end` indexlar orasidagi noyob belgilarni sonini hisoblaymiz
   * Bu belgilarni soni `start` va `end` indexlari orasidagi palindromlari soni bo'ladi

3. **Natija qaytarish:**
   Palindromlar sonini qaytaramiz

```text
"aabca"

firstIdx = {a:0, b:2, c:3}
lastIdx = {a:4, b:2, c:3}

a belgisi
start = 0, end = 4

s[0] va s[4] orasida a, b, c - noyob belgilar. Bular va a belgi bilan palindrom yasasa bo'ladi
1. aaa
2. aba
3. aca
```

---

[Go Playground](https://go.dev/play/p/WuDZPBP5QzM)

## Murakkablik tahlili

**Vaqt murakkabligi:**

* Indexlash uchun: O(n).
* Unique belgilarni topish uchun: O(n).
* Umumiy: **O(n)**.

**Xotira murakkabligi:**

* Kirish uzunligi ortgani bilan biz faqat 26 belgini tekshirganimiz uchun: **O(1)**
