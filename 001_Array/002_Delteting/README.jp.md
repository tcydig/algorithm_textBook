# Array Deletions

## 配列 削除方法 一覧

| 方法 | 
| --- | 
| 最後の要素を削除 |
| 最初に要素を削除 |
| 特定のIndexの要素を削除 |


## 最後の要素を削除

最後に挿入する場合は基本的に最後尾のIndex数を取得し、そこに値を削除する<br>

~~~python
    # Index数を固定で指定し、配列を作成
    list = [0] * 5
    # lengthにて最後尾のIndexを管理する
    length = 0

    # 値をすべてのIndexに入れる
    for i in range(5):
        list[i] = length
        length += 1

    print('最後尾のIndexは',length - 1)
    print('削除前の要素',list)

    # 最後尾を削除する
    for index in range(length - 1):
        print('index:',index,'要素:',list[index])
    
~~~
上記の実行結果が以下
~~~python
    最後尾のIndexは 4
    削除前の要素 [0, 1, 2, 3, 4]
    index: 0 要素: 0
    index: 1 要素: 1
    index: 2 要素: 2
    index: 3 要素: 3
~~~

## 最初の要素を削除

最初の要素を削除する場合は、削除したことでスペースが空くため他の要素を左に一つづ移動させる<br>
そして、この移動させる処理は全ての要素を左に一つづつ移動するため時間が多く必要、かつその時間は固定ではなく配列の長さに依存している。<br>
時間計算量で表すとO(N)となる。※N -> 配列の長さ
~~~python
    # Index数を固定で指定し、配列を作成
    list = [0] * 5
    # lengthにて最後尾のIndexを管理する
    length = 0

    # 値をすべてのIndexに入れる
    for i in range(5):
        list[i] = length
        length += 1

    print('削除前の要素',list)

    # 要素を左に一つづつ移動
    for index in range(1,length,1):    
        list[index - 1] = list[index]
        
    length -= 1

    print('---↓ 削除後 ↓---')
    for index in range(length):
        print('index:',index,'要素:',list[index])
~~~
上記の実行結果が以下
~~~python
    削除前の要素 [0, 1, 2, 3, 4]
    ---↓ 削除後 ↓---
    index: 0 要素: 1
    index: 1 要素: 2
    index: 2 要素: 3
    index: 3 要素: 4
~~~

## 特定のIndexに挿入

特定のIndexに削除する場合も、削除する要素以降の要素を全て左に一つ移動させる必要がある<br>
そのため、この削除方法でもある程度の時間がかかる<br>
~~~python
    # Index数を固定で指定し、配列を作成
    list = [0] * 5
    # lengthにて最後尾のIndexを管理する
    length = 0

    # 値をすべてのIndexに入れる
    for i in range(5):
        list[i] = length
        length += 1

    print('削除前の要素',list)

    # 削除したいIndex
    indexToDelet = 2

    # Index:2以降の要素をすべて左に一つづつ移動
    for index in range(indexToDelet + 1,length,1):
        list[index - 1] = list[index]

    length -= 1

    print('---↓ 削除後 ↓---')
    for index in range(length):
        print('index:',index,'要素:',list[index])
~~~
上記の実行結果が以下
~~~python
    削除前の要素 [0, 1, 2, 3, 4]
    ---↓ 削除後 ↓---
    index: 0 要素: 0
    index: 1 要素: 1
    index: 2 要素: 3
    index: 3 要素: 4
~~~

## 参照ドキュメント
https://leetcode.com/explore/featured/card/fun-with-arrays/526/deleting-items-from-an-array/3246/