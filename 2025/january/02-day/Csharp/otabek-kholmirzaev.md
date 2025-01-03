# [Count Vowel Strings in Ranges](https://leetcode.com/problems/count-vowel-strings-in-ranges/)

## Masala sharti
So'zlardan tashkil topgan `words` massivi(array) va `queries` deb nomlangan so‘rovlar ro‘yxati berilgan. Har bir `queries[i]` so‘rov uchun javob sifatida `words` massividan `queries[i]` = [$l_i, r_i$] oraliqda joylashgan, **bosh va oxirgi harfi unli bo‘lgan so‘zlar sonini** toping.

### Input 
- `words = ["aba","bcb","ece","aa","e"]`
- `queries = [[0,2],[1,4],[1,1]]`

### Output
- `ans = [2,3,0]`

## Kod

```csharp
public class Solution {
    public int[] VowelStrings(string[] words, int[][] queries) {
        var vowels = new HashSet<char> { 'a', 'e', 'i', 'o', 'u' };
        var n = words.Length;
        var prefixCount = new int[n + 1];
        for (int i = 0; i < n; i++) {
            prefixCount[i+1] = prefixCount[i] + IsValid(words[i], vowels); 
        } 

        var m = queries.Length;
        var ans = new int[m];
        for (int i = 0; i < m; i++) {
            var (l, r) = (queries[i][0], queries[i][1]);
            ans[i] = prefixCount[r+1] - prefixCount[l];
        } 

        return ans;
    }

    private int IsValid(string word, HashSet<char> vowels) {
        return vowels.Contains(word[0]) && vowels.Contains(word[^1]) ? 1 : 0;  
    }
}
```

### Tushuntirish

1. **Unli harflar ro‘yxatini tuzish:**  
   `HashSet<char>` yordamida tezkor tekshirish uchun unli harflar (`'a'`, `'e'`, `'i'`, `'o'`, `'u'`) saqlanadi.

2. **Prefiks hisoblagich:**  
   - `prefixCount[i]` — bu `words` qatorida 0-dan `i-1` gacha bo‘lgan unli bilan boshlanib va tugaydigan so‘zlar sonini saqlaydi.
   - Har bir so‘z uchun `IsValid` yordamchi funksiyasi orqali so‘z unli bilan boshlanib va tugashini tekshiradi.

3. **So‘rovlarni qayta ishlash:**  
   - Har bir `(l, r)` so‘rov uchun natija `prefixCount[r+1] - prefixCount[l]` orqali hisoblanadi. Bu `[l, r]` oralig‘ida nechta mos so‘z borligini hisoblaydi.

4. **Yordamchi funksiya:**  
   `IsValid` funksiyasi so‘zning birinchi va oxirgi belgisi unli ekanligini tekshiradi va mos bo‘lsa `1`, aks holda `0` qaytaradi.

## Murakkablik tahlili

- **Vaqt murakkabligi:**  
  - Prefiksni hisoblash: O(n), bu yerda `n` — so‘zlar soni.  
  - So‘rovlarni qayta ishlash: O(m), bu yerda `m` — so‘rovlar soni.  
  - Umumiy: O(n + m).

- **Xotira murakkabligi:**  
  - Prefiks hisoblagich uchun O(n).

## Xulosa
Ushbu yechim prefiks yig‘indisi(prefix sum) usulidan foydalangan holda unli so‘zlar sonini tez va samarali hisoblaydi.
