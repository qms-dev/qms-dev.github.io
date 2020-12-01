---
layout: default
title: 接口文档
nav_order: 4
has_children: false
permalink: docs/api
---

# 接口文档
{: .no_toc }

## 接口名称
{: .no_toc .text-delta }

1. TOC
{:toc}

---

## 获取特定题目内容

> 通过题目唯一标识获取题目内容

**请求方式**

**接口说明：**`id`在URL中直接作为参数拼接

**请求方法：**GET

**请求URL：**https://example.com/api/problem?id={id}

**返回结果（JSON）**

| 参数        | 类型   | 是否必填 | 描述                             |
| ----------- | ------ | -------- | -------------------------------- |
| errcode     | Int    | 是       | 错误码                           |
| errmsg      | String | 是       | 错误信息                         |
| question_id | Int    | 是       | 题目id，单平台来源唯一           |
| platform    | String | 是       | 来源平台                         |
| title       | String | 是       | 标题                             |
| content     | String | 是       | 题目内容（带html标记的题干内容） |
| difficulty  | String | 是       | 题目难度  (easy/medium/hard)     |



**示例**

```json
返回：
{
    
}
```

