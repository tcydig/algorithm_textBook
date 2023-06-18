# Array two-pointer

## two-pointerとは？
two-pointerとは2つのIndexを管理する事で、配列の要素を同時に別の場所を参照する。<br>

two-pointerの処理を以下の問題を使用して確認。<br>
本問題はleetcodeにて提供されているものとなります。<br>
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

## 解答
ここでは以下の2つのpointerを使用する<br>
readPointer -> 全ての要素を読み込み、重複している値を特定する<br>
writePointer -> 重複している値を上書きする際に使用するIndexを管理。<br>

上記を使用した実装が以下の通り
~~~python
    def removeDuplicates(array,length):

        trimLength = length
        # エッジケースの対処
        if (array is None):
            return None

        writePointer = 1

        for readPointer in range(1,length,1):
            if array[readPointer] != array[readPointer - 1]:
                array[writePointer] = array[readPointer]
                writePointer += 1

        return writePointer

    # Input list
    list =  [0, 0, 1, 1, 1, 2, 2, 3, 3, 4]

    print('変換後の配列:',list[0:removeDuplicates(list,len(list))])
~~~

上記の実行結果が以下
~~~text
変換後の配列: [0, 1, 2, 3, 4]
~~~

## 補足
two-pointerにはいくつか方法がある。<br>
先頭から進むポインターと最後尾から進むポインターを使ったりと、方法は色々ある

## 参照ドキュメント
https://leetcode.com/explore/featured/card/fun-with-arrays/511/in-place-operations/3255/