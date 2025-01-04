# [Count Vowel Strings in Ranges](https://leetcode.com/problems/count-vowel-strings-in-ranges/)

## Masala sharti

So'zlardan tashkil topgan `words` massivi(array) va `queries` deb nomlangan so‘rovlar ro‘yxati berilgan. Har bir `queries[i]` so‘rov uchun javob sifatida `words` massividan `queries[i]` = [$l_i, r_i$] oraliqda joylashgan, **bosh va oxirgi harfi unli bo‘lgan so‘zlar sonini** toping.

### Input

- `words = ["aba","bcb","ece","aa","e"]`
- `queries = [[0,2],[1,4],[1,1]]`

### Output

- `ans = [2,3,0]`

## Kod

```go
func vowelStrings(words []string, queries [][]int) []int {
    var (
        vowelCounts = make([]int, len(words)+1)
        ans = make([]int, len(queries))
        vowels = map[byte]bool{
        'a':true,
        'e':true,
        'i':true,
        'o':true,
        'u':true,
    }
    )

    for i, word := range words {
        if vowels[word[0]] && vowels[word[len(word)-1]] {
            vowelCounts[i+1]++
        }
        vowelCounts[i+1]+=vowelCounts[i]
    }

            
    for i, query := range queries {
        ans[i] = vowelCounts[query[1]+1]-vowelCounts[query[0]]
    }

    return ans
}
```

### Tushuntirish

1. **Unli harflar ro‘yxatini tuzish:**  
   `vowels` yordamida O(1) time complexity bilan har bir `word`ni bosh (`word[0]`) va oxirgi (`word[len(word)-1]`) harflarni tekshiramiz
2. **Prefiks hisoblagich:**  
   - `vowelCounts[i]` — bu `words` qatorida 0-dan `i-1` gacha bo‘lgan unli bilan boshlanib va tugaydigan so‘zlar sonini saqlaydi.
   - `words`ni `for` yordamida iterate qilib `vowels` yordamida tekshiramiz

3. **So‘rovlarni qayta ishlash:**  
   - Har bir `(l, r)` so‘rov uchun natija `vowelCounts[r+1] - vowelCounts[l]` orqali hisoblanadi. Bu `[l, r]` oralig‘ida nechta mos so‘z borligini hisoblaydi.

## Murakkablik tahlili

- **Vaqt murakkabligi:**  
  - Prefiksni hisoblash: O(n), bu yerda `n` — so‘zlar soni.  
  - So‘rovlarni qayta ishlash: O(m), bu yerda `m` — so‘rovlar soni.  
  - Umumiy: O(n + m).

- **Xotira murakkabligi:**  
  - Prefiks hisoblagich uchun O(n).

[GoPlayground](https://go.dev/play/p/9LrlF9jiGo-)

## Xulosa

Ushbu yechim prefiks yig‘indisi(prefix sum) usulidan foydalangan holda unli so‘zlar sonini tez va samarali hisoblaydi.
