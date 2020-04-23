# Numpy100本ノックの感想文21〜30

## 目次

- [np.setterrでNumpyの警告を無視する](#npsetterrでNumpyの警告を無視する)
- [虚数を出せるnp.emath.sqrtと出せないnp.sqrt](#虚数を出せるnpemathsqrtと出せないnpsqrt)

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

### 
