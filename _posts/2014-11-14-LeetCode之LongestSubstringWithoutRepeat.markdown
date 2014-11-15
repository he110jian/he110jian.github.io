---
layout: post
---

<h2>{{ page.title }}</h2>
<p class='meta'>{{ page.date | date_to_string }} - NanJing</p>
----------

### Longest Substring Without Repeating Characters ###
Given a string, find the length of the longest substring without repeating characters. For example, the longest substring without repeating letters for "abcabcbb" is "abc", which the length is 3. For "bbbbb" the longest substring is "b", with the length of 1.

#####solution1#####
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

----------
