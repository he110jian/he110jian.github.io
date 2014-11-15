---
layout: post
---

<h2>{{ page.title }}</h2>
<p class='meta'>{{ page.date | date_to_string }} - NanJing</p>
----------

### Add Two Numbers ###

You are given two linked lists representing two non-negative numbers. The digits are stored in reverse order and each of their nodes contain a single digit. Add the two numbers and return it as a linked list.

Input: (2 -> 4 -> 3) + (5 -> 6 -> 4)
Output: 7 -> 0 -> 8

#####solution1#####
{% highlight cpp %}
/**
 * Definition for singly-linked list.
 * struct ListNode {
 *     int val;
 *     ListNode *next;
 *     ListNode(int x) : val(x), next(NULL) {}
 * };
 */
class Solution {
public:
    ListNode *addTwoNumbers(ListNode *l1, ListNode *l2) {
		ListNode *result = new ListNode(0);
		ListNode *cur = result;
		int t,add=0;
		while (l1 && l2)
		{
			ListNode *pnew = new ListNode(0);
			t = l1->val + l2->val + add;
			if (t >= 10)
			{
				pnew->val = t - 10;
				add = 1;
			}
			else
			{
				pnew->val = t;
				add = 0;
			}
			cur->next = pnew;
			cur = pnew;
			l1 = l1->next;
			l2 = l2->next;
		}
		while (l1)
		{
			ListNode *pnew = new ListNode(0);
			t = l1->val + add;
			if (t >= 10)
			{
				pnew->val = t - 10;
				add = 1;
			}
			else
			{
				pnew->val = t;
				add = 0;
			}
			cur->next = pnew;
			cur = pnew;
			l1 = l1->next;
		}
		while (l2)
		{
			ListNode *pnew = new ListNode(0);
			t = l2->val + add;
			if (t >= 10)
			{
				pnew->val = t - 10;
				add = 1;
			}
			else
			{
				pnew->val = t;
				add = 0;
			}
			cur->next = pnew;
			cur = pnew;
			l2 = l2->next;
		}
		if (add)
		{
			ListNode *pnew = new ListNode(0);
			pnew->val = add;
			cur->next = pnew;
			cur = pnew;
		}
		return result->next;
	}
};
{% endhighlight %}


----------
