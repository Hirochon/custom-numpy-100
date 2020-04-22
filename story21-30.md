# Numpy100本ノックの感想文21〜30

## 目次

- [np.tileでnp多次元配列を連続させよう！](#nptileでnp多次元配列を連続させよう)
- [np.(mean,std)で正規化しよう！](#npmeanstdで正規化しよう)
- [行列の掛け算(外積)はnp.dotを使う！](#行列の掛け算外積はnpdotを使う)
- [np配列の中のある部分だけに演算を行う](#np配列の中のある部分だけに演算を行う)
- [float型のrandomそれはnp.random.uniform](#float型のrandomそれはnprandomuniform)
- [四捨五入の方法一覧(round, trunc, floor, ceil, fix)](#四捨五入の方法一覧roundtruncfloorceilfix)
- [となりのnp配列符号を決定する関数np.copysign](#となりのnp配列符号を決定する関数npcopysign)
- [配列間で共通の値を見つけるnp.interesect1d](#配列間で共通の値を見つけるnp.interesect1d)


## 感想

### np.tileでnp多次元配列を連続させよう！
- `np.tile`で配列をaxis=0,1どちらにも増幅させられる！
- 第1引数で配列指定,第2引数で増幅数
1. 2次元で`axis=0`方向(縦)に増幅させる

```python:jupyter.py
Z_tile = np.tile(np.array([[0,1],[1,0]]), (4,1))
print(Z_tile)
```

2. 2次元で`axis=1`方向(横)に増幅させる

```python:jupyter.py
Z = np.tile(np.array([[0,1],[1,0]]), (1,4))
print(Z)
```

3. 2次元で２次元的に増幅させる

```python:jupyter.py
Z = np.tile(np.array([[0,1],[1,0]]), (4,4))
print(Z)
```

### np.(mean,std)で正規化しよう！
```python:jupyter.py
Z_55 = np.random.random((5, 5))
Z_55 = (Z_55 - np.mean (Z_55)) / (np.std (Z_55))
print(Z_55)
```

### 行列の掛け算(外積)はnp.dotを使う！
```python:jupyter.py
Z = np.dot(np.ones((5,3)), np.ones((3,2)))
```

### np配列の中のある部分だけに演算を行う
- 多分普通のリストでもできるかな？

```python:jupyter.py
Z = np.arange(11)
Z[(3 < Z) & (Z < 8)] *= -1
print(Z)
# ↓ 実行結果
# [ 0  1  2  3 -4 -5 -6 -7  8  9 10]
```

### float型のrandomそれはnp.random.uniform
- あるのは薄々気付いてたけど、使うの初めて説

```python:jupyter.py
Z_uni = np.random.uniform(-10,+10,10)
print(Z_uni)
# ↓ 実行結果
# [ 6.71513405  1.82678094  7.71655629 -1.13988178  4.83471589  0.04326439 -4.19139452  6.68664864 -0.97458844 -3.4317147 ]
```

### 四捨五入の方法一覧(round, trunc, floor, ceil, fix)
1. 四捨五入: `np.round()`
2. 切り捨て(小数点以下を消す): `np.trunc()`
3. 切り捨て(小さい方の整数に丸める): `np.floor()`

```python:jupyter.py
print (np.floor(Z_uni))
# ↓ 実行結果
# [ 6.  1.  7. -2.  4.  0. -5.  6. -1. -4.]
```

4. 切り上げ: `np.ceil()`

```python:jupyter.py
print (np.ceil(np.abs(Z_uni)))
# ↓ 実行結果
# [ 7.  2.  8. -1.  5.  1. -4.  7. -0. -3.]
```

5. ゼロに近い方に丸める: `np.fix()`

```python:jupyter.py
print (np.fix(Z_uni))
# ↓ 実行結果
# [ 6.  1.  7. -1.  4.  0. -4.  6. -0. -3.]
```

### となりのnp配列符号を決定する関数np.copysign
- 下の例は元通りにしてるだけだけど、`copysign`の第2引数によっては符号が変化する

```python:jupyter.py
print (np.copysign(np.ceil(np.abs(Z_uni)), Z_uni))
```

### 配列間で共通の値を見つけるnp.interesect1d
```python:jupyter.py
Z1 = np.random.randint(0,10,10)
Z2 = np.random.randint(0,10,10)
print(Z1, Z2)
print(np.intersect1d(Z1,Z2))
# ↓ 実行結果
# [2 0 2 5 4 9 8 8 6 1] [1 6 9 8 7 6 6 7 3 1]
# [1 6 8 9]
```
