## 1st
#### 同じ値のノードを飛ばしてつなぎなおす実装
- 見ているノードと次のノードを見て、値が同じだったら次の次と繋ぎなおす
- 飛ばされる中間のノードをdeleteすべきか迷ったが、普通にスコープ抜けて破棄されそうだと思ってしなかった。
- ifやwhileの条件や位置はいくらかパターンありそうだけど、この記述でひとまず十分シンプルそう

##### Complexity
ノードの数Nに対して、
- Time O(N)  
- Space O(1)
  
```C++
class Solution {
public:
    ListNode* deleteDuplicates(ListNode* head) {
      ListNode *checking_node = head;

      if (checking_node == nullptr) {
        return head;
      }
      while (checking_node->next != nullptr) {

        if (checking_node->val == checking_node->next->val) {
          checking_node->next = checking_node->next->next;
        } else {
          checking_node = checking_node->next;
        }
      }

      return head;
    }
};
```
