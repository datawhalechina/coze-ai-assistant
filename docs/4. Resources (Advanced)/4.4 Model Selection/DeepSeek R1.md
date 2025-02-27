# Coze接入DeepSeek R1

## 前言

DeepSeek-R1是**深度求索（DeepSeek）于2025年1月20日发布的人工智能大型语言模型**，专门适用于数学、编码和逻辑等任务，性能对标OpenAI o1。

我们目前有三种Coze接入DeepSeek R1的方法，插件两种（分别是自定义插件与使用外部API）、官方火山引擎接入一种
## 插件接入DeepSeek R1

### 自定义插件

![](Pasted image 20250217222156.png)

输入插件名称（DeepSeek R1）、插件描述（插件接入DeepSeek R1）、方式选择（云侧插件 - 在 Coze IDE 中创建）、IDE选择（Node.js）。
![](attachmentss/Pasted image 20250217222801.png)

在进入插件详情页创建工具

输入工具名称（DeepSeek_R1）和工具介绍（DeepSeek R1 模型调用）。

![](attachmentss/Pasted image 20250217223200.png)


然后开始动手是现实下DeepSeek推理模型的接入  

编写调用代码

```
// 引用依赖包
import OpenAI from "openai";

export async function handler({ input, logger }) {
  // 定义请求地址
  const API_URL = 'https://api.deepseek.com';
  
  // 从新的输入结构中获取API密钥、模型名称和消息内容
  const API_KEY = input.APIKey;
  const MODEL_NAME = input.model;
  const USER_MESSAGE = input.messages;

  // 构建初始化参数
  const openai = new OpenAI({
    baseURL: API_URL,
    apiKey: API_KEY
  });

  // 发送请求
  const completion = await openai.chat.completions.create({
    messages: [{ role: "user", content: USER_MESSAGE }],
    model: MODEL_NAME,
  });

  console.log(completion);

  // 返回参数
  return {
    data: {
      'reasoning_content': completion.choices[0].message.reasoning_content,
      'content': completion.choices[0].message.content
    }
  };
}
```

![](attachmentss/Pasted image 20250217224431.png)

点击左下角依赖包添加`openai`查找添加
![](attachmentss/Pasted image 20250217224632.png)

切换到元数据添加输入参数和输出参数
- 新建三个输入参数，下面分别是名称、描述
	- APIKey——`密钥`
	- model——`模型型号`
	- messages——`用户提示词`
	
- 返回参数
	- data——`输出内容`
		- reasoning_content——`思维链内容`
		- content——`最终回答内容`


测试代码

在测试之前我们先要获取密钥（key）

前往API 密钥地址： https://platform.deepseek.com/api_keys

创建API key

![](attachmentss/Pasted image 20250217223517.png)

点击输入的自动生成，填写密钥、模型和提示词


我自己的DeepSeek没有钱，到时候再补

![](attachmentss/Pasted image 20250217230820.png)

发布

## Coze官方火山引擎接入