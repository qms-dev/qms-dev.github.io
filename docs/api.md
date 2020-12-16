---
layout: default
title: 接口文档
nav_order: 4
has_children: false
permalink: docs/api
---

# 接口文档

> 实际使用过程中，替换示例API`/api`前面的部分即可

{: .no_toc }

## 接口名称
{: .no_toc .text-delta }

1. TOC
{:toc}

---

## 获取题目列表

> 获取当前平台的所有题目列表

**请求方法：**GET

**URL示例：**`https://example.com/api/questionset`

**返回结果（JSON）**

| 参数   | 类型   | 是否必填 | 描述             |
| ------ | ------ | -------- | ---------------- |
| status | Int    | 是       | 错误码           |
| msg    | String | 是       | 错误信息         |
| data   | Json   | 否       | 题目列表（全部） |

**题目列表（全部）**

| 参数       | 类型        | 是否必填 | 描述                                  |
| ---------- | ----------- | -------- | ------------------------------------- |
| id         | Int         | 是       | qmoj唯一题目id，不保证连续            |
| title      | String      | 是       | 题目标题                              |
| difficulty | Int         | 是       | 题目难度  (0/1/2对应easy/medium/hard) |
| topic_tags | Json(Array) | 是       | 题目的标签，中文形式                  |

**响应示例**

```json
{
    "status": 0,
    "msg": "",
    "data": {
        "list": [
            {
                "id": 1,
                "title": "两数之和",
                "difficulty": 0,
                "topic_tags": [
                    "数组",
                    "哈希表"
                ]
            },
            {
                "id": 2,
                "title": "三数之和",
                "difficulty": 1,
                "topic_tags": [
                    "数组",
                    "哈希表"
                ]
            }
        ]
    }
}
```

**错误示例**

```json
{
    "status": -1,
    "msg": "服务器内部错误，请重试"
}
```



## 获取题目列表（分页）

> 按照分页条件获取当前平台的题目列表

**接口说明：**所有参数在URL中直接作为参数拼接

**请求方法：**GET

**URL示例：**`https://example.com/api/questionset?pageNum=1&pageSize=5&orderBy=title desc`

**请求参数说明**

| 参数     | 是否必传 | 描述                                                       |
| -------- | -------- | ---------------------------------------------------------- |
| pageNum  | 是       | 页码，从1开始                                              |
| pageSize | 是       | 每页大小上限                                               |
| orderby  | 是       | 排序依据，在这里可以用`id`、`titile`、或者`difficulty`排序 |

**返回结果（JSON）**

| 参数   | 类型   | 是否必填 | 描述         |
| ------ | ------ | -------- | ------------ |
| status | Int    | 是       | 错误码       |
| msg    | String | 是       | 错误信息     |
| data   | Json   | 否       | 详细分页数据 |

**详细分页数据**

| 参数     | 类型 | 是否必填 | 描述             |
| -------- | ---- | -------- | ---------------- |
| pageNum  | Int  | 是       | 页码，从1开始    |
| pageSize | Int  | 是       | 本页的实际记录数 |
| total    | Int  | 是       | 记录总数         |
| pages    | Int  | 是       | 总页数           |
| list     | Json | 是       | 当前页的记录     |

**当前页的记录**

| 参数       | 类型        | 是否必填 | 描述                                  |
| ---------- | ----------- | -------- | ------------------------------------- |
| id         | Int         | 是       | qmoj唯一题目id，不保证连续            |
| title      | String      | 是       | 题目标题                              |
| difficulty | Int         | 是       | 题目难度  (0/1/2对应easy/medium/hard) |
| topic_tags | Json(Array) | 是       | 题目的标签，中文形式                  |

**响应示例**

```json
{
    "status": 0,
    "msg": "",
    "data": {
        "pageNum": 1,
        "pageSize": 2,
        "total": 12,
        "pages": 3,
        "list": [
            {
                "id": 1,
                "title": "两数之和",
                "difficulty": 0,
                "topic_tags": [
                    "数组",
                    "哈希表"
                ]
            },
            {
                "id": 2,
                "title": "三数之和",
                "difficulty": 1,
                "topic_tags": [
                    "数组",
                    "哈希表"
                ]
            }
        ]
    }
}
```

**错误示例**

```json
{
    "status": -1,
    "msg": "已超过当前最大页码数"
}
```



## 获取特定题目内容

> 通过题目唯一标识获取题目内容

**接口说明：**`id`在URL中直接作为参数拼接

**请求方法：**GET

**URL示例：**`https://example.com/api/questions?id=1`

**返回结果（JSON）**

| 参数   | 类型   | 是否必填 | 描述                                       |
| ------ | ------ | -------- | ------------------------------------------ |
| status | Int    | 是       | 错误码                                     |
| msg    | String | 是       | 错误信息                                   |
| data   | Json   | 否       | 题目内容，请求成功时携带，具体内容见下方表 |



**题目内容（JSON）**

| 参数       | 类型        | 是否必填 | 描述                                                         |
| ---------- | ----------- | -------- | ------------------------------------------------------------ |
| id         | Int         | 是       | qmoj唯一题目id                                               |
| platform   | String      | 是       | 来源平台(如：LeetCode，原创等)                               |
| title      | String      | 是       | 标题                                                         |
| content    | String      | 是       | 题目内容（带html标记的题干内容）                             |
| difficulty | Int         | 是       | 题目难度  (0/1/2对应easy/medium/hard)                        |
| languages  | Json(Array) | 是       | 支持的语言类型，从小到大排列，具体类型参考[语言类型参照表](/languagetypes) |
| topic_tags | Json(Array) | 是       | 题目的标签，中文形式                                         |



**响应示例**

```json
{
    "status": 0,
    "msg": "",
    "data": {
        "id": 1,
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
    "status": -1,
    "msg": "请求的题目不存在，请检查参数是否正确"
}
```



## 提交题解

> 提交题解到后端，并返回唯一的提交流水号

**接口说明：**请求参数使用JSON格式

**请求方法：**POST