---
title: logseq/query
public: true
tags:
date: 2024-10-05
updated: 2024-10-05
toc: true
mathjax: true
---

`{{query (page-tags paper)}}`
query-table:: false
query-properties:: [:title :tags]

[Logseq's database schema](https://github.com/logseq/logseq/blob/master/deps/db/src/logseq/db/schema.cljs)

[queries (logseq.com)](https://docs.logseq.com/#/page/queries)

[Advanced Queries (logseq.com)](https://docs.logseq.com/#/page/Advanced%20Queries)

  + [query祛魅 (logseq.pro)](https://logseq.pro/#/page/query%E7%A5%9B%E9%AD%85)

`{{query (and (page-tags tag1) (page-tags tag2)) }}`

advanced query

  + 获取包含 `#Paper` 标记笔记中的所有 todo

```clojure
{{< logseq/orgQUERY >}}{:title [:h2 "Doing"]
  :query [:find (pull ?b [*])
:where
  [?p :block/name]
  ; 取page的page-properties
  [?p :block/properties ?prop]
  ; 取page-properties中“publication-title:: value1, value1, value3”的值
  ; 即: 取出列表“value1, value1, value3”
  [(get ?prop :tags) ?v] 
  [(contains? ?v "Paper")]
  [?b :block/page ?p]
  [?b :block/marker ?m]
  [(= ?m "TODO")]
]
}
{{< / logseq/orgQUERY >}}
```

  + [我的 Logseq 使用习惯 (limboy.me)](https://limboy.me/posts/logseq/)

    + 找到所有引用了包含  `category`  属性为  `Programming`  的页面的 Block。

``` clojure
{{< logseq/orgQUERY >}}; 以下注释是我查找网上文章结合自己的理解，不一定对
; '?xxx' 表示一个变量
; '$' 表示数据库
; ':xxx' 表示字段和查询关键字
{:title [:h2 "Todo"]
 :query [:find (pull ?b [*]) ;找到所有符合条件的条目，'*' 表示条目的所有字段
 :in $ ?category ;'?category' 就是通过 'inputs' 传过来的变量
 :where
  [?b :block/ref-pages ?p] ;条件语句用 '[]' 表示，?p 是什么下面会说明
  [?p :block/properties ?pr] ;?p 是包含了 properties 为 ?pr 的页面，?pr 是什么，下面会说明
  [(get ?pr :category) ?t] ; get 是获取 object 的属性，并将它设置为 ?t
  [(contains? ?t ?category)]; contains?（注意'?'在后面）表示 predict，也就是符合特定条件
  (not [?b :block/marker ?m]); not [xxx] 表示对 [xxx] 的结果取反
 ]
 :inputs ["Programming"] ; 传入一个参数
}
{{< / logseq/orgQUERY >}}
```

    + 找到标记为 TODO

``` clojure
{{< logseq/orgQUERY >}}{:title [:h2 "Doing"]
 :query [:find (pull ?b [*])
 :in $ ?category
:where
 [?b :block/marker ?m]
 [(= ?m "TODO")]
 [?b :block/ref-pages ?p]
 [?p :block/properties ?pr]
 [(get ?pr :category) ?t]
 [(contains? ?t ?category)]
]
 :inputs ["Programming"]
}
{{< / logseq/orgQUERY >}}
```




