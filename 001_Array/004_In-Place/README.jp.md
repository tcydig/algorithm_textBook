# Array In-Place

## In-Placeアルゴリズムとは？
in-placeアルゴリズムとは、データ構造の変換をする際に、追加の記憶領域をほとんど使わずに行うアルゴリズムを意味する。<br>
in-place でないアルゴリズムは not-in-place あるいは out-of-place などと呼ばれることもある。<br>

in-placeとout-of-placeの処理の違いを以下の問題を使用して確認。<br>
本問題はleetcodeにて提供されているものとなります。<br>
https://leetcode.com/explore/featured/card/fun-with-arrays/511/in-place-operations/3257/

## サンプル問題
与えられた整数の配列を基に、奇数のIndexの値を2乗して配列を返却する
~~~text
Input: array = [9, -2, -9, 11, 56, -12, -3]
Output: [81, -2, 81, 11, 3136, -12, 9]
Explanation: The numbers at even indexes (0, 2, 4, 6) have been squared, 
whereas the numbers at odd indexes (1, 3, 5) have been left the same.
~~~

## out-of-placeの場合
愚直に本問題を解決する場合には以下のような手法が考えられると思います。<br>
~~~text
与えられたリストとは別に新しいリストを作成
そのうえで、与えられたリストをFor文で一つ一つ要素を取得し、偶数の場合は2乗して新しいリストに格納し、奇数以外の場合はそのままリストに格納するようにする
~~~
上記の方針で、実装すると以下の通り
~~~python
    # out-of-placeの関数
    def squareEven(array,length):

        # エッジケースの対処
        if (array is None):
            return None

        # 新規のListを作成する
        newList = [0] * length
        
        for index in range(length):
            element = array[index]

            # 偶数Indexの場合は2乗する
            if (index % 2) == 0:
                element *= element
            
            newList[index] = element
        
        return newList

    # Input list
    list =  [9, -2, -9, 11, 56, -12, -3]

    print('変換後の配列:',squareEven(list,len(list)))
~~~
上記の実行結果が以下
~~~python
    変換後の配列: [81, -2, 81, 11, 3136, -12, 9]
~~~
与えられた配列と同一サイズの配列を新規に作成するため、<br>
上記の処理ではO(N)の空間計算量を必要とする

## In-Placeの場合
In-placeの場合は以下のような手法が考えられる
~~~text
Indexが偶数の場合に与えられたリストの要素を2乗して、与えられたリストにそもまま上書きをする
~~~
上記の方針で、実装すると以下の通り
~~~python
    # In-Placeの関数
    def squareEven(array,length):

        # エッジケースの対処
        if (array is None):
            return None
        
        for index in range(length):
            # 偶数Indexの場合は2乗する
            if (index % 2) == 0:
                array[index] *= array[index]
        
        return array

    # Input list
    list =  [9, -2, -9, 11, 56, -12, -3]

    print('変換後の配列:',squareEven(list,len(list)))
~~~
上記の実行結果が以下
~~~python
    変換後の配列: [81, -2, 81, 11, 3136, -12, 9]
~~~
この場合は新しい配列を作成していないため、追加の空間を必要としない

## 時間計算量も考慮に入れたIn-place
上記の例では空間計算量を考慮に入れて実装を入れたが実際は空間計算量と時間計算量の両方を考慮しないといけない<br>
次の以下の例題を基に考える。（こちらの問題もleetcodeにて提供されています）<br>
https://leetcode.com/explore/featured/card/fun-with-arrays/511/in-place-operations/3255/

## サンプル問題
与えられたソート済みの配列を基に、重複している数値を削除し一つだけ存在している形で配列を返却する
~~~text
例題１
Input: array = [1, 1, 2]
Output: [1, 2]
例題２
Input: array = [0, 0, 1, 1, 1, 2, 2, 3, 3, 4]
Output: [0, 1, 2, 3, 4]
~~~

## In-Place（空間計算量のみ考慮）の場合
空間計算量のみを考慮して今回の問題を解くと以下のようになる
~~~text
与えられた配列をFor文で回し、次の要素が重複している場合は削除する。
削除する際は、それ以降の要素をすべて左に一つずらす事で対応
~~~
上記の方針で、実装すると以下の通り
~~~python
    # In-Placeの関数
    def removeDuplicates(array,length):

        trimLength = length
        # エッジケースの対処
        if (array is None):
            return 0
        
        for index in range(length - 2,-1,-1):
            if array[index] == array[index + 1] :
                for j in range(index + 1,length,1):
                    array[j - 1] = array[j]
                trimLength -= 1
        return trimLength

    # Input list
    list =  [1, 1, 2]
    removeDuplicates(list,len(list))
    print('変換後の配列:',list[0:removeDuplicates(list,len(list))])
~~~
上記の実行結果が以下
~~~python
    変換後の配列: [1, 2]
~~~
この場合は新しい配列を作成していないため、追加の空間を必要としないO(1)となる<br>
しかし、時間計算量の場合はO(n2)となる

## In-Place（時間計算量も考慮）の場合
時間計算量も考慮して今回の問題を解くと以下のようになる
~~~text
与えられた配列をFor文で回し、次の要素が重複している場合は削除する。
削除する際は、それ以降の要素をすべて左に一つずらす事で対応
~~~
上記の方針で、実装すると以下の通り
~~~python
    # In-Placeの関数
    def copyWithRemovedDuplicates(array,length):

        trimLength = length
        # エッジケースの対処
        if (array is None):
            return None

        uniqueNumbers = 0

        for index in range(length):
            if index == 0 or array[index] != array[index - 1]:
                uniqueNumbers += 1
        
        results = [0] * uniqueNumbers

        positionInResult = 0
        for index in range(length):
            if index == 0 or array[index] != array[index - 1]:
                results[positionInResult] = array[index]
                positionInResult += 1
        return results

    # Input list
    list =  [0, 0, 1, 1, 1, 2, 2, 3, 3, 4]

    print('変換後の配列:',copyWithRemovedDuplicates(list,len(list)))
~~~
上記の実行結果が以下
~~~python
    変換後の配列: [0, 1, 2, 3, 4]
~~~
この場合は空間計算量はO(1)となり、時間計算量はO(N)となる<br>
※配列を新たに作成しているが、'='での代入は参照渡しになるので新規に空間を余分にとらない<br>

## 参照ドキュメント
https://ja.wikipedia.org/wiki/In-place%E3%82%A2%E3%83%AB%E3%82%B4%E3%83%AA%E3%82%BA%E3%83%A0<br>
https://leetcode.com/explore/featured/card/fun-with-arrays/511/in-place-operations/3257/
