---
layout: post
---

<h2>{{ page.title }}</h2>
<p class='meta'>{{ page.date | date_to_string }} - NanJing</p>

---

### solr app接口 ###

上传全部配置：
java -classpath .:/home/uss/cloud/lib/* org.apache.solr.cloud.ZkCLI -cmd upconfig -zkhost 10.148.134.8:4181,10.148.163.3:4181,10.148.163.4:4181 -confdir /home/uss/cloud/conf/book_conf/conf/ -confname test_conf

更新单个文件：（前参数是目标文件，后参数是本地文件）
java -classpath .:/home/reader/cloud/lib/* org.apache.solr.cloud.ZkCLI -zkhost 10.148.134.8:3181,10.148.163.3:3181,10.148.163.4:3181 -cmd putfile /configs/book_conf/managed-schema /home/reader/cloud/conf/book_conf/conf/managed-schema

创建collection：
http://10.124.2.34:8983/solr/admin/collections?action=CREATE&name=test_collection&numShards=1&replicationFactor=2&collection.configName=test_conf

删除collection：
http://10.124.2.34:8983/solr/admin/collections?action=DELETE&name=test_collection

Reload Collection:
http://10.124.2.34:8983/solr/admin/collections?action=RELOAD&name=test_collection


### Docker搭建solrCloud集群 ###

http://www.linuxidc.com/Linux/2017-09/146842.htm

### docker间通信 ###

http://blog.51cto.com/ylw6006/1606239

---

