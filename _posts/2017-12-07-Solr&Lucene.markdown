---
layout: post
---

<h2>{{ page.title }}</h2>
<p class='meta'>{{ page.date | date_to_string }} - NanJing</p>

---
 
http://10.124.0.109:8888/solr/f8564dfb90874dcdad56e48b1d13115c_shard1_replica2/select?q=坦克+坦克*%5E5&sort=score+desc&fl=ID%2CNAME%2Cname_s%2Cscore%2Cdoc&wt=json&indent=true&debugQuery=true&defType=edismax&qf=NAME+name_s%5E10&stopwords=true&lowercaseOperators=true&debug.explain.structured=true

完全匹配使用fq进行过滤即可  
其中name_s为不分词字段，NAME为分词字段  
查询域NAME name_s^10	 
name_s字段中包含“坦克”的文档数(docFreq=1, maxDocs=4393217)  
NAME字段中包含“坦克”的文档数 (docFreq=793, maxDocs=4393217)  

weight(name_s:坦克^10.0 in 32002)，因为name_s为不分词字段，当目标文档的name_s为“坦克”时，得分最大，为其他时无匹配，不得分。  
weight(NAME:坦克 in 32002)，因为NAME为分词字段，当目标文档的NAME包含“坦克”时，匹配并得分，但由于idf太大，此时得分较低。  
weight(name_s:坦克*^10.0 in 32002)，因为name_s为不分词字段，当目标文档的name_s以“坦克”开头时，得分，其他不得分。  
weight(NAME:坦克*^10.0 in 32002)，因为NAME为分词字段，当目标文档的NAME包含“坦克”时，匹配并得分，且得分相同。  
其中，当包含*时，默认相似度得分仅来源queryNorm，与tf，idf无关。

    {
      "responseHeader":{
    "status":0,
    "QTime":3,
    "params":{
      "q":"坦克 坦克*^10",
      "defType":"edismax",
      "indent":"true",
      "qf":"NAME name_s^10",
      "fl":"ID,NAME,name_s,score,doc",
      "sort":"score desc",
      "rows":"10",
      "wt":"json",
      "lowercaseOperators":"true",
      "debug.explain.structured":"true",
      "debugQuery":"true",
      "stopwords":"true"}},
      "response":{"numFound":784,"start":0,"maxScore":13.675559,"docs":[
      {
    "ID":"50000000000382100218",
    "NAME":"坦克",
    "name_s":["坦克"],
    "score":13.675559},
      {
    "ID":"10000000006116099000",
    "NAME":"坦克帝国",
    "name_s":["坦克帝国"],
    "score":0.8516184},
      {
    "ID":"10000000006122533000",
    "NAME":"坦克战神",
    "name_s":["坦克战神"],
    "score":0.8516184},
      {
    "ID":"10000000006124542000",
    "NAME":"坦克传奇",
    "name_s":["坦克传奇"],
    "score":0.8516184},
      {
    "ID":"10000000006128060000",
    "NAME":"坦克联盟",
    "name_s":["坦克联盟"],
    "score":0.8516184},
      {
    "ID":"30000000000621115512",
    "NAME":"坦克大赛19国坦克手角逐",
    "name_s":["坦克大赛19国坦克手角逐"],
    "score":0.8043574},
      {
    "ID":"10000000006106931000",
    "NAME":"坦克闯关",
    "name_s":["坦克闯关"],
    "score":0.78921604},
      {
    "ID":"10000000006117450000",
    "NAME":"坦克大战全民高手",
    "name_s":["坦克大战全民高手"],
    "score":0.78921604},
      {
    "ID":"10000000006117898000",
    "NAME":"坦克之战",
    "name_s":["坦克之战"],
    "score":0.78921604},
      {
    "ID":"10000000006123522000",
    "NAME":"坦克大战",
    "name_s":["坦克大战"],
    "score":0.78921604}]
      },
      "debug":{
    "queryBoosting":{
      "q":"坦克 坦克*^10",
      "match":null},
    "rawquerystring":"坦克 坦克*^10",
    "querystring":"坦克 坦克*^10",
    "parsedquery":"(+(DisjunctionMaxQuery((name_s:坦克^10.0 | NAME:坦克)) DisjunctionMaxQuery((name_s:坦克*^10.0 | NAME:坦克*)^10.0)))/no_coord",
    "parsedquery_toString":"+((name_s:坦克^10.0 | NAME:坦克) (name_s:坦克*^10.0 | NAME:坦克*)^10.0)",
    "explain":{
      "50000000000382100218":{
    "match":true,
    "value":13.675559,
    "description":"sum of:",
    "details":[{
    "match":true,
    "value":13.135952,
    "description":"max of:",
    "details":[{
    "match":true,
    "value":13.135952,
    "description":"weight(name_s:坦克^10.0 in 32002) [DefaultSimilarity], result of:",
    "details":[{
    "match":true,
    "value":13.135952,
    "description":"score(doc=32002,freq=1.0), product of:",
    "details":[{
    "match":true,
    "value":0.8419173,
    "description":"queryWeight, product of:",
    "details":[{
    "match":true,
    "value":10.0,
    "description":"boost"},
      {
    "match":true,
    "value":15.602426,
    "description":"idf(docFreq=1, maxDocs=4393217)"},
      {
    "match":true,
    "value":0.0053960662,
    "description":"queryNorm"}]},
      {
    "match":true,
    "value":15.602426,
    "description":"fieldWeight in 32002, product of:",
    "details":[{
    "match":true,
    "value":1.0,
    "description":"tf(freq=1.0), with freq of:",
    "details":[{
    "match":true,
    "value":1.0,
    "description":"termFreq=1.0"}]},
      {
    "match":true,
    "value":15.602426,
    "description":"idf(docFreq=1, maxDocs=4393217)"},
      {
    "match":true,
    "value":1.0,
    "description":"fieldNorm(doc=32002)"}]}]}]},
      {
    "match":true,
    "value":0.49921885,
    "description":"weight(NAME:坦克 in 32002) [DefaultSimilarity], result of:",
    "details":[{
    "match":true,
    "value":0.49921885,
    "description":"score(doc=32002,freq=1.0), product of:",
    "details":[{
    "match":true,
    "value":0.051902004,
    "description":"queryWeight, product of:",
    "details":[{
    "match":true,
    "value":9.618489,
    "description":"idf(docFreq=793, maxDocs=4393217)"},
      {
    "match":true,
    "value":0.0053960662,
    "description":"queryNorm"}]},
      {
    "match":true,
    "value":9.618489,
    "description":"fieldWeight in 32002, product of:",
    "details":[{
    "match":true,
    "value":1.0,
    "description":"tf(freq=1.0), with freq of:",
    "details":[{
    "match":true,
    "value":1.0,
    "description":"termFreq=1.0"}]},
      {
    "match":true,
    "value":9.618489,
    "description":"idf(docFreq=793, maxDocs=4393217)"},
      {
    "match":true,
    "value":1.0,
    "description":"fieldNorm(doc=32002)"}]}]}]}]},
      {
    "match":true,
    "value":0.53960663,
    "description":"max of:",
    "details":[{
    "match":true,
    "value":0.53960663,
    "description":"name_s:坦克*^10.0, product of:",
    "details":[{
    "match":true,
    "value":10.0,
    "description":"boost"},
      {
    "match":true,
    "value":0.053960662,
    "description":"queryNorm"}]},
      {
    "match":true,
    "value":0.053960662,
    "description":"NAME:坦克*, product of:",
    "details":[{
    "match":true,
    "value":1.0,
    "description":"boost"},
      {
    "match":true,
    "value":0.053960662,
    "description":"queryNorm"}]}]}]},
      "10000000006116099000":{
    "match":true,
    "value":0.8516184,
    "description":"sum of:",
    "details":[{
    "match":true,
    "value":0.31201178,
    "description":"max of:",
    "details":[{
    "match":true,
    "value":0.31201178,
    "description":"weight(NAME:坦克 in 1918) [DefaultSimilarity], result of:",
    "details":[{
    "match":true,
    "value":0.31201178,
    "description":"score(doc=1918,freq=1.0), product of:",
    "details":[{
    "match":true,
    "value":0.051902004,
    "description":"queryWeight, product of:",
    "details":[{
    "match":true,
    "value":9.618489,
    "description":"idf(docFreq=793, maxDocs=4393217)"},
      {
    "match":true,
    "value":0.0053960662,
    "description":"queryNorm"}]},
      {
    "match":true,
    "value":6.0115557,
    "description":"fieldWeight in 1918, product of:",
    "details":[{
    "match":true,
    "value":1.0,
    "description":"tf(freq=1.0), with freq of:",
    "details":[{
    "match":true,
    "value":1.0,
    "description":"termFreq=1.0"}]},
      {
    "match":true,
    "value":9.618489,
    "description":"idf(docFreq=793, maxDocs=4393217)"},
      {
    "match":true,
    "value":0.625,
    "description":"fieldNorm(doc=1918)"}]}]}]}]},
      {
    "match":true,
    "value":0.53960663,
    "description":"max of:",
    "details":[{
    "match":true,
    "value":0.53960663,
    "description":"name_s:坦克*^10.0, product of:",
    "details":[{
    "match":true,
    "value":10.0,
    "description":"boost"},
      {
    "match":true,
    "value":0.053960662,
    "description":"queryNorm"}]},
      {
    "match":true,
    "value":0.053960662,
    "description":"NAME:坦克*, product of:",
    "details":[{
    "match":true,
    "value":1.0,
    "description":"boost"},
      {
    "match":true,
    "value":0.053960662,
    "description":"queryNorm"}]}]}]},
      "10000000006122533000":{
    "match":true,
    "value":0.8516184,
    "description":"sum of:",
    "details":[{
    "match":true,
    "value":0.31201178,
    "description":"max of:",
    "details":[{
    "match":true,
    "value":0.31201178,
    "description":"weight(NAME:坦克 in 2261) [DefaultSimilarity], result of:",
    "details":[{
    "match":true,
    "value":0.31201178,
    "description":"score(doc=2261,freq=1.0), product of:",
    "details":[{
    "match":true,
    "value":0.051902004,
    "description":"queryWeight, product of:",
    "details":[{
    "match":true,
    "value":9.618489,
    "description":"idf(docFreq=793, maxDocs=4393217)"},
      {
    "match":true,
    "value":0.0053960662,
    "description":"queryNorm"}]},
      {
    "match":true,
    "value":6.0115557,
    "description":"fieldWeight in 2261, product of:",
    "details":[{
    "match":true,
    "value":1.0,
    "description":"tf(freq=1.0), with freq of:",
    "details":[{
    "match":true,
    "value":1.0,
    "description":"termFreq=1.0"}]},
      {
    "match":true,
    "value":9.618489,
    "description":"idf(docFreq=793, maxDocs=4393217)"},
      {
    "match":true,
    "value":0.625,
    "description":"fieldNorm(doc=2261)"}]}]}]}]},
      {
    "match":true,
    "value":0.53960663,
    "description":"max of:",
    "details":[{
    "match":true,
    "value":0.53960663,
    "description":"name_s:坦克*^10.0, product of:",
    "details":[{
    "match":true,
    "value":10.0,
    "description":"boost"},
      {
    "match":true,
    "value":0.053960662,
    "description":"queryNorm"}]},
      {
    "match":true,
    "value":0.053960662,
    "description":"NAME:坦克*, product of:",
    "details":[{
    "match":true,
    "value":1.0,
    "description":"boost"},
      {
    "match":true,
    "value":0.053960662,
    "description":"queryNorm"}]}]}]},
      "10000000006124542000":{
    "match":true,
    "value":0.8516184,
    "description":"sum of:",
    "details":[{
    "match":true,
    "value":0.31201178,
    "description":"max of:",
    "details":[{
    "match":true,
    "value":0.31201178,
    "description":"weight(NAME:坦克 in 2421) [DefaultSimilarity], result of:",
    "details":[{
    "match":true,
    "value":0.31201178,
    "description":"score(doc=2421,freq=1.0), product of:",
    "details":[{
    "match":true,
    "value":0.051902004,
    "description":"queryWeight, product of:",
    "details":[{
    "match":true,
    "value":9.618489,
    "description":"idf(docFreq=793, maxDocs=4393217)"},
      {
    "match":true,
    "value":0.0053960662,
    "description":"queryNorm"}]},
      {
    "match":true,
    "value":6.0115557,
    "description":"fieldWeight in 2421, product of:",
    "details":[{
    "match":true,
    "value":1.0,
    "description":"tf(freq=1.0), with freq of:",
    "details":[{
    "match":true,
    "value":1.0,
    "description":"termFreq=1.0"}]},
      {
    "match":true,
    "value":9.618489,
    "description":"idf(docFreq=793, maxDocs=4393217)"},
      {
    "match":true,
    "value":0.625,
    "description":"fieldNorm(doc=2421)"}]}]}]}]},
      {
    "match":true,
    "value":0.53960663,
    "description":"max of:",
    "details":[{
    "match":true,
    "value":0.53960663,
    "description":"name_s:坦克*^10.0, product of:",
    "details":[{
    "match":true,
    "value":10.0,
    "description":"boost"},
      {
    "match":true,
    "value":0.053960662,
    "description":"queryNorm"}]},
      {
    "match":true,
    "value":0.053960662,
    "description":"NAME:坦克*, product of:",
    "details":[{
    "match":true,
    "value":1.0,
    "description":"boost"},
      {
    "match":true,
    "value":0.053960662,
    "description":"queryNorm"}]}]}]},
      "10000000006128060000":{
    "match":true,
    "value":0.8516184,
    "description":"sum of:",
    "details":[{
    "match":true,
    "value":0.31201178,
    "description":"max of:",
    "details":[{
    "match":true,
    "value":0.31201178,
    "description":"weight(NAME:坦克 in 2670) [DefaultSimilarity], result of:",
    "details":[{
    "match":true,
    "value":0.31201178,
    "description":"score(doc=2670,freq=1.0), product of:",
    "details":[{
    "match":true,
    "value":0.051902004,
    "description":"queryWeight, product of:",
    "details":[{
    "match":true,
    "value":9.618489,
    "description":"idf(docFreq=793, maxDocs=4393217)"},
      {
    "match":true,
    "value":0.0053960662,
    "description":"queryNorm"}]},
      {
    "match":true,
    "value":6.0115557,
    "description":"fieldWeight in 2670, product of:",
    "details":[{
    "match":true,
    "value":1.0,
    "description":"tf(freq=1.0), with freq of:",
    "details":[{
    "match":true,
    "value":1.0,
    "description":"termFreq=1.0"}]},
      {
    "match":true,
    "value":9.618489,
    "description":"idf(docFreq=793, maxDocs=4393217)"},
      {
    "match":true,
    "value":0.625,
    "description":"fieldNorm(doc=2670)"}]}]}]}]},
      {
    "match":true,
    "value":0.53960663,
    "description":"max of:",
    "details":[{
    "match":true,
    "value":0.53960663,
    "description":"name_s:坦克*^10.0, product of:",
    "details":[{
    "match":true,
    "value":10.0,
    "description":"boost"},
      {
    "match":true,
    "value":0.053960662,
    "description":"queryNorm"}]},
      {
    "match":true,
    "value":0.053960662,
    "description":"NAME:坦克*, product of:",
    "details":[{
    "match":true,
    "value":1.0,
    "description":"boost"},
      {
    "match":true,
    "value":0.053960662,
    "description":"queryNorm"}]}]}]},
      "30000000000621115512":{
    "match":true,
    "value":0.8043574,
    "description":"sum of:",
    "details":[{
    "match":true,
    "value":0.26475078,
    "description":"max of:",
    "details":[{
    "match":true,
    "value":0.26475078,
    "description":"weight(NAME:坦克 in 1303619) [DefaultSimilarity], result of:",
    "details":[{
    "match":true,
    "value":0.26475078,
    "description":"score(doc=1303619,freq=2.0), product of:",
    "details":[{
    "match":true,
    "value":0.051902004,
    "description":"queryWeight, product of:",
    "details":[{
    "match":true,
    "value":9.618489,
    "description":"idf(docFreq=793, maxDocs=4393217)"},
      {
    "match":true,
    "value":0.0053960662,
    "description":"queryNorm"}]},
      {
    "match":true,
    "value":5.100974,
    "description":"fieldWeight in 1303619, product of:",
    "details":[{
    "match":true,
    "value":1.4142135,
    "description":"tf(freq=2.0), with freq of:",
    "details":[{
    "match":true,
    "value":2.0,
    "description":"termFreq=2.0"}]},
      {
    "match":true,
    "value":9.618489,
    "description":"idf(docFreq=793, maxDocs=4393217)"},
      {
    "match":true,
    "value":0.375,
    "description":"fieldNorm(doc=1303619)"}]}]}]}]},
      {
    "match":true,
    "value":0.53960663,
    "description":"max of:",
    "details":[{
    "match":true,
    "value":0.53960663,
    "description":"name_s:坦克*^10.0, product of:",
    "details":[{
    "match":true,
    "value":10.0,
    "description":"boost"},
      {
    "match":true,
    "value":0.053960662,
    "description":"queryNorm"}]},
      {
    "match":true,
    "value":0.053960662,
    "description":"NAME:坦克*, product of:",
    "details":[{
    "match":true,
    "value":1.0,
    "description":"boost"},
      {
    "match":true,
    "value":0.053960662,
    "description":"queryNorm"}]}]}]},
      "10000000006106931000":{
    "match":true,
    "value":0.78921604,
    "description":"sum of:",
    "details":[{
    "match":true,
    "value":0.24960943,
    "description":"max of:",
    "details":[{
    "match":true,
    "value":0.24960943,
    "description":"weight(NAME:坦克 in 1541) [DefaultSimilarity], result of:",
    "details":[{
    "match":true,
    "value":0.24960943,
    "description":"score(doc=1541,freq=1.0), product of:",
    "details":[{
    "match":true,
    "value":0.051902004,
    "description":"queryWeight, product of:",
    "details":[{
    "match":true,
    "value":9.618489,
    "description":"idf(docFreq=793, maxDocs=4393217)"},
      {
    "match":true,
    "value":0.0053960662,
    "description":"queryNorm"}]},
      {
    "match":true,
    "value":4.8092446,
    "description":"fieldWeight in 1541, product of:",
    "details":[{
    "match":true,
    "value":1.0,
    "description":"tf(freq=1.0), with freq of:",
    "details":[{
    "match":true,
    "value":1.0,
    "description":"termFreq=1.0"}]},
      {
    "match":true,
    "value":9.618489,
    "description":"idf(docFreq=793, maxDocs=4393217)"},
      {
    "match":true,
    "value":0.5,
    "description":"fieldNorm(doc=1541)"}]}]}]}]},
      {
    "match":true,
    "value":0.53960663,
    "description":"max of:",
    "details":[{
    "match":true,
    "value":0.53960663,
    "description":"name_s:坦克*^10.0, product of:",
    "details":[{
    "match":true,
    "value":10.0,
    "description":"boost"},
      {
    "match":true,
    "value":0.053960662,
    "description":"queryNorm"}]},
      {
    "match":true,
    "value":0.053960662,
    "description":"NAME:坦克*, product of:",
    "details":[{
    "match":true,
    "value":1.0,
    "description":"boost"},
      {
    "match":true,
    "value":0.053960662,
    "description":"queryNorm"}]}]}]},
      "10000000006117450000":{
    "match":true,
    "value":0.78921604,
    "description":"sum of:",
    "details":[{
    "match":true,
    "value":0.24960943,
    "description":"max of:",
    "details":[{
    "match":true,
    "value":0.24960943,
    "description":"weight(NAME:坦克 in 1990) [DefaultSimilarity], result of:",
    "details":[{
    "match":true,
    "value":0.24960943,
    "description":"score(doc=1990,freq=1.0), product of:",
    "details":[{
    "match":true,
    "value":0.051902004,
    "description":"queryWeight, product of:",
    "details":[{
    "match":true,
    "value":9.618489,
    "description":"idf(docFreq=793, maxDocs=4393217)"},
      {
    "match":true,
    "value":0.0053960662,
    "description":"queryNorm"}]},
      {
    "match":true,
    "value":4.8092446,
    "description":"fieldWeight in 1990, product of:",
    "details":[{
    "match":true,
    "value":1.0,
    "description":"tf(freq=1.0), with freq of:",
    "details":[{
    "match":true,
    "value":1.0,
    "description":"termFreq=1.0"}]},
      {
    "match":true,
    "value":9.618489,
    "description":"idf(docFreq=793, maxDocs=4393217)"},
      {
    "match":true,
    "value":0.5,
    "description":"fieldNorm(doc=1990)"}]}]}]}]},
      {
    "match":true,
    "value":0.53960663,
    "description":"max of:",
    "details":[{
    "match":true,
    "value":0.53960663,
    "description":"name_s:坦克*^10.0, product of:",
    "details":[{
    "match":true,
    "value":10.0,
    "description":"boost"},
      {
    "match":true,
    "value":0.053960662,
    "description":"queryNorm"}]},
      {
    "match":true,
    "value":0.053960662,
    "description":"NAME:坦克*, product of:",
    "details":[{
    "match":true,
    "value":1.0,
    "description":"boost"},
      {
    "match":true,
    "value":0.053960662,
    "description":"queryNorm"}]}]}]},
      "10000000006117898000":{
    "match":true,
    "value":0.78921604,
    "description":"sum of:",
    "details":[{
    "match":true,
    "value":0.24960943,
    "description":"max of:",
    "details":[{
    "match":true,
    "value":0.24960943,
    "description":"weight(NAME:坦克 in 2018) [DefaultSimilarity], result of:",
    "details":[{
    "match":true,
    "value":0.24960943,
    "description":"score(doc=2018,freq=1.0), product of:",
    "details":[{
    "match":true,
    "value":0.051902004,
    "description":"queryWeight, product of:",
    "details":[{
    "match":true,
    "value":9.618489,
    "description":"idf(docFreq=793, maxDocs=4393217)"},
      {
    "match":true,
    "value":0.0053960662,
    "description":"queryNorm"}]},
      {
    "match":true,
    "value":4.8092446,
    "description":"fieldWeight in 2018, product of:",
    "details":[{
    "match":true,
    "value":1.0,
    "description":"tf(freq=1.0), with freq of:",
    "details":[{
    "match":true,
    "value":1.0,
    "description":"termFreq=1.0"}]},
      {
    "match":true,
    "value":9.618489,
    "description":"idf(docFreq=793, maxDocs=4393217)"},
      {
    "match":true,
    "value":0.5,
    "description":"fieldNorm(doc=2018)"}]}]}]}]},
      {
    "match":true,
    "value":0.53960663,
    "description":"max of:",
    "details":[{
    "match":true,
    "value":0.53960663,
    "description":"name_s:坦克*^10.0, product of:",
    "details":[{
    "match":true,
    "value":10.0,
    "description":"boost"},
      {
    "match":true,
    "value":0.053960662,
    "description":"queryNorm"}]},
      {
    "match":true,
    "value":0.053960662,
    "description":"NAME:坦克*, product of:",
    "details":[{
    "match":true,
    "value":1.0,
    "description":"boost"},
      {
    "match":true,
    "value":0.053960662,
    "description":"queryNorm"}]}]}]},
      "10000000006123522000":{
    "match":true,
    "value":0.78921604,
    "description":"sum of:",
    "details":[{
    "match":true,
    "value":0.24960943,
    "description":"max of:",
    "details":[{
    "match":true,
    "value":0.24960943,
    "description":"weight(NAME:坦克 in 2320) [DefaultSimilarity], result of:",
    "details":[{
    "match":true,
    "value":0.24960943,
    "description":"score(doc=2320,freq=1.0), product of:",
    "details":[{
    "match":true,
    "value":0.051902004,
    "description":"queryWeight, product of:",
    "details":[{
    "match":true,
    "value":9.618489,
    "description":"idf(docFreq=793, maxDocs=4393217)"},
      {
    "match":true,
    "value":0.0053960662,
    "description":"queryNorm"}]},
      {
    "match":true,
    "value":4.8092446,
    "description":"fieldWeight in 2320, product of:",
    "details":[{
    "match":true,
    "value":1.0,
    "description":"tf(freq=1.0), with freq of:",
    "details":[{
    "match":true,
    "value":1.0,
    "description":"termFreq=1.0"}]},
      {
    "match":true,
    "value":9.618489,
    "description":"idf(docFreq=793, maxDocs=4393217)"},
      {
    "match":true,
    "value":0.5,
    "description":"fieldNorm(doc=2320)"}]}]}]}]},
      {
    "match":true,
    "value":0.53960663,
    "description":"max of:",
    "details":[{
    "match":true,
    "value":0.53960663,
    "description":"name_s:坦克*^10.0, product of:",
    "details":[{
    "match":true,
    "value":10.0,
    "description":"boost"},
      {
    "match":true,
    "value":0.053960662,
    "description":"queryNorm"}]},
      {
    "match":true,
    "value":0.053960662,
    "description":"NAME:坦克*, product of:",
    "details":[{
    "match":true,
    "value":1.0,
    "description":"boost"},
      {
    "match":true,
    "value":0.053960662,
    "description":"queryNorm"}]}]}]}},
    "QParser":"ExtendedDismaxQParser",
    "altquerystring":null,
    "boost_queries":null,
    "parsed_boost_queries":[],
    "boostfuncs":null,
    "timing":{
      "time":3.0,
      "prepare":{
    "time":0.0,
    "query":{
      "time":0.0},
    "facet":{
      "time":0.0},
    "facet_module":{
      "time":0.0},
    "mlt":{
      "time":0.0},
    "highlight":{
      "time":0.0},
    "stats":{
      "time":0.0},
    "expand":{
      "time":0.0},
    "elevator":{
      "time":0.0},
    "debug":{
      "time":0.0}},
      "process":{
    "time":2.0,
    "query":{
      "time":0.0},
    "facet":{
      "time":0.0},
    "facet_module":{
      "time":0.0},
    "mlt":{
      "time":0.0},
    "highlight":{
      "time":0.0},
    "stats":{
      "time":0.0},
    "expand":{
      "time":0.0},
    "elevator":{
      "time":0.0},
    "debug":{
      "time":2.0}}}}}

### 一些优化 ###

OR 得分由sum改为max（5.3.1）不行  
     org.apache.lucene.search.DisjunctionSumScorer.score()
     org.apache.lucene.search.BooleanScorer.scoreDocument()
     org.apache.lucene.search.BooleanScorer.collect()

重写DF-IDF相似度算法，屏蔽fileldLength、tf、idf影响（6..6.0）

修复查询解析器mm，只对分词有效（英文搜索受影响）（6..6.0）
org.apache.solr.search.ExtendDismaxQparser.parseOriginalQuery()
solr start -p 8888 -f -a "-Xdebug -Xrunjdwp:transport=dt_socket,server=y,suspend=y,address=8888

---

