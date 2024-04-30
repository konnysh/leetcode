## 1st

#### setによる実装
- 最初はsetの実装だけ思いついた、フロイドの循環検出を使うのは思いつかなかった
- setの実装ならサイクル検出だけの問題とほとんど変わらない

##### Complexity
ノードの数Nに対して、
- Time O(NlogN)  
- Space O(N)
  
```C++
class Solution {
public:
    ListNode *detectCycle(ListNode *head) {
      set<ListNode *> passed_node;
      ListNode *checking_node = head;

      while (checking_node != nullptr) {
        if (passed_node.count(checking_node)) {
          return checking_node;
        }

        passed_node.insert(checking_node);
        checking_node = checking_node->next;
      }

      return nullptr;
    }
};
```

#### フロイドの循環検出による実装
- 片方ポインタを先頭に戻して等速で進めるとちょうどスタート地点に戻る
  - フロイドで合流するK番目のノードは、サイクルの先頭のS番目のノードを0としてサイクルの長さLを法にmodとってサイクル上に順に割り振る番号ではK-S
  - Kは、２つのポインタの移動距離の差に等しく、これはサイクルの長さlの整数倍
  - slowを先頭に戻してSステップ進めば、slowは当然サイクルの先頭、fastのサイクル上の番号はK-S+S≡K≡0 (mod L)でこちらもサイクルの先頭

##### Complexity
ノードの数Nに対して、
- Time O(N)  
- Space O(1)  

```C++
class Solution {
public:
    ListNode *detectCycle(ListNode *head) {
      ListNode *fast = head;
      ListNode *slow = head;

      while (fast != nullptr) {
        if (fast->next == nullptr) {
          return nullptr;
        }

        fast = fast->next->next;
        slow = slow->next;

        if (fast == slow) {
          slow = head;

          while (fast != slow) {
            fast = fast->next;
            slow = slow->next;
          }

          return fast;
        }
      }

      return nullptr;
    }
};
```
