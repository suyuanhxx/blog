---
title: solr实践
date: 2017-11-22
tags:
---

## solr实践
Solr是一个高性能，基于Lucene的全文搜索服务器。同时对其进行了扩展，提供了比Lucene更为丰富的查询语言。实现了可配置、可扩展并对查询性能进行了优化，并且提供了一个完善的功能管理界面，是一款非常优秀的全文搜索引擎。
<!--more-->
## 工作方式
1. 文档通过Http利用XML 加到一个搜索集合中。
2. 查询该集合也是通过http收到一个XML/JSON响应来实现。
3. 它的主要特性包括：高效、灵活的缓存功能，垂直搜索功能，高亮显示搜索结果，通过索引复制来提高可用性，
4. 提供一套强大Data Schema来定义字段，类型和设置文本分析，提供基于Web的管理界面等。

## 特点
1. 索引，用来检索关键字
2. 分词，
3. “定时器”，定时“全量更新”和“重建索引”，防止数据不一致，或者查询效率低。
## 使用步骤：
1. solr服务器搭建搭建部署，配置
2. 将数据库中的查询内容导入到solr索引库，这里使用的是solrj的客户端实现的。
3. 建立搜索服务，供客户端调用。调用solr，查询内容，这中间有分页功能的实现等。solr高亮显示的实现。
4. 客户端接收页面的请求参数，调用搜索服务，进行搜索。
## solr相关命令
1. 启动 ./bin/solr start
2. 删除所以索引数据
    ```
    <delete><query>*:*</query></delete>
    <commit/>
    ```