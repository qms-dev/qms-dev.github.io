---
layout: default
title: 接口文档
nav_order: 4
has_children: false
permalink: docs/api
---

# 接口文档

> 实际使用过程中，替换``https://example.com`即可

{: .no_toc }

## 接口名称
{: .no_toc .text-delta }

1. TOC
{:toc}

---

## 获取题目列表(完成)

> 获取当前平台的所有题目列表

**请求方法：**GET

**URL示例：**`https://example.com/questionset`

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
| topicTags  | Json(Array) | 是       | 题目的标签，中文形式                  |

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
                "topicTags": [
                    "数组",
                    "哈希表"
                ]
            },
            {
                "id": 2,
                "title": "三数之和",
                "difficulty": 1,
                "topicTags": [
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



## 获取题目列表（分页）(未完成)

> 按照分页条件获取当前平台的题目列表

**接口说明：**所有参数在URL中直接作为参数拼接

**请求方法：**GET

**URL示例：**`https://example.com/questionset?pageNum=1&pageSize=5&orderBy=title desc`

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
| topicTags  | Json(Array) | 是       | 题目的标签，中文形式                  |

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
                "topicTags": [
                    "数组",
                    "哈希表"
                ]
            },
            {
                "id": 2,
                "title": "三数之和",
                "difficulty": 1,
                "topicTags": [
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



## 获取特定题目内容(完成)

> 通过题目唯一标识获取题目内容

**接口说明：**`id`在URL中直接作为参数拼接

**请求方法：**GET

**URL示例：**`https://example.com/questions?id=1`

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
| topicTags  | Json(Array) | 是       | 题目的标签，中文形式                                         |



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
        "topicTags": [
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




## 提交题解(完成)

> 提交题解到后端，并返回唯一的提交流水号

**接口说明：**请求参数使用JSON格式

**请求方法：**POST

**URL示例：**`https://example.com/answers/submit`



**请求参数：**

| 参数     | 类型   | 是否必填 | 描述                                                         |
| -------- | ------ | -------- | ------------------------------------------------------------ |
| id       | Int    | 是       | 要提交的题目号                                               |
| answer   | string | 是       | 题解内容                                                     |
| language | Int    | 是       | 使用的语言类型，具体类型参考[语言类型参照表](/docs/languagetypes) |



**返回结果（JSON）**

| 参数   | 类型   | 是否必填 | 描述                     |
| ------ | ------ | -------- | ------------------------ |
| status | Int    | 是       | 错误码                   |
| msg    | String | 是       | 错误信息                 |
| data   | Json   | 否       | 提交详情，响应成功时返回 |



**提交详情（JSON)**

| 参数         | 类型   | 是否必填 | 描述                             |
| ------------ | ------ | -------- | -------------------------------- |
| submissionId | String | 是       | 提交流水号，用于查询本次答题结果 |



**请求示例代码（JavaScript）**

```javascript
var myHeaders = new Headers();
myHeaders.append("Content-Type", "application/json");

var raw = JSON.stringify({"id":1,"answer":"print(\"hello,world!\")","language":3});

var requestOptions = {
  method: 'POST',
  headers: myHeaders,
  body: raw,
  redirect: 'follow'
};

fetch("https://example.com/answers/submit", requestOptions)
  .then(response => response.text())
  .then(result => console.log(result))
  .catch(error => console.log('error', error));
```



**响应示例**

```json
{
    "status": 0,
    "msg": "",
    "data": {
        "submissionId":"10001"
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





## 获取判题结果(完成)

> 通过提交流水号获取判题结果

**接口说明：**`id`是提交题目的流水号，在URL中直接作为参数拼接

**请求方法：**GET

**URL示例：**`https://example.com/judgement?id=1`

**返回结果（JSON）**

| 参数   | 类型   | 是否必填 | 描述                                       |
| ------ | ------ | -------- | ------------------------------------------ |
| status | Int    | 是       | 错误码(此处会出现特殊错误码-2，详见错误码) |
| msg    | String | 是       | 错误信息                                   |
| data   | Json   | 否       | 判题结果                                   |



**判题结果**

| 参数           | 类型   | 是否必填 | 描述                                                         |
| -------------- | ------ | -------- | ------------------------------------------------------------ |
| id             | String | 是       | 提交题目流水号                                               |
| result         | Int    | 是       | 提交结果枚举，(0/1/2/3/4/5对应AC/WA/CE/RE/TLE/MLE)[^1]       |
| time           | String | 是       | 花费时间，字符串形式，可以直接显示在前端，如("80 ms"，"N/A"等) |
| memory         | String | 是       | 使用内存，花费时间，字符串形式，可以直接显示在前端，如("37.9 MB"，"N/A"等) |
| language       | int    | 是       | 使用的语言类型，具体类型参考[语言类型参照表](/docs/languagetypes) |
| lastTestCase   | String | 否       | 最后一个测试用例的内容，目前除AC和CE以外，此字段会有内容     |
| expectedOutput | String | 否       | 最后一个测试用例期望输出的结果，目前除AC和CE以外，此字段会有内容 |
| totalCorrect   | int    | 否       | 通过的测试用例数，目前除CE以外，此字段会有内容               |
| totalTestCases | int    | 否       | 总共的测试用例数，目前除CE以外，此字段会有内容               |
| error          | String | 否       | 错误信息，目前当出现RE，CE时此字段会有内容                   |
| errorDetail    | String | 否       | 错误详情，目前当出现RE，CE时候会有内容                       |



**响应示例**

```json
{
  "status": 0,
  "msg": "",
  "data": {
    "id": "100000001",
    "result": 3,
    "time": "N/A",
    "memory": "N/A",
    "language": 3,
    "lastTestCase": "[2,7,11,15]\n9",
    "expectedOutput": "[0,1]",
    "totalCorrect": 0,
    "totalTestCases": 52,
    "error": "Line 3: NameError: name 'pring' is not defined",
    "errorDetail": "NameError: name 'pring' is not defined\n    pring(hello)\nLine 3 in twoSum (Solution.py)\n    ret = Solution().twoSum(param_1, param_2)\nLine 29 in _driver (Solution.py)\n    _driver()\nLine 40 in <module> (Solution.py)"
  }
}
```

**错误示例**

```json
{
    "status": -2,
    "msg": "正在判题中，请稍后再试"
}
```









[^1]:Accepted (AC), Presentation Error (PE) ,Wrong Answer (WA),Runtime Error (RE),Time Limit Exceeded (TLE) ,Memory Limit Exceeded (MLE) ,Output Limit Exceeded (OLE),Compilation Error (CE) ,Restricted Function (RF),Internal Error (IE)