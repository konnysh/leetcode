## 1st

#### 番兵を使った実装
- 番兵の実装は最初思いつかず、答え見て知った
- 答え見てからコードをシンプルにしたが、改行含む条件式があってまだ見づらかった
- 色々見て考えた結果、変数名を変えることにした。
  - 一番使う変数が一番分かるから、形容詞付けずシンプルに
  - 計算に必要で新しく定義した変数の方にこそ字数を割く
     - コードがすっきり＆変数の字数にメリハリついて分かりやすくなった(？)
   
- whileやif-elseがちょっと重なると、いっぱい空行入れたくなる
  - スタイルガイド曰く、空行は最小限にして情報を画面に出来るだけ収めよ
  - コメント行の上の空行は必要と正当化しつつ結局空行いれた
  - コメント行がないところの空行の入れ方は考えないといけない。
    - 上空行か下空行か空行無しのどれかをブロック内で統一してやればよさそう

##### Complexity
ノードの数Nに対して、
- Time O(N)  
- Space O(1)
  
```C++
class Solution {
public:
    ListNode* deleteDuplicates(ListNode* head) {
      ListNode *node = head;
      ListNode dummy_head(-1, head);
      ListNode *previous_node = &dummy_head;

      while (node != nullptr) {
        if (node->next != nullptr && node->val == node->next->val) {

          //skips duplicated nodes
          previous_node->next = nullptr;
          int duplicated_value = node->val;
          while (node != nullptr && node->val == duplicated_value) {
            node = node->next;
          }
        } else {

          //connects the node to list
          previous_node->next = node;
          previous_node = node;
          node = node->next;
        }
      }

      return dummy_head.next;
    }
};
```
