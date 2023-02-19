# chatgpt_plus_python_api
用于ChatGPT Plus的Python调用API，实现新开对话和连续对话。

## 准备

你应该先登录[ChatGPT Website](https://chat.openai.com/chat)，找到名为`cf_clearance`、`__Secure-next-auth.session-token`、`_puid`的Cookies，复制它们的值。

其中`_puid`为Plus会员专属值，没它不行。

## 安装依赖

``` bash
pip install requests
```

## 快速开始

1. 在`chatgpt.py`代码相应位置粘贴`cf_clearance`、`session_token`、`_puid`的值。

2. 发送新会话窗口消息
  ``` python
  from chatgpt import send_new_message

  text,conversation_id = send_new_message("你是谁？")
  ```

3. 发送连续对话消息
  ``` python
  from chatgpt import send_message

  conversation_id = "60ccf5ba-8e12-4cb9-8700-44d7a2579e93"
  text = send_message("今天是多少号？", conversation_id)
  ```

4. 新开会话窗口+连续对话
  ``` python
  from chatgpt import send_new_message,send_message
  
  text,conversation_id = send_new_message("你是谁？")
  text = send_message("我刚刚问你什么问题？", conversation_id)
  ```

## 注意事项

1. 官方限制接口同一时间只能发送一条信息，所以做不了并发，同时发送会返回429状态码，程序已做等待20秒重试处理。
  `一次只有一条消息。 在发送另一条消息之前，请等待任何其他响应完成，或者等待一分钟。`

2. 原则上只能Plus会员账号调用，免费账号会有CF验证。
