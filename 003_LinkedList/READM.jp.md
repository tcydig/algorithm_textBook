# LinekdList（連携リスト）

## LinekdListとは
LinekdListのそれぞれのノードでは値と**次のノードと紐づている参照フィールド**を保持している<br>
構造としては以下の通り
~~~python
class ListNode:
    def __init__(self, val):
        self.val = val
        self.next = None
~~~

## ADD
配列の場合はIndexにて各要素を管理しているため、追加する際に場合によっては多くの要素が移動する必要があった<br>
しかし、LinekdListの場合はIndexで各要素を管理しているわけでないため要素を挿入した際に要素の移動が必要ない<br>
つまりO(N)にてノードの追加が可能になる<br>
具体期にはノード同士の紐づけを行っている参照フィールドの値を入れ替えるのみで完結するためである

## DELET
配列の場合はIndexにて各要素を管理しているため、削除する際に場合によっては多くの要素が移動する必要があった<br>
しかし、LinekdListの場合はIndexで各要素を管理しているわけでないため要素を削除した際に要素の移動が必要ない<br>
しかし、参照フィールドの値を走査する必要があるためO（N）の時間計算量が必要<br>

## Doubly Linked Listとは

Doubly Linked ListとはLinkedListとは違い、一つのノードで前と後ろの参照フィールドを格納している<br>
構造としては以下の通り
~~~python
class ListNode:
    def __init__(self, val):
        self.val = val
        self.next = None
        self.prev = None
~~~

## ADD

LinkedListと同様に時間計算量はO(1)

## DELET

こちらの場合は、時間計算量/空間計算量共にO（1）となる<br>
なぜなら一つのノードに前と後ろの参照フィールドを持っているため、走査をする必要がない
