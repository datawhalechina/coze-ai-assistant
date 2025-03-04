# 3.2 智能体基础设置

## 3.2.1 智能体的模式

大家新建一个智能体的时候，可以在选择模式的地方发现，有三个选项
![](attachments/Pasted image 20250124154439.png)

我们来看看分别是：
1. 单Agent (LLM模式)
2. 单Agent (对话流模式)
3. 多Agents

在本章节，我们主要说一下**单Agent**的LLM模式；第2个对话流模式，放在第五章节；第3个多Agnets 比较复杂，但是逻辑和工作流较想，所以目前没有打算专门做一个章节讲解，可以[[docs/11. Case Library/Case Library/Werewolf Game|参考“狼人杀案例”学习（点击跳转）]]。

### 3.2.1.1 单 Agent 模式概述

### 3.2.1.2 对话流模式概述
对话流模式适用于智能体技能流程相对固定的场景，例如售后服务场景下指定某个对话流处理咨询问题、长文生成场景下根据用户的每个 query分段生成内容。

**对话流模式介绍**

通常情况下，我们通过人设与回复逻辑来指定智能体在不同场景下的不同技能，例如约束智能体使用指定插件回复某类问题，但用户 Query 复杂的情况下，智能体不一定会根据设计的逻辑进行处理，导致智能体回复不符合预期。

此时你可以将智能体设置为对话流模式。在该模式下无需设置人设与回复逻辑，智能体有且只有一个对话流，智能体用户的所有对话均会触发此对话流处理。智能体通过开始节点的 USER_INPUT 传入问题，并以结束节点作为智能体的回复。

对话流适用于 Chatbot 等需要在响应对话请求时进行复杂逻辑处理的对话式应用程序，例如智能客服、虚拟伴侣等。

**限制说明**

- 对话流模式的智能体只能绑定一个对话流，且对话流开始节点未添加 USER_INPUT 外的其他变量。
- 对话流模式的智能体不支持添加技能、知识等配置，但你可以将某些技能和知识配置在智能体的对话流中，例如对话流中添加知识库处理节点。
### 3.2.1.3 多 Agent 模式概述
您可以通过多 Agent 模式搭建功能更加全面和复杂的 AI智能体。

在扣子中创建智能体后，智能体默认使用单 Agent 模式。在单 Agent 模式下处理复杂任务时，您必须编写非常详细和冗长的提示词，而且您可能需要添加各种插件和工作流等，这增加了调试智能体的复杂性。调试时任何一处细节改动，都有可能影响到智能体的整体功能，实际处理用户任务时，处理结果可能与预期效果有较大出入。

为了解决上述问题，扣子提供了多 Agent 模式，该模式下您可以为智能体添加多个 Agent，并连接、配置各个 Agent 节点，通过多节点之间的分工协作来高效解决复杂的用户任务。

多 Agent 模式通过以下方式来简化复杂的任务场景。

- 您可以为不同的 Agent 配置独立的提示词，将复杂任务分解为一组简单任务，而不是在一个智能体的提示词中设置处理任务所需的所有判断条件和使用限制。
- 多 Agent 模式允许您为每个 Agent 节点配置独立的插件和工作流。这不仅降低了单个 Agent 的复杂性，还提高了测试智能体时 bug 修复的效率和准确性，您只需要修改发生错误的 Agent 配置即可。


**工作流和多 Agent 模式有什么区别？**

- 工作流是一种以低代码方式开发插件的方法。您可以将各种节点添加到工作流中，并像为智能体添加插件一样，添加并使用工作流。
- 多 Agent 模式允许您通过将不同的人物设定分配给不同的 Agent 来扩展智能体的功能。用户与一个 Agent 交谈时，当用户输入的内容满足跳转条件时，对话将移交给另一个 Agent 进行处理。多 Agent 模式更适合处理复杂的任务。

**更多学习教程参考**

