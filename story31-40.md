# Numpy100本ノックの感想文21〜30

## 目次

- [np.setterrでNumpyの警告を無視する](#npsetterrでNumpyの警告を無視する)
- [虚数を出せるnp.emath.sqrtと出せないnp.sqrt](#虚数を出せるnpemathsqrtと出せないnpsqrt)
- [Numpyだって今日の日付出せますnp.datetime64メソッド](#Numpyだって今日の日付出せますnpdatetime64メソッド)
- [期間決めたら日付全て出力もできるnp.datetime64メソッド](#期間決めたら日付全て出力もできるnp.datetime64メソッド)
- [演算と出力をきめられるnp.(add,divide,negative,multiply)](#演算と出力をきめられるnpadddividenegativemultiply)
- [5つもあるんだぞ整数への変換方法](#5つもあるんだぞ整数への変換方法)
- [np.arangeってこんな使い方できるの！？！？編](#nparangeってこんな使い方できるの編)
- [yieldだとイテレータ。←を含む関数はジェネレータを整数表示する](#yieldだとイテレータを含む関数はジェネレータを整数表示する)
- [np.linspaceで要素数を使った等差数列をつくる！](#nplinspaceで要素数を使った等差数列をつくる)
- [sortでソートする](#sortでソートする)


## 感想

### np.setterrでNumpyの警告を無視する
[参考ScipyURL](https://docs.scipy.org/doc/numpy/reference/generated/numpy.seterr.html)

```python:jupyter.py
defaults = np.seterr(all="ignore")
```

### 虚数を出せるnp.emath.sqrtと出せないnp.sqrt

```python:jupyter.py
np.sqrt(-1) == np.emath.sqrt(-1)
print(np.sqrt(-1), np.emath.sqrt(-1))
```

### Numpyだって今日の日付出せますnp.datetime64メソッド
- `np.timedelta64`で日付の引き算とかしてるw

```python:jupyter.py
yesterday = np.datetime64('today', 'D') - np.timedelta64(1, 'D')
today     = np.datetime64('today', 'D')
tomorrow  = np.datetime64('today', 'D') + np.timedelta64(1, 'D')
print(yesterday, today, tomorrow)
# ↓出力結果
# 2020-04-22 2020-04-23 2020-04-24
```

### 期間決めたら日付全て出力もできるnp.datetime64メソッド

```python:jupyter.py
Z = np.arange('2016-07', '2016-08', dtype='datetime64[D]')
print(Z)
```

### 演算と出力をきめられるnp.(add,divide,negative,multiply)

```python:jupyter.py
A = np.ones(3)*1
B = np.ones(3)*2
print(np.add(A,B,out=B))
print(np.divide(A,2,out=A))
print(np.negative(A,out=A))
print(np.multiply(A,B,out=A))
```

### 5つもあるんだぞ整数への変換方法

```python:jupyter.py
Z = np.random.uniform(0,10,10)
print(Z)
print(Z - Z%1)
print(np.floor(Z))
print(np.ceil(Z)-1)
print(Z.astype(int))
print(np.trunc(Z))
```

### np.arangeってこんな使い方できるの！？！？編

```python:jupyter.py
Z = np.zeros((5,5))
Z += np.arange(5)
print(Z)
```

### yieldだとイテレータ。←を含む関数はジェネレータを整数表示する
- `yield`(イテレータ)でfor文すると早くなるらしい…
- `yield`を関数に定義するとジェネレータになる

```python:jupyter.py
def generate():
    for x in range(10):
        yield x
Z = np.fromiter(generate(),dtype=int,count=-1)
print(Z)
```

### np.linspaceで要素数を使った等差数列をつくる！
- 第一引数で開始位置
- 第二引数で終了位置
- 第三引数で要素数
- `endpoint=False`で最終の位置をいれないでの要素数になる
- `retstep=True`だと公差を出力する

```python:jupyter.py
Z = np.linspace(0,1,11,endpoint=False)[1:]
print(Z)
# ↓実行結果
# [0.09090909 0.18181818 0.27272727 0.36363636 0.45454545 0.54545455
#  0.63636364 0.72727273 0.81818182 0.90909091]
```

### sortでソートする

```python:jupyter.py
Z = np.random.random(10)
Z.sort()
```
