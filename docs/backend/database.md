---
layout: default
title: 数据实体设计
parent: 后端文档
nav_order: 1
---

# 数据实体设计
{: .no_toc }

## 数据表名称
{: .no_toc .text-delta }

1. TOC
{:toc}

---

## 题目信息表(qmoj_question)

> 用来容纳题目信息

| 数据库字段名             | 类型         | 描述                                                |
| ------------------------ | ------------ | --------------------------------------------------- |
| id                       | bigint       | 自增主键                                            |
| question_id              | int          | 平台问题的ID(单平台唯一)                            |
| content                  | text         | 题目的内容，中文简体(默认)                          |
| title                    | varchar(255) | 题目的标题，中文简体(默认)                          |
| difficulty               | tinyint      | 分别有：easy(1)：简单；medium：中等(2)；hard：难(3) |
| lang_to_valid_playground | json         | 题目允许提交的语言类型                              |
| create_time              | datetime     | 创建时间                                            |
| modify_time              | datetime     | 修改时间                                            |
| platform                 | tinyint      | 题目来源平台                                        |
| question_slug            | varchar(255) | 题目slug(题目标识符，例如leetcode第一道题为two-sum) |



