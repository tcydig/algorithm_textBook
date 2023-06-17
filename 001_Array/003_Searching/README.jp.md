# Array SEarcihng

## 配列 検索方法 一覧

| 方法 | 
| --- | 
| 線型探索 |
※適宜追加予定

## 線型探索

取得したい要素のIndexが分からない場合、配列の要素を最初から順に検索する<br>
この検索のアルゴリズムを**線形探索**という<br>
最初から順に検索をかけるため、時間計算量はO(N)となる。

~~~python
    # 線形探索用の関数
    def linearSearch(array,length,element):

        # エッジケースの対処
        if (array is None or length == 0):
            return False
        for index in range(length):
            if array[index] == element:
                return True
        
        return False

    # Index数を固定で指定し、配列を作成
    list = [0] * 5
    # lengthにて最後尾のIndexを管理する
    length = 0

    # 値をすべてのIndexに入れる
    for i in range(5):
        list[i] = length
        length += 1

    print('検索対象の配列:',list)

    # 検索対象がある場合
    targetInt1 = 3
    if linearSearch(list,length,targetInt1):
        print('ターゲット１の数値が入っています')
    else:
        print('ターゲット１の数値が入っていません')

    # 検索対象がない場合
    targetInt2 = 100
    if linearSearch(list,length - 1,targetInt2):
        print('ターゲット２の数値が入っています')
    else:
        print('ターゲット２の数値が入っていません')
    
~~~
上記の実行結果が以下
~~~python
    検索対象の配列: [0, 1, 2, 3, 4]
    ターゲット１の数値が入っています
    ターゲット２の数値が入っていません
~~~

## 参照ドキュメント
https://leetcode.com/explore/featured/card/fun-with-arrays/527/searching-for-items-in-an-array/3296/