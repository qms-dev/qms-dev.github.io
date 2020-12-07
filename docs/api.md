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

**接口说明：**`id`在URL中直接作为参数拼接

**请求方法：**GET

**请求URL：**https://example.com/api/problem?id={id}

**返回结果（JSON）**

| 参数    | 类型   | 是否必填 | 描述                                       |
| ------- | ------ | -------- | ------------------------------------------ |
| errcode | Int    | 是       | 错误码                                     |
| errmsg  | String | 是       | 错误信息                                   |
| data    | Json   | 否       | 题目内容，请求成功时携带，具体内容见下方表 |



**题目内容（JSON）**

| 参数        | 类型        | 是否必填 | 描述                                               |
| ----------- | ----------- | -------- | -------------------------------------------------- |
| question_id | Int         | 是       | 题目id，单平台来源唯一                             |
| platform    | String      | 是       | 来源平台(如：LeetCode，原创等)                     |
| title       | String      | 是       | 标题                                               |
| content     | String      | 是       | 题目内容（带html标记的题干内容）                   |
| difficulty  | Int         | 是       | 题目难度  (0/1/2对应easy/medium/hard)              |
| languages   | Json(Array) | 是       | 支持的语言类型，从小到大排列，具体类型参考语言类表 |
| topic_tags  | Json(Array) | 是       | 题目的标签，中文形式                               |



**响应示例**

```json
{
    "errcode": 200,
    "errmsg": "",
    "data": {
        "question_id": 1,
        "platform": "LeetCode",
        "title": "两数之和",
        "content": "<p>给定一个整数数组 <code>nums</code>&nbsp;和一个目标值 <code>target</code>，请你在该数组中找出和为目标值的那&nbsp;<strong>两个</strong>&nbsp;整数，并返回他们的数组下标。</p>\n\n<p>你可以假设每种输入只会对应一个答案。但是，数组中同一个元素不能使用两遍。</p>\n\n<p>&nbsp;</p>\n\n<p><strong>示例:</strong></p>\n\n<pre>给定 nums = [2, 7, 11, 15], target = 9\n\n因为 nums[<strong>0</strong>] + nums[<strong>1</strong>] = 2 + 7 = 9\n所以返回 [<strong>0, 1</strong>]\n</pre>\n",
        "difficulty": 1,
        "languages": [
            0,
            1,
            2
        ],
        "topic_tags": [
            "数组",
            "哈希表"
        ]
    }
}
```



**错误示例**

```json
{
    "errcode": 400,
    "errmsg": "请求的题目不存在，请检查参数是否正确",
}
```