[官方文档：多 Agent 模式](https://www.coze.cn/docs/guides/multiagent) 
https://www.Coze.cn/docs/guides/multiagent 

[使用Coze的muilt-agent驯服GPT-4](https://mp.weixin.qq.com/s/sjRFE44cjBfn4p3_3vv4vg) 
https://mp.weixin.qq.com/s/sjRFE44cjBfn4p3_3vv4vg 

[Multi-agent mode实践 | 用Coze手捏一个Bot](https://mp.weixin.qq.com/s/YV7M7othSzMjKpm8xNHU-w) 
https://mp.weixin.qq.com/s/YV7M7othSzMjKpm8xNHU-w 

[视频：分享一个在Coze上做提示词工程以及设计多智能体应用的最佳实践案例](https://www.bilibili.com/video/BV1MC411h7ok/) 
https://www.bilibili.com/video/BV1MC411h7ok/ 

[视频：【Agent共学第二期】Kai分享 | 一百个字搭谁是卧底-多Agent](https://www.bilibili.com/video/BV1Ew4m1S7eq) 
https://www.bilibili.com/video/BV1Ew4m1S7eq/

## 3.2.2 提示词

提示词是一种自然语言指令，它为大语言模型（LLM）提供任务指导。搭建智能体的第一步就是设置提示词，你可以根据业务需要直接编写提示词，也可以使用提示词模版、引用提示词资源或通过 AI 自动生成提示词。​

### 3.2.2.1 直接编写提示词​

你可以根据业务需要编写提示词，提示词编写得越清晰明确，智能体的回复也会越符合预期。关于如何编写提示词，请参考​编写提示词。​

1. 登录[扣子平台](https://www.coze.cn/)。​

2. 在左侧导航栏中选择工作空间，并在页面顶部空间列表中选择个人空间或团队空间。​

	系统默认创建了一个个人空间，该空间内创建的资源例如智能体、插件、知识库是你的私有资源，其他用户不可见。你也可以创建团队或加入其他团队，团队内的资源可以和其他团队成员共享。更多信息，请参考​管理团队。​

3. 在所选空间中，单击目标智能体或创建一个新智能体。​

4. 在人设与回复逻辑面板中编写提示词。
![](attachments/Pasted image 20250124203526.png)

### 3.2.2.2 使用提示词模版​

扣子根据不同的业务场景提供了多套提示词模版，你可以直接使用模版，或参考模版编写提示词。​

1. 在人设与回复逻辑面板的右下角，单击提示词库。
![](attachments/Pasted image 20250124203631.png)

2. 在**推荐**页签下，选择系统推荐的提示词模版，然后单击**插入提示词**。
![](attachments/Pasted image 20250124203644.png)

使用提示词后，系统会将选择的提示词自动填充到提示词的编辑框中，你可以基于自己的业务场景修改提示词。修改提示词时，你需要重点关注提示词中的高亮部分。

- 添加文本：如果提示词中包含编辑块，你需要根据编辑块的空白引导添加文本内容。

![](attachments/Pasted image 20250124203657.png)

- 添加技能：如果提示词中引用了技能，你需要添加或替换为当前智能体或工作流中已经配置的技能，以确保技能可用。
![](attachments/Pasted image 20250124203705.png)

### 3.2.2.2 引用提示词资源

提示词可以作为资源保存在资源库中，供团队内的其他成员引用。引用提示词资源前，请确保资源库中已经创建了提示词，详情可参考[创建提示词](https://www.coze.cn/open/docs/guides/management_prompt#0a99aebe) 。

>如果引用的提示词中包含了插件、工作流、图像流资源，而智能体中未配置该资源，引用提示词后，提示词中资源块名称会显示为灰色。此时，大模型不会调用对应资源，为智能体添加资源后，大模型方可按照提示词指令正常执行。


1. 在**人设与回复逻辑**面板的右下角，单击**提示词库**。

![](attachments/Pasted image 20250124205936.png)

2. 在**团队**页签下，选择团队空间内的提示词资源，然后单击**插入提示词**。
![](attachments/Pasted image 20250124210001.png)

使用提示词后，系统会将选择的提示词自动填充到提示词的编辑框中，你可以基于自己的业务场景修改提示词。修改提示词时，你需要重点关注提示词中的高亮部分。

- 添加文本：如果提示词中包含编辑块，你需要根据编辑块的空白引导添加文本内容。
![](attachments/Pasted image 20250124210012.png)

- 添加技能：如果提示词中引用了技能，你需要添加或替换为当前智能体或工作流中已经配置的技能，以确保技能可用。
![](attachments/Pasted image 20250124210021.png)

### 3.2.2.3 AI 生成提示词

你可以通过自然语言告诉 AI 你希望编写或优化的提示词，大语言模型会根据你的描述，自动生成提示词；你也可以根据调试结果，告诉大语言模型提示词哪里不符合预期以及你的预期效果，大语言模型会自动帮你完成优化。

1. 在**人设与回复逻辑**面板的右上角，单击**优化**。
![](attachments/Pasted image 20250124220912.png)

2. 输入你希望编写或优化的提示词，单击发送图标，AI 会根据你的描述自动生成提示词。

	如果你的智能体已完成调试，你可以单击**根据调试结果优化**，然后输入哪里不符合预期以及你的预期效果，大语言模型会自动帮你完成优化。

![](attachments/Pasted image 20250124220942.png)

3. 单击**替换**，AI 生成的提示词会自动填充到提示词编辑框中。

	你也可以对 AI 生成的提示词执行以下操作：

	- **退出**：关闭 AI 生成的页面。
	- **复制**：复制 AI 生成的提示词。
	- **重新生成**：如果你对 AI 生成的提示词不满意或想要尝试不同的结果，可以单击重新生成图标，AI 会再次根据你的输入生成新提示词。
	- **点赞**：如果 AI 生成的提示词符合你的期望或对你有帮助，可以单击点赞图标，来给予正面反馈。
	- **点踩**：如果 AI 生成的提示词不满足你的需求，可以单击点踩图标，然后选择不满意的原因，帮助 AI 学习并改进未来的输出。

![](attachments/Pasted image 20250124221024.png)





## 3.2.3 整体页面


### 3.2.3.1 单 Agent 模式布局页面
![](attachments/Pasted image 20250124221227.png)

我们可以看到**单 Agent 模式**下，我们整个页面分为上下两个部分，上面一部分内容较少，主要是当前编辑的介绍和一些选项；下面一部分东西较多，可以分为三栏，分别是“人设与回复逻辑”、“技能”、“预览与调试”。

