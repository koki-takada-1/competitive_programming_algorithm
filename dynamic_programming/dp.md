# 動的計画法(Dynamic Programming)

最適化問題を部分構造最適性を満足する部分問題に分解可能であれば、部分問題の最適解を統合して元の問題の最適解を求められる方法。

部分構造最適性：＝「元の問題の最適解が、ある部分問題の最適解を含む」

## 例1.[Educational DP Contest A-Frog1](https://atcoder.jp/contests/dp/tasks/dp_a)

![問題文](/dynamic_programming/Atcoder_dp1.png) 
実行時間制限: 2 sec / メモリ制限: 1024 MB

回答例
```c++
#include <bits/stdc++.h>
using namespace std;
#define rep(i, n) for(int i=0;i<(n);i++)
 
int main(void){
    int N;
    cin >> N;
    int h[N],dp[N];
    rep(i,N) cin >> h[i];
 
    rep(i,N) {
        if(i==0){
            dp[i] = 0;
        } else if (i==1){
            dp[i] = abs(h[i]-h[i-1]); 
        } else {
            // min(1つ前からジャンプするコスト, 2つ前からジャンプするときのコスト)
            dp[i] = min(dp[i-2]+abs(h[i]-h[i-2]),dp[i-1]+abs(h[i]-h[i-1]));
        }
    }
    cout << dp[N-1] <<endl;
    return 0;
}

```
## 例2.ナップサック問題
重さと価値がそれぞれ $w_i,v_i~(1\le i\le N)$ であるような $N$ 個の品物があります。  
これらの品物から、重さの総和が $W$ を超えないように選んだときの価値の総和の最大値を求めなさい。

回答例
```c++
#include <bits/stdc++.h>
using namespace std;
 
int main(void){
    int N,W;
    cin >> N >> W;
    int w[N],v[N];
    long dp[N+1][W+1];// DPテーブル
    for(int i = 0; i<N; i++) cin >> w[i] >> v[i];
 
    //配列の初期化
    for(int i = 0; i<=W; i++) dp[0][i] = 0;
    
    for(int i = 0; i<N; i++) {
        for(int j = 0; j<=W; j++) {
            if (j < w[i]) {
                dp[i+1][j] = dp[i][j];
            } else {
                dp[i+1][j] = max(dp[i][j], dp[i][j-w[i]]+v[i]);
            }
        }
    }
    cout << dp[N][W] <<endl;
    return 0;
}
```



