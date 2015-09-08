---
layout: post
---

<h2>{{ page.title }}</h2>
<p class='meta'>{{ page.date | date_to_string }} - NanJing</p>
----------

### Mini Stack ###
Design a stack that supports push, pop, top, and retrieving the minimum element in constant time.

{% highlight cpp %}
class MinStack {
private:
	struct minnode
	{
		int val;
		int count;
		minnode(int v) :val(v), count(1){}
	};
	stack<int> realstack;
	stack<minnode> ministack;
public:
	MinStack(){}
	void push(int x) {
		realstack.push(x);
		if (!ministack.empty())
		{
			if (x >= ministack.top().val)
				++ministack.top().count;
			else
			{
				ministack.push(minnode(x));
			}
		}
		else
			ministack.push(minnode(x));
	}

	void pop() {
		realstack.pop();
		if (ministack.top().count > 1)
			--ministack.top().count;
		else
			ministack.pop();
	}

	int top() {
		return realstack.empty() ? 0 : realstack.top();
	}

	int getMin() {
		return ministack.empty() ? 0 : ministack.top().val;
	}
};
{% endhighlight %}

### Wildcard Matching ###
Implement wildcard pattern matching with support for '?' and '*'. '?' Matches any single character. '*' Matches any sequence of characters (including the empty sequence).


{% highlight cpp %}
class Solution {
public:
    bool isMatch(const char *s, const char *p) {
    
        bool star = false;
        const char *str, *ptr;
        for (str = s, ptr = p; *str != '\0'; str++, ptr++)
        {
            switch (*ptr) 
            {
                case '?':
                    break;
                case '*':
                {
                    star = true;
                    s = str, p = ptr;
                    while (*p == '*')
                        p++;
                    if (*p == '\0') 
                        return true;
                    str = s - 1;
                    ptr = p - 1;
                    break;
                }
                default:
                {
                    if (*str != *ptr) 
                    {
                        if (!star) 
                            return false;
                        s++;
                        str = s - 1;
                        ptr = p - 1;
                    }
                }
            }
        }
        while (*ptr == '*')
            ptr++;
        return (*ptr == '\0');
    }
};
{% endhighlight %}

### Merge k Sorted Lists  ###

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
    ListNode *mergeTwoList(ListNode *l1, ListNode *l2) {
        if(l1 == NULL)
            return l2;
        if(l2 == NULL)
            return l1;
        ListNode *merge = new ListNode(0);
		ListNode *pcur = merge;
		while (l1&&l2)
		{
			if (l1->val > l2->val)
			{
				pcur->next = l2;
				l2 = l2->next;
			}
			else
			{
			    pcur->next = l1;
				l1 = l1->next;
			}
			pcur = pcur->next;
		}
		pcur->next = l1==NULL?l2:l1;
		return merge->next;
    }
    
    ListNode *mergeKLists(vector<ListNode *> &lists) {
        if(!lists.size())
            return NULL;
        
        for(int i = 1;i<lists.size();i*=2)
        {
            for(int j=0;j<lists.size()&&(i+j)<lists.size();)
            {
                lists[j] = mergeTwoList(lists[j],lists[i+j]);
                j=j+i*2;
            }
        }
        return lists[0];
    }
};
{% endhighlight %}

----------
