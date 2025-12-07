### Hi there, I'm Vincent Zhang! 👋

**🏭 Industrial AI Brain v2.0 | 工业智脑综合管理平台**

**一个基于 LLM Agent 的工业 4.0 边缘侧综合解决方案。集成了多模态故障诊断、IoT 数据实时大屏与自然语言设备控制中枢。**

Full-stack AI application engineer focusing on building agentic, multimodal and data-intensive applications on top of LLMs for real-world industrial scenarios.

---

#### 🛠️ Tech Stack | 技术栈
*   **Frontend**: Streamlit (Native Navigation, Custom CSS injection for Mobile-First design)
*   **LLM Core**: OpenAI SDK (Compatible with SiliconFlow API)
    *   *Vision*: Qwen-VL-Max / Qwen2-VL-72B
    *   *Agent*: Qwen2.5-Coder-32B-Instruct (Optimized for JSON output)
*   **Data Engineering**: Pandas, NumPy (Synthetic Data Generation)
*   **Visualization**: Plotly Interactive Charts
*   **Backend Logic**: Python Class-based State Management (`RobotController`)
---

#### 🏆 Featured Project | 代表作

**🏭 Industrial AI Brain v2.0 | 工业智脑综合管理平台**

[🔗 **View Project Source Code / 点击查看项目代码**](https://github.com/vincentzhang569-dot/my-ai-brain)
---

## 📺 核心功能演示 (Features)

### 1. 🚑 智能故障诊断 (Intelligent Diagnosis)
基于 **Qwen2-VL** 视觉大模型与 RAG 技术。
*   **看图说话**：直接上传报错屏幕/设备照片，AI 自动识别故障代码。
*   **专家思维链**：内置 20 年经验专家 Prompt，输出“根因分析-排查步骤-安全警示”标准化报告。
*   **文档知识库**：支持上传维修手册 (PDF)，进行基于文档的精准问答。

### 2. 📊 IoT 预测性维护大屏 (Predictive Maintenance Dashboard)
基于 **Plotly** 与 **Streamlit** 的高性能数据可视化。
*   **实时监控**：模拟 10 台工业机器人的温度、震动、负载数据流。
*   **故障预警**：自动检测异常阈值（如温度 > 75°C），在图表中高亮显示。
*   **高性能架构**：采用 `@st.cache_data` 实现数据缓存，秒级加载。

### 3. 🎮 AI 指挥官 (Agentic Controller) - **核心亮点**
基于 **Function Calling (工具调用)** 的智能体工作流。
*   **自然语言控制**：输入“1号机过热，立马停机”，AI 自动解析意图。
*   **一键宏指令**：支持“一键启动”、“全线停机”等复杂逻辑原子化封装。
*   **鲁棒性设计**：内置 JSON 强力解析引擎与参数清洗机制，确保指令执行 100% 成功率。
---

#### 📫 Connect with me | 联系我
*   **Focus**: Industrial AI Application & Agentic Workflow
*   **Email**: *vincentzhang569@gmail.com]*
