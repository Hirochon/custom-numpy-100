# Numpy100本ノックの感想文21〜30

## 目次

- [np.setterrでNumpyの警告を無視する](#npsetterrでNumpyの警告を無視する)
- [虚数を出せるnp.emath.sqrtと出せないnp.sqrt](#虚数を出せるnpemathsqrtと出せないnpsqrt)
- [Numpyだって今日の日付出せますnp.datetime64メソッド](#Numpyだって今日の日付出せますnpdatetime64メソッド)
- [期間決めたら日付全て出力もできるnp.datetime64メソッド](#期間決めたら日付全て出力もできるnp.datetime64メソッド)
- [演算と出力をきめられるnp.(add,divide,negative,multiply)](#演算と出力をきめられるnpadddividenegativemultiply)
- [5つもあるんだぞ整数への変換方法](#5つもあるんだぞ整数への変換方法)


## 感想

### np.setterrでNumpyの警告を無視する
[参考ScipyURL](https://docs.scipy.org/doc/numpy/reference/generated/numpy.seterr.html)

```python
defaults = np.seterr(all="ignore")
```

### 虚数を出せるnp.emath.sqrtと出せないnp.sqrt

```python
np.sqrt(-1) == np.emath.sqrt(-1)
print(np.sqrt(-1), np.emath.sqrt(-1))
```

### Numpyだって今日の日付出せますnp.datetime64メソッド
- `np.timedelta64`で日付の引き算とかしてるw

```python
yesterday = np.datetime64('today', 'D') - np.timedelta64(1, 'D')
today     = np.datetime64('today', 'D')
tomorrow  = np.datetime64('today', 'D') + np.timedelta64(1, 'D')
print(yesterday, today, tomorrow)
# ↓出力結果
# 2020-04-22 2020-04-23 2020-04-24
```

### 期間決めたら日付全て出力もできるnp.datetime64メソッド

```python
Z = np.arange('2016-07', '2016-08', dtype='datetime64[D]')
print(Z)
```

### 演算と出力をきめられるnp.(add,divide,negative,multiply)

```python
A = np.ones(3)*1
B = np.ones(3)*2
print(np.add(A,B,out=B))
print(np.divide(A,2,out=A))
print(np.negative(A,out=A))
print(np.multiply(A,B,out=A))
```

### 5つもあるんだぞ整数への変換方法

```python
Z = np.random.uniform(0,10,10)
print(Z)
print(Z - Z%1)
print(np.floor(Z))
print(np.ceil(Z)-1)
print(Z.astype(int))
print(np.trunc(Z))
```

### 
