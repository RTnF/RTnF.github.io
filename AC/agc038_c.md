---
layout: default
title: AGC038-C LCMs
---

# **AtCoder 精進記録**
[TOP page](../)
## AGC038-C LCMs
### 点数
700

### 問題概要
数列 $A_i (i=0,\cdots,N-1)$ に対し、 $\sum_{i=0}^{N-2} \sum_{j=i+1}^{N-1} \mathrm{lcm}{(A_i, A_j)}$ を求めよ。

### 制約
- $2 \le N \le 200{,}000$
- $1 \le A_i \le 1{,}000{,}000$
- 入力はすべて整数

### メモ
解説AC。  
入力は何が何個あるかの情報 $cnt(x)$ に変換できる。  
lcmに似た、積和は $O(N)$ で求められる。  
$\sum_{i=1}^{V} \sum_{i|j, j \le V} \sum_{i|k, k \le V} f(j, k)$ は、 $f$ が $O(1)$ のとき $O(V \log V)$。この式と問題文の式から出発してうまい式変形を探す(meet-in-the-middle)。  
$\sum_{i=1}^{V} \sum_{i|j, j \le V} \sum_{i|k, k \le V} w_i \cdot jk \cdot cnt(j)cnt(k)$ は、積和の各項 $jk$ に係数 $\sum_{d|\gcd(j, k)} w_d$ がかかる。  
$\sum_{d|i} w_d = 1/i$ である数列 $w_i$ を用意できれば、この式が答えになる。
