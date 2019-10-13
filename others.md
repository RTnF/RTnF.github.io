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
```
#include <bits/stdc++.h>
using namespace std;
using ll = long long;
using ld = long double;
using vi = vector<int>;
using vvi = vector<vi>;
using vvvi = vector<vvi>;
using vll = vector<ll>;
using vvll = vector<vll>;
using vvvll = vector<vvll>;
using vs = vector<string>;
using pll = pair<ll, ll>;
using vp = vector<pll>;
template<class T> using V = vector<T>;
template<class T> using VV = vector<vector<T> >;
#define rep(i, n) for(ll i = 0; i < (n); i++)
#define repb(i, n) for(ll i = (n)-1; i >= 0; i--)
#define repr(i, a, b) for(ll i = (a); i < (b); i++)
#define reprb(i, a, b) for(ll i = (a)-1; i >= (b); i--)
#define ALL(a) (a).begin(), (a).end()
#define SZ(x) ((ll)(x).size())
const ll MOD = 1000000007;
const ll INF = 100000000000000000LL;
inline ll GCD(ll a, ll b){ return b?GCD(b, a % b):a; }
inline ll LCM(ll a, ll b){ return a/GCD(a, b)*b; }
inline ll powint(unsigned long long x, ll y){ ll r=1; while(y){ if(y&1) r*=x; x*=x; y>>=1; } return r; }
inline ll powmod(ll x, ll y, ll m = MOD){ ll r=1; while(y){ if(y&1) r*=x; x*=x; r%=m; x%=m; y>>=1; } return r; }
template<class S, class T>inline bool chmax(S &a, const T &b){ if(a<b) { a=b; return 1; } return 0; }
template<class S, class T>inline bool chmin(S &a, const T &b){ if(b<a) { a=b; return 1; } return 0; }
#ifdef OJ_LOCAL
#include "dump.hpp"
#else
#define dump(...) ((void)0)
#endif

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
    // 3 -> not used
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
