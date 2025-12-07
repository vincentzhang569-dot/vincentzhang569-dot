# 🏭 Industrial AI Brain v2.0 | 工业智脑综合管理平台

[![Streamlit App](https://static.streamlit.io/badges/streamlit_badge_black_white.svg)](https://your-app-url.streamlit.app)
![Python](https://img.shields.io/badge/Python-3.10%2B-blue)
![AI Model](https://img.shields.io/badge/Model-Qwen2.5--Coder%20%7C%20Qwen--VL-violet)
![Framework](https://img.shields.io/badge/Framework-Streamlit-orange)
![License](https://img.shields.io/badge/License-MIT-green)

> **一个基于 LLM Agent 的工业 4.0 边缘侧综合解决方案：把多模态故障诊断、IoT 实时大屏、自然语言设备控制统一在一个“工业大脑”里。适合部署在工厂中控室、产线长办公电脑或运维工程师平板上。**

---

## 📺 核心功能概览 (Feature Overview)

### 1. 🚑 智能故障诊断 (Intelligent Diagnosis)

基于 **Qwen-VL 系列视觉大模型 + RAG 文档问答**：

- **看图就能诊断**：上传设备报警界面 / 现场照片，AI 自动识别：
  - 报警代码 / 报错信息
  - 关键 UI 元素（温度、转速、状态灯等）
- **专家级思维链报告**：内置“资深维修工程师”风格 Prompt，输出结构化诊断结果：
  - 「故障现象 → 根因分析 → 排查步骤 → 安全警示」
- **文档级知识库问答**：
  - 支持上传维修手册 / 说明书（PDF 等）
  - 基于 RAG 的“段落级精确问答”，可追溯到原文位置，方便审核与交接

> 目标：让一线班组长也能拿到接近“20 年经验工程师”的故障分析结论。

---

### 2. 📊 IoT 预测性维护大屏 (Predictive Maintenance Dashboard)

基于 **Plotly + Streamlit** 的高互动可视化：

- **实时监控视图**  
  - 模拟 10 台工业机器人/设备的 **温度、振动、负载、运行状态** 数据流  
  - 支持按设备、时间区间、指标类型筛选
- **异常检测与预警**  
  - 支持阈值告警（如温度 > 75°C 自动高亮）  
  - 图表中对异常点做标记，方便追溯
- **高性能数据管线**  
  - 使用 `@st.cache_data` 对历史数据与特征工程结果进行缓存  
  - 秒级加载大屏，适配多用户同时访问

> 当前 Demo 使用合成数据，架构设计上可无缝替换为 OPC-UA / MQTT / 时序数据库等工业数据源。

---

### 3. 🎮 AI 指挥官 (Agentic Controller) — **核心亮点**

基于 **Function Calling / 工具调用** 的智能体工作流引擎：

- **自然语言控制设备**  
  - 输入「1 号机过热，先降负载到 60%，如果还超 75°C 就停机」  
  - AI 解析为结构化指令 → 下发给内部 `RobotController` 模块
- **一键宏指令**  
  - 支持封装「一键启动整线 / 平滑停机 / 夜班节能模式」等复合逻辑  
  - 方便班组长和调度员使用
- **鲁棒性与安全设计**  
  - 严格的 JSON 解析与参数校验：  
    - 自动纠正温度单位（℃ / ℉）、设备 ID 书写错误等  
    - 对不安全指令（如直接高负载启动长期停机设备）进行拦截与二次确认
  - 为接入真实 PLC / MES / SCADA 预留接口层（目前为模拟执行层）

> 这个模块是将 LLM 变成“生产指挥官”的关键，而不仅仅是一个聊天机器人。

---

## 🧩 系统架构 (System Architecture)

从“老板视角”到“工程师视角”的整体设计如下：

```text
[Operator / Engineer]
        │  自然语言 & 图片
        ▼
 ┌──────────────────────┐
 │   Streamlit Web UI   │  ← 多页面：故障诊断 / IoT 大屏 / AI 指挥官
 └──────────────────────┘
        │  调用
        ▼
 ┌────────────────────────────┐
 │   LLM Agent Orchestrator   │
 │      (Qwen2.5 / Qwen-VL)   │
 └────────────────────────────┘
   │          │           │
   │          │           │
   ▼          ▼           ▼
[Vision Tool] [RAG 工具]  [Control Tool]
   │          │           │
设备图片   维修手册库      RobotController
              │
              ▼
          知识检索/回答
多模态入口：文本 + 图片输入统一到 Agent 层处理

工具化能力：

vision_tool：处理图片理解与故障识别

rag_tool：面向文档的检索与问答

control_tool：将自然语言转成结构化设备控制指令

边缘侧友好：全部基于 Python / Streamlit，可部署在工控机、工业 PC 或本地服务器

🛠️ 技术栈 (Tech Stack)

Frontend

Streamlit 原生多页面导航

自定义 CSS 注入，适配移动端与中控室大屏

LLM Core

OpenAI SDK 协议兼容客户端（可对接 SiliconFlow 等国产模型服务）

Vision: Qwen-VL-Max / Qwen2-VL-72B

Agent: Qwen2.5-Coder 系列（强化 JSON / Function Calling 输出）

Data & Analytics

pandas, numpy 用于合成与处理设备运行数据

指标计算 / 特征工程可扩展至预测性维护算法（如剩余寿命估计 RUL）

Visualization

Plotly 交互式图表（折线图、散点图、告警点标注等）

Backend Logic

基于 Python Class 的状态管理：RobotController 等

清晰区分：

LLM 推理层

业务策略层

设备控制/模拟层

🚀 快速开始 (Quick Start)
1. 克隆仓库
git clone https://github.com/your-username/my-ai-brain.git
cd my-ai-brain

2. 安装依赖
pip install -r requirements.txt

3. 配置密钥

在项目根目录创建 .streamlit/secrets.toml：

SILICONFLOW_API_KEY = "sk-xxxxxxxxxxxx"


如使用其他 OpenAI 协议兼容服务，可在代码中切换 Base URL 与 Model 名称。

4. 启动平台
streamlit run main.py


启动后将自动在浏览器中打开 Web 界面。

📱 移动端与中控大屏适配 (Mobile & Control Room Ready)

本项目针对 竖屏平板 / 手机 与 中控室大屏 做了样式优化：

隐藏式导航栏：重写 Streamlit Header，最大化业务区域展示面积

卡片式设备布局：使用 Flexbox，使设备信息在窄屏自动换行堆叠

深色主题：全站 Dark Mode，更符合中控室、夜班环境，降低视觉疲劳

🏭 典型工业 4.0 场景 (Use Cases)

场景 1：班组长夜班值守

上传报警照片 → AI 给出初步诊断与排查建议

一键生成标准化故障处理记录，方便交接与留档

场景 2：设备管理部周例会

打开 IoT 大屏 → 回看一周关键设备的温度 / 振动异常

快速筛出“需要重点关注”的设备，形成维护计划

场景 3：IT / 自动化工程师二次开发

通过 Agent Controller 接口接入现有 MES / SCADA 系统

将自然语言控制能力嵌入已有中控平台 UI 中

📂 项目结构 (Project Structure)

示意结构，具体可按实际代码调整。

my-ai-brain/
├── main.py                # Streamlit 入口，多页面路由
├── pages/
│   ├── 1_🩺_故障诊断.py
│   ├── 2_📊_IoT_大屏.py
│   └── 3_🎮_AI_指挥官.py
├── core/
│   ├── agents.py          # Agent 工作流 & Function Calling
│   ├── controller.py      # RobotController 等业务逻辑
│   ├── vision.py          # Qwen-VL 调用封装
│   └── rag.py             # 文档解析与检索问答
├── data/
│   └── demo_sensors.csv   # 演示用合成数据
├── requirements.txt
└── README.md

🧭 Roadmap

 支持真实工业协议接入（OPC-UA / MQTT / Modbus 等）

 引入简单预测模型，实现基于时间序列的剩余寿命预测（RUL）

 增加账户体系与操作日志审计，方便企业内部上线

 集成多工厂 / 多产线切换能力

 提供 Docker 镜像与一键部署脚本

🤝 企业合作 & 二次开发 (For Enterprise & Integrators)

如果你是：

工厂设备管理 / 智能制造负责人

工业软件集成商 / SI

想做“从 0 到 1 工业 AI 应用”的技术团队

可以基于本项目做：

私有化部署与模型本地化（内网大模型 / 自训练模型接入）

接入现有的 PLC / MES / SCADA / EAM 系统

定制化的安全策略与审批流（如高风险操作二次确认）

👨‍💻 Author

Vincent Zhang
Focus on Industrial AI Application & Agentic Workflow.
欢迎通过 Issue / PR / Email 交流工业场景落地与二次开发合作。
