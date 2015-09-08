---
layout: post
---

<h2>{{ page.title }}</h2>
<p class='meta'>{{ page.date | date_to_string }} - NanJing</p>
----------

### Longest Substring Without Repeating Characters ###
Given a string, find the length of the longest substring without repeating characters. For example, the longest substring without repeating letters for "abcabcbb" is "abc", which the length is 3. For "bbbbb" the longest substring is "b", with the length of 1.

{% highlight cpp %}
class Solution {
public:
    int lengthOfLongestSubstring(string s) {
        int locs[128];
        memset(locs, -1, sizeof(locs));
        int start = -1, max = 0;
        for (int i = 0; i < s.size(); ++i)
        {
            if (locs[s[i]] > idx)
            {
                start = locs[s[i]];
            }
            if (i - start > max)
            {
                max = i - start;
            }
            locs[s[i]] = i;
        }
        return max;
    }
};
{% endhighlight %}

### Add Two Numbers ###

You are given two linked lists representing two non-negative numbers. The digits are stored in reverse order and each of their nodes contain a single digit. Add the two numbers and return it as a linked list.

Input: (2 -> 4 -> 3) + (5 -> 6 -> 4)
Output: 7 -> 0 -> 8

{% highlight cpp %}
/**
 * Definition for singly-linked list.
 * struct ListNode {
 *     int val;
 *     ListNode *next;
 *     ListNode(int x) : val(x), next(NULL) {}
 * };
 */
class Solution {
public:
	ListNode *addTwoNumbers(ListNode *l1, ListNode *l2) {
	
		int t1, t2, carry = 0;
		ListNode* tail = new ListNode(0);
		ListNode* ptr = tail;
		while(l1 != NULL || l2 != NULL){
		t1 = 0;
		if(l1 != NULL)
		{
			t1 = l1->val;
			l1 = l1->next;
		}
		t2 = 0;
		if(l2 != NULL)
		{
			t2 = l2->val;
			l2 = l2->next;
		}
		int tmp = t1 + t2 + carry;
		ptr->next = new ListNode(tmp % 10);
		carry = tmp / 10;
		ptr = ptr->next;
		}
		if(carry == 1)
		{
			ptr->next = new ListNode(1);
		}
		return tail->next;
	}
};
{% endhighlight %}
----------
