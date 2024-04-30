## 1st

#### setによる実装

- 最初に考えたのはポインタをsetに入れていく方法、フロイドの循環検出は答え見て知った
- NULLは型がintになって微妙らしいのでnullptrに変えた
- setの実装が気になってclangのソース見に行ったらtemplateまみれで何書いてあるのか全くわからず断念…
  - 実装は二分木らしい、アルゴリズムイントロダクションに書いてあるので今度読む
- 要素数0の配列のケースで一敗。 こういうケースが来ることを予期してなかった、これからは注意する

##### Complexity
ノードの数Nに対して、
- Time O(NlogN)  
- Space O(N)
  
```C++
class Solution {
public:
    bool hasCycle(ListNode *head) {
      set<ListNode *> passed_node;
      ListNode *checking_node = head;

      if (checking_node == nullptr) {
        return false;
      }
      while (checking_node != nullptr) {
        if (passed_node.count(checking_node)) {
          return true;
        }
        passed_node.insert(checking_node);
        checking_node = checking_node->next;
      }
      
      return false;
    }
};
```

#### フロイドの循環検出による実装

- 1段階目ではwhileより前に一度ポインタを動かす実装だったが、その分if文が増えたのでwhile文中で動かすようにした
- while文中のfastは1つ先さえnullptrじゃなければ、->nextでエラーならないのでOK。1段階目では2個先までチェックしてしまった。

```C++
class Solution {
public:
    bool hasCycle(ListNode *head) {
      ListNode *fast = head;
      ListNode *slow = head;

      while (fast != nullptr) {
        if (fast->next == nullptr) {
          return false;
        }
        fast = fast->next->next;
        slow = slow->next;

        if (fast == slow) {
          return true;
        }
      }

      return false;
    }
};
```
