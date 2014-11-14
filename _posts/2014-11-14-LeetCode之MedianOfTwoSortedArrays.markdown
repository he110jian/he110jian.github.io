---
layout: post
---

<h2>{{ page.title }}</h2>
<p class='meta'>{{ page.date | date_to_string }} - NanJing</p>
----------

### Median of Two Sorted Arrays ###
There are two sorted arrays A and B of size m and n respectively. Find the median of the two sorted arrays. The overall run time complexity should be O(log (m+n)).

#####solution1#####
{% highlight cpp %}
class Solution {
public:
    double findMedianSortedArrays(int A[], int m, int B[], int n)
    {
    	int h = m > n ? m : n;
    	int l = m < n ? m : n;
    	int flag = (m % 2) ^ (n % 2);
    	int w = (h - l) / 2 + l;
    	vector<int> comb;
    	int i = 0, j = 0;
    	int count = 0;
    	while (i < m && j < n)
    	{
    		comb.push_back((A[i]>B[j] ? B[j++] : A[i++]));
    		if (++count == w+1)
    			break;
    	}
    	while (i < m)
    	{
    		if (count == w+1)
    			break;
    		comb.push_back(A[i++]);
    		++ count;
    	}
    	while (j < n)
    	{
    		if (count == w+1)
    			break;
    		comb.push_back(B[j++]);
    		++count;
    	}
    	if (flag)
    		return comb[w];
    	else
    		return double(comb[w]) / 2 + double(comb[w - 1]) / 2;
    }
};
{% endhighlight %}

----------
