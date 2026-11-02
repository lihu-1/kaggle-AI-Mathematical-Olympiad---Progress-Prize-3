# AIMO Progress Prize 3 推理方案

## 任务与入口

针对数学竞赛题生成整数答案。推理入口为 [aimo-3-gpt-oss-120b-with-tools.ipynb](aimo-3-gpt-oss-120b-with-tools.ipynb)，通过 Kaggle AIMO 3 inference server 接收题目并返回 id 与 answer。

## 方法

1. 从 Kaggle 输入加载 GPT-OSS 120B 权重，并启动模型服务；notebook 设置 65,536 token 上下文和 temperature 1.0。
2. 通过提示词要求模型分析题意、探索解法、逐步求解并检查结果，以 boxed 格式输出 0–99999 的非负整数。
3. 推理过程中可调用本地 Python 工具进行计算或符号验证；模型根据工具返回继续生成。
4. 从生成文本提取答案，对多次生成结果进行投票和加权选择，再交给比赛推理接口。

## 运行与依赖

在 Kaggle 中打开 notebook，挂载比赛数据、`gpt-oss-120b/transformers/default/1` 模型和 `aimo-3-utils` 离线依赖包，按单元格顺序运行。模型规模较大，需要与 notebook 配置相符的 GPU 资源。正式评分使用 inference server；本地网关路径供调试。

本仓库只包含推理 notebook，不包含模型权重或离线依赖。运行环境、时间预算和模型路径变化均可能影响复现。当前说明依据代码整理，未重新执行或验证比赛成绩。
