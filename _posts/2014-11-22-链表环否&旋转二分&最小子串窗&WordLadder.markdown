---
layout: post
---

<h2>{{ page.title }}</h2>
<p class='meta'>{{ page.date | date_to_string }} - NanJing</p>
----------

### Linked List Cycle ###
Given a linked list, determine if it has a cycle in it.

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
    bool hasCycle(ListNode *head) {
        ListNode *slow = head, *fast = head;
        while (fast && fast->next) 
        {
            slow = slow->next;
            fast = fast->next->next;
            if (slow == fast) 
                return true;
        }
        return false;
    }
};
{% endhighlight %}

### Search in Rotated Sorted Array ###
Suppose a sorted array is rotated at some pivot unknown to you beforehand.(i.e., 0 1 2 4 5 6 7 might become 4 5 6 7 0 1 2).You are given a target value to search. If found in the array return its index, otherwise return -1. You may assume no duplicate exists in the array.

{% highlight cpp %}
class Solution {
public:
int search(int A[], int n, int target) {
        int first = 0, last = n;
        while (first != last)
        {
            const int mid = (first + last) / 2;
            if (A[mid] == target)
                return mid;
            if (A[first] <= A[mid])
            {
                if (A[first] <= target && target < A[mid])
                    last = mid;
                else
                    first = mid + 1;
            } 
            else
            {
                if (A[mid] < target && target <= A[last-1])
                    first = mid + 1;
                else
                    last = mid;
            }
        }
                return -1;
    }
};
{% endhighlight %}

### Minimum Window Substring ###
Given a string S and a string T, find the minimum window in S which will contain all the characters in T in complexity O(n).For example, S = "ADOBECODEBANC", T = "ABC", Minimum window is "BANC". Note: If there is no such window in S that covers all characters in T, return the emtpy string "". If there are multiple such windows, you are guaranteed that there will always be only one unique minimum window in S.

{% highlight cpp %}

	string minWindow(string S, string T) {
		if (S.empty()) return "";
		if (S.size() < T.size()) return "";
		const int ASCII_MAX = 128;
		int appeared_count[ASCII_MAX];
		int expected_count[ASCII_MAX];
		fill(appeared_count, appeared_count + ASCII_MAX, 0);
		fill(expected_count, expected_count + ASCII_MAX, 0);
		for (size_t i = 0; i < T.size(); i++) expected_count[T[i]]++;
		int minWidth = INT_MAX, min_start = 0;
		int wnd_start = 0;
		int appeared = 0;

		for (size_t wnd_end = 0; wnd_end < S.size(); wnd_end++)
		{
			if (expected_count[S[wnd_end]] > 0) 
			{
				appeared_count[S[wnd_end]]++;
				if (appeared_count[S[wnd_end]] <= expected_count[S[wnd_end]])
					appeared++;
			}
			if (appeared == T.size()) 
			{ 
				while (appeared_count[S[wnd_start]] > expected_count[S[wnd_start]]
					|| expected_count[S[wnd_start]] == 0) 
				{
					appeared_count[S[wnd_start]]--;
					wnd_start++;
				}
				if (minWidth > (wnd_end - wnd_start + 1)) 
				{
					minWidth = wnd_end - wnd_start + 1;
					min_start = wnd_start;
				}
			}
		}
		if (minWidth == INT_MAX) return "";
		else return S.substr(min_start, minWidth);
	}
{% endhighlight %}

### word ladder ###

给定start单词，end单词，以及一个dict字典。请求找出start到end的所有最短路径，路径上的每个单词都要呈如今dict中，且每次改变一个字母。如start="hit"; end="cog"; dict={"hot"，"dot"，"dog"，"lot"，"log"}，则答案为：[["hit"，"hot"，"dot"，"dog"，"cog"]，"hit"，"hot"，"lot"，"log"，"cog"]]。
{% highlight cpp %}
void gen_path(unordered_map<string, vector<string> > &father, vector<string> &path, const string &start, const string &word,
vector<vector<string> > &result)
{
	path.push_back(word);
	if (word == start)
	{
		result.push_back(path);
		reverse(result.back().begin(), result.back().end());
	}
	else
	{
		for (const auto& f : father[word])
		{
			gen_path(father, path, start, f, result);
		}
	}
	path.pop_back();
}

vector<vector<string>> findLadders(string start, string end, unordered_set<string> &dict) {
	unordered_set<string> current, next;
	unordered_set<string> visited;
	unordered_map<string, vector<string> > father;
	bool found = false;
	auto state_is_target = [&](const string &s) {return s == end;};
	auto state_extend = [&](const string &s)
	{
		unordered_set<string> result;
		for (size_t i = 0; i < s.size(); ++i)
		{
			string new_word(s);
			for (char c = 'a'; c <= 'z'; c++)
			{
				if (c == new_word[i]) 
					continue;
				swap(c, new_word[i]);
				if ((dict.count(new_word) > 0|| new_word == end) && !visited.count(new_word))
				{
					result.insert(new_word);
				}
				swap(c, new_word[i]);
			}
		}
		return result;
	};
	current.insert(start);
	while (!current.empty() && !found)
	{
		for (const auto& word : current)
		visited.insert(word);
		for (const auto& word : current)
		{
			const auto new_states = state_extend(word);
			for (const auto &state : new_states)
			{
				if (state_is_target(state)) found = true;
				next.insert(state);
				father[state].push_back(word);
			}
		}
		current.clear();
		swap(current, next);
	}
	vector<vector<string> > result;
	if (found)
	{
		vector<string> path;
		gen_path(father, path, start, end, result);
	}
	return result;
}
{% endhighlight %}

----------
