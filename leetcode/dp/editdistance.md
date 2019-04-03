- 先上关键代码
```java
for(int i =0; i <= m; i++){
            cost[i][0] = i;
}
for(int i =0; i <= n; i++){
            cost[0][i] = i;
}
        // the staus when just reach the interval
for(int i = 0; i < m; i++){
    for(int j =0; j < n; j++){
            if(word1.charAt(i) == word2.charAt(j)) {
                    cost[i+1][j+1] = cost[i][j];
            }
            else {
                    // replace a ch
                    int min = cost[i][j];
                    //insert a ch
                    min = Math.min(cost[i+1][j], min);
                    
                    min = Math.min(cost[i][j+1], min);
                    cost[i+1][j+1] = min + 1;
                }
            }
        }
```
Let following be the function definition :-

f(i, j) := minimum cost (or steps) required to convert first i characters of word1 to first j characters of word2

Case 1: word1[i] == word2[j], i.e. the ith the jth character matches.

f(i, j) = f(i - 1, j - 1)

Case 2: word1[i] != word2[j], then we must either insert, delete or replace, whichever is cheaper

f(i, j) = 1 + min { f(i, j - 1), f(i - 1, j), f(i - 1, j - 1) }
- f(i, j - 1) represents insert operation
- f(i - 1, j) represents delete operation
- f(i - 1, j - 1) represents replace operation
- base case :f(0, k) = f(k, 0) = k
- 做dp的题一定要理解递推公式是怎么来的， 同时进行合理的初始化
