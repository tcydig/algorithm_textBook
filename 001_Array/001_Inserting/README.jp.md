# Array Insersions

## 配列 挿入方法 一覧

| 方法 | 
| --- | 
| 最後に挿入 |
| 最初に挿入 |
| 特定のIndexに挿入 |


## 最後に挿入

最後に挿入する場合は基本的に最後尾のIndex数を取得し、そこに値を挿入する<br>

~~~python
    # Index数を固定で指定し、配列を作成
    list = [0] * 5
    # lengthにて最後尾のIndexを管理する
    length = 0

    # Index:2 まで値を入れる（= 最後尾のIndexを3とする）
    for i in range(3):
        list[i] = length
        length += 1

    for index, value in enumerate(list):
        print('index:',index,'value:',value)
    print('最後尾のIndexは',length)

    # 最後尾に挿入する
    list[length] = 10

    for index, value in enumerate(list):
        print('index:',index,'value:',value)
~~~
上記の実行結果が以下
~~~python
    index: 0 value: 0
    index: 1 value: 1
    index: 2 value: 2
    index: 3 value: 0
    index: 4 value: 0
    最後尾のIndexは 3
    index: 0 value: 0
    index: 1 value: 1
    index: 2 value: 2
    index: 3 value: 10
    index: 4 value: 0
~~~

## 最初に挿入

最初に挿入をする場合は、新しい要素を挿入するためのスペースを空ける必要があるため配列の要素を全て右に一つずつ移動させる必要がある<br>
そして、この移動させる処理は全ての要素を右に一つづつ移動するため時間が多く必要、かつその時間は固定ではなく配列の長さに依存している。<br>
時間計算量で表すとO(N)となる。※N -> 配列の長さ
~~~python
    # 最後尾に挿入した結果をそのまま利用

    # 要素を右に一つづつ移動（ただし、最後の要素はデフォルト値のため移動はしていない）
    for index in range(length,-1,-1):
        list[index + 1] = list[index]
    print('配列の要素を全て右に移動後:',list)

    # 最初に挿入
    list[0] = 100
    print('挿入後:',list)
~~~
上記の実行結果が以下
~~~python
    配列の要素を全て右に移動後: [0, 0, 1, 2, 10]
    挿入後: [100, 0, 1, 2, 10]
~~~

## 特定のIndexに挿入

特定のIndexに挿入する場合も、挿入する要素以降の要素を全て右に一つ移動させる必要がある<br>
そのため、この挿入方法でもある程度の時間がかかる<br>
~~~python
    # 挿入したいIndex
    indexToInsert = 2

    # Index:2以降の要素をすべて右に一つづつ移動（ただし、最後の要素はデフォルト値のため移動はしていない）
    for index in range(length, indexToInsert - 1, -1):
        list[index + 1] = list[index]
    print('index:2以降の要素をすべて右に移動後:',list)

    # 特定の要素に挿入
    list[indexToInsert] = 100
    print('挿入後:',list)
~~~
上記の実行結果が以下
~~~python
    index:2以降の要素をすべて右に移動後: [0, 1, 2, 2, 10]
    挿入後: [0, 1, 100, 2, 10]
~~~

## 補足
実際コーディングする際はapeend()で最後尾に挿入したり、.lengthでリストのサイズを取得したりする<br>
そういった便利な変数や関数を使用するため、挿入する事が目的で上記のようなFor文で実装する事はないと思われる<br>

## 参照ドキュメント
https://leetcode.com/explore/featured/card/fun-with-arrays/525/inserting-items-into-an-array/3244/