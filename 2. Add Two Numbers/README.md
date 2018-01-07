# 思路

同时遍历两个链表，将l2加到l1上，遇10进1.

特例：

1、l1.length > l2.length    carry == 1 or carry == 0 

2、l1.length < l2.length    carry == 1 or carry == 0

3、l1.length == l2.length   carry == 1 or carry == 0
    
    (note: 6种情况需要考虑齐全。)
    
# 错误版

（包含编写过程中存在的错误。）

错误：时间超时

    /**
     * Definition for singly-linked list.
     * struct ListNode {
     *     int val;
     *     struct ListNode *next;
     * };
     */
    struct ListNode* addTwoNumbers(struct ListNode* l1, struct ListNode* l2) {
        int carry = 0;

        struct ListNode* l1_node = l1;
        struct ListNode* l2_node = l2;
        struct ListNode* l1_end;

        while (l1_node != NULL && l2_node != NULL) {
            l1_node->val += l2_node->val + carry;
            carry = 0;

            if (l1_node->val >= 10) { //没有保护等于。
                l1_node->val -= 10;
                carry = 1;
            }

            l1_end = l1_node;
            l1_node = l1_node->next;
            l2_node = l2_node->next;
        }

        if (l2_node != NULL) {
            l2_node->val += carry;
            l1_end->next = l2_node;
        }
        else if (l1_node != NULL)   //缺少考虑l1_node为NULL的情况。l1长度小于l2.
        {
            while(l1_node != NULL && carry == 1)
            {
                l1_node->val += carry;
                if (l1_node->val >= 10)
                {
                    l1_node->val -= 10;
                    carry = 1;
                }
            }
        }

        if (carry == 1)  //缺少考虑最后存在进位的情况。
        {
            l1_end->next = (struct ListNode *)malloc(sizeof(struct ListNode));
            l1_node = l1_end->next;
            l1_node->next = NULL;
            l1_node->val = 1;
        }

        return l1;
    }
