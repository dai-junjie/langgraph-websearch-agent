# LangGraph 网络搜索代理

这个项目实现了一个使用 LangGraph 的智能网络搜索代理，旨在通过生成搜索查询、收集结果并反思收集到的信息来执行迭代研究，以确定是否需要额外的搜索。

## 功能特点

- **智能查询生成**：根据研究主题自动生成相关搜索查询
- **迭代研究过程**：执行多次搜索循环直到收集到足够的信息
- **反思机制**：评估收集到的信息以确定是否需要更多研究
- **结构化输出**：提供格式良好的答案并包含来源引用

## 工作原理

代理遵循循环过程：
1. **查询生成**：根据研究主题创建搜索查询
2. **网络搜索**：使用 Tavily 搜索 API 执行搜索
3. **反思**：评估收集到的信息是否足够
4. **决策**：要么生成后续查询以进行额外研究，要么提供最终答案

## 代理工作流程

![代理工作流程](./assert/graph.png)

上图展示了 LangGraph 网络搜索代理的完整工作流程，显示了查询如何生成、执行并通过多次研究循环进行优化。

## 前提条件

- Python 3.8+
- 所需环境变量：
  - `LLM_BASE_URL`：LLM API 的基础 URL
  - `LLM_API_KEY`：LLM 服务的 API 密钥
  - `TAVILY_API_KEY`：Tavily 搜索服务的 API 密钥

## 安装

1. 安装所需包：
   ```bash
   pip install langchain langgraph langchain-openai langchain-tavily
   ```

2. 设置环境变量：
   ```bash
   export LLM_BASE_URL="your_llm_base_url"
   export LLM_API_KEY="your_llm_api_key"
   export TAVILY_API_KEY="your_tavily_api_key"
   ```

## 使用方法

使用研究主题运行代理：
```python
from graph import graph

initial_state = {
    "messages": "什么是 LangGraph？",
    "search_query_count": 1,
    "max_research_loops": 2
}

for event in graph.stream(initial_state):
    print(event)
```

## 项目结构

- `graph.py`：LangGraph 代理的主要实现
- `prompt.py`：用于查询生成、反思和答案格式化的系统提示
- `util.py`：处理研究主题的实用函数

## 配置

可以调整的关键参数：
- `search_query_count`：要生成的初始搜索查询数量
- `max_research_loops`：要执行的最大研究循环次数

## 依赖项

- langchain
- langgraph
- langchain-openai
- langchain-tavily
- pydantic