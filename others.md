# その他
## N個^M属性の全探索
### 問題概要
　N個の区別できる要素がある。それぞれにM個ある属性のうち1つをつけるとき、考えられる状態を全探索せよ。
### 時間計算量
　O(N^M)
### 説明
　M=2の場合、bit全探索と呼ばれる。
　状態をM進法のN桁の数字と考える。
### コード
例題：Synthetic Kadomatsu
```C++
int main(){
    ll n;
    cin >> n;
    vll goal(3);
    rep(i, 3){
        cin >> goal[i];
    }
    vll l(n);
    rep(i, n){
        cin >> l[i];
    }
    // 0, 1, 2それぞれ使用する 3は使用しない
    vll state(n);
    auto calc_MP = [&](){
        ll ret = 0;
        vll len(4, 0);
        vll cnt(4, 0);
        rep(j, n){
            len[state[j]] += l[j];
        }
        rep(i, 3){
            cnt[i] = count(ALL(state), i);
            if(cnt[i] == 0) return INF;
            ret += 10 * (cnt[i] - 1);
            ret += abs(len[i] - goal[i]);
        }
        return ret;
    };
    ll state_num = powint(4, n);
    ll ans = INF;
    rep(i, state_num){
        rep(k, n){
            state[k] = (i / powint(4, k)) % 4;
        }
        chmin(ans, calc_MP());
    }
    cout << ans << endl;
    return 0;
}
```
