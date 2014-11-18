---
layout: post
---

<h2>{{ page.title }}</h2>
<p class='meta'>{{ page.date | date_to_string }} - NanJing</p>
----------

### LRU Cache ###
Design and implement a data structure for Least Recently Used (LRU) cache. It should support the following operations: get and set. get(key) - Get the value (will always be positive) of the key if the key exists in the cache, otherwise return -1. set(key, value) - Set or insert the value if the key is not already present. When the cache reached its capacity, it should invalidate the least recently used item before inserting a new item.

{% highlight cpp %}
class LRUCache{
private:
	struct CacheNode{
		int key;
		int value;
		CacheNode(int k, int v) :key(k), value(v){}
	};
public:
	LRUCache(int capacity) {
		this->capacity = capacity;
	}

	int get(int key) {
		if (cacheMap.find(key) == cacheMap.end())
			return -1;
		cacheList.splice(cacheList.begin(),cacheList,cacheMap[key]);
		cacheMap[key] = cacheList.begin();
		return cacheMap[key]->value;
	}

	void set(int key, int value) {
		if (cacheMap.find(key) == cacheMap.end())
		{
			if (cacheList.size() == capacity)
			{
				cacheMap.erase(cacheList.back().key);
				cacheList.pop_back();//cacheList.erase(cacheMap[key]);
			}
			cacheList.push_front(CacheNode(key, value));
			//cacheList.insert(cacheList.begin(), CacheNode(key, value));
			cacheMap[key] = cacheList.begin();
		}
		else
		{
			cacheMap[key]->value == value;
			cacheList.splice(cacheList.begin(), cacheList, cacheMap[key]);
			cacheMap[key] = cacheList.begin();
		}
	}
private:
	list<CacheNode> cacheList;
	unordered_map<int, list<CacheNode>::iterator> cacheMap;
	//#include <unordered_map>,需要有序时则选择hash_map（#include <hash_map>）
	int capacity;
};
{% endhighlight %}

### Roman to int ###

{% highlight cpp %}
class Solution {
public:
	inline int map(const char c) 
	{
		switch (c) {
			case 'I': return 1;
			case 'V': return 5;
			case 'X': return 10;
			case 'L': return 50;
			case 'C': return 100;
			case 'D': return 500;
			case 'M': return 1000;
			default: return 0;
		}
	}

	int romanToInt(string s) 
	{
		int result = 0;
		for (size_t i = 0; i < s.size(); i++) 
		{
			if (i > 0 && map(s[i]) > map(s[i - 1]))
			{
				result += (map(s[i]) - 2 * map(s[i - 1]));
			}
			else
			{
				result += map(s[i]);
			}
		}
		return result;
	}
};
{% endhighlight %}


----------
