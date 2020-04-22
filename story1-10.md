# Numpy100本ノックの感想文1〜10

## 目次

- [0のみの行列を作るzerosメソッド](#0のみの行列を作るzerosメソッド)
- [行列のサイズを知れるsizeとitemsize](#行列のサイズを知れるsizeとitemsize)
- [指定した範囲で連続する数字列を作成するarange](#指定した範囲で連続する数字列を作成するarange)
- [reshapeによる次元の変換](#reshapeによる次元の変換)
- [nonzero()による0のリスト内の消去](#nonzeroによる0のリスト内の消去)

## 感想

### 0のみの行列を作るzerosメソッド
- 以下は10個の0列をつくるやつ！

```python:jupyter.py
zeros_10 = zeros(10)
```

- 10×10の行列を作りたいときはこれ！

```python:jupyter.py
zeros_10_10 = zeros((10,10))
```

### 行列のサイズを知れるsizeとitemsize
- np行列のsizeとitemsizeを使ってかけることによりメモリを算出

```python:jupyter.py
zeros_10_10 = np.zeros((10, 10))
display(zeros_10_10)
print(zeros_10_10.size, zeros_10_10.itemsize)
print("%d bytes" % (zeros_10_10.size * zeros_10_10.itemsize))
```

### 指定した範囲で連続する数字列を作成するarange
- arangeで始めの数字(S)〜終わりの数字(E+1)のE個のarrayを作成する

```python:jupyter.py
Z_10_49 = np.arange(10, 49)
print(Z_10_49)
```

### reshapeによる次元の変換
- 0~8の１次元のリストを３次元のリストに変換する

```python:jupyter.py
Z_08 = np.arange(0,9)
display(Z_08)
Z_08_33 = Z_08.reshape(3,3)
display(Z_08_33)
```

### nonzero()による0のリスト内の消去
1. `[1,2,0,0,4,0]`のnumpy行列を用意する
2. nonzeroメソッドによって0を消去！

```python:jupyter.py
Z_zero = np.array([1,2,0,0,4,0])
display(Z_zero)
Z_non_zero = Z_zero.nonzero()
display(Z_non_zero)
```
