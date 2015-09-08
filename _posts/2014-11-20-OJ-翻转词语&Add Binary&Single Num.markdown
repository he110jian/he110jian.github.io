---
layout: post
---

<h2>{{ page.title }}</h2>
<p class='meta'>{{ page.date | date_to_string }} - NanJing</p>
----------

### Reverse Words in a String ###
Given an input string, reverse the string word by word.
For example,
Given s = "the sky is blue",
return "blue is sky the".

{% highlight cpp %}
void reverseWords(string &s) {
	
	string res="";
	for (int i = s.length()-1; i >= 0;)
	{
		while (i >= 0 && s[i] == ' ')
		{
			--i;
		}
		int j = i;
		while (i>=0 && s[i] != ' ')
		{
			--i;
		}
		if (i < j)
		{
			string strTmp;
			strTmp.assign(s, i+1, j - i);
			res += strTmp;
			res += " ";
		}
	}
	s = res.assign(res,0,res.length()-1);
}
{% endhighlight %}

### Add Binary ###
Given two binary strings, return their sum (also a binary string).
For example,
a = "11"
b = "1"
Return "100"

{% highlight cpp %}
class Solution {
public:
    string addBinary(string a, string b) {
    	if (!a.length())
    		return b;
    	if (!b.length())
    		return a;
    	vector<bool> res;
    	res.clear();
    	int carry = 0;
    	int i, j;
    	for (i = a.length() - 1, j = b.length() - 1; i >= 0|| j >= 0; --i, --j)
    	{
    		int t1, t2;
    		t1 = i < 0 ? 0 : a[i] - '0';
    		t2 = j < 0 ? 0 : b[j] - '0';
    		
    		int temp = t1 + t2 + carry;
    		if (temp >= 2)
    			carry = 1;
    		else
    			carry = 0;
    		res.push_back(temp%2);
    	}
    
    	if (carry)
    		res.push_back(1);
    	string result="";
    	for (int i = res.size() - 1; i >= 0; --i)
    	{
    		if (res[i])
    			result += '1';
    		else
    			result += '0';
    
    	}
    	return result;
    }
};
{% endhighlight %}

### Single Number ###
Given an array of integers, every element appears twice except for one. Find that single one.

{% highlight cpp %}
class Solution {
public:
    int singleNumber(int A[], int n) {
        int res = 0;
        for(int i=0;i<n;++i)
            res = res^A[i];
        return res;
    }
};
{% endhighlight %}

----------
