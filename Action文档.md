# Action 生成器 - action_0001

## 概述

动作生成器 `action_0001` 是一个用于处理信息并根据用户的需求发送消息的工具。它支持通过不同的平台发送消息，如邮件或即时消息平台。

**版本:** 0.0.1

## 输入参数

- **ActionType**: 指定发送消息的类型。这可以是邮件发送或即时消息发送。
- **Platform**: 指定发送消息的平台。这取决于ActionType的选择，可以是微信、电子邮件等。
- **Content**: 要发送的消息内容。

## 输出参数

- **status**: 表明动作执行的结果，可能的值为 "success" 或 "fail"。
- **type**: 输出的数据类型，通常是一个字符串，表示操作的结果。

## 模板

动作生成器包含以下模板，用于处理不同类型的消息发送：

### 微信消息模板

- **actionType**: "message"
- **platform**: "wechat"
- **content**: "{input.Content}"
- **to**: 接收消息的用户列表，如 ["user1", "user2"]
- **mention**: 需要在消息中提及的用户列表
- **at_all**: 是否@所有人

### 邮件发送模板

- **actionType**: "email"
- **content**: "{input.Content}"
- **subject**: 邮件主题（从内容中推测）
- **attachment**: 邮件附件列表，包括文件名、路径和类型
- **from**: 发送者的邮件地址列表
- **cc**: 抄送给的邮件地址列表
- **to**: 接收者的邮件地址列表


``` json
{
    "generator_id": "action_0001",
    "type": "action",
    "description": "通过Processor 得到处理的信息并发送给用户", # optional
    "version": "0.0.1", # optional
    "input": [
        {
            "name": "ActionType", # 邮件或者是发送消息
            "description": "选择发送消息方式"
        },
        {
            "name": "Platform",
            "description": "选择发送消息平台"
        },
        {
            "name": "Content",
            "description": "消息内容"
        }
    ],
    "output": [
        {
            "status": "success", # success or fail
            "type": "string"
        },
    ],
    "template": [
        {
            "actionType": "message",
            "platform": "wechat",
            "content": "{input.Content}",
            "to": [
                "user1",
                "user2"
            ],
            "mention": [
                "user1",
                "user2"
            ],
            "at_all": false,
        },
        {
            "actionType": "message",
            "platform": "wechat",
            "content": "{input.Content}",
            "to": [
                "user1",
                "user2"
            ],
            "mention": [
                "user1",
                "user2"
            ],
            "at_all": false,
        },
        {
            "actionType": "email",
            "content": "{input.Content}",
            "subject": "", # guess from the content
            "attachment": [
                {
                    "file_name": "file1",
                    "file_path": "file1_path",
                    "file_type": "file1_type"
                },
                {
                    "file_name": "file2",
                    "file_path": "file2_path",
                    "file_type": "file2_type"
                }
            ],
            "from": [
                "user1", #email address
            ],
            "cc": [
                "user1", #email address
                "user2" #email address
            ],
            "to": [
                "user1", #email address
                "user2" #email address
            ],
        }
    ]
}
```