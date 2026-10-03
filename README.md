<div align="center">
  <h1>🌌 运气的形状 (The Shape of AGI)</h1>
  <p><b>一部关于算力、概率与硅基进化的视觉编年史</b></p>
  <p>✨ <i>Interactive Canvas Animation · 60FPS · Zero Dependencies (except GSAP)</i> ✨</p>
</div>

---

## 📖 项目概述 (Overview)
本项目是一个全屏沉浸式的交互网页大秀，旨在通过纯前端（HTML5 Canvas 2D + GSAP）的技术手段，将大语言模型（LLM）的演进史进行高度视觉化的呈现。从最底层的逻辑门，到 Word2Vec 的高维空间，再到混合专家架构（MoE）与 GPT-6 Astra 的终极推演，全程以**数学方程和粒子物理**驱动，力求打造出干货满满且极具电影级质感的知识科普大赏。

## 💡 核心视效与底层算法 (Core Algorithms)

为了在 60fps 下保持丝滑的性能，本作没有使用繁重的 WebGL/Three.js 框架，而是完全基于底层 Canvas API 构建了一套轻量级的数学粒子引擎。

*   **词向量的高维坍缩 (Word Embeddings)**：通过多向引力计算，模拟词汇在数百维语义空间中的坐标靠拢。
*   **自注意力机制 (Self-Attention)**：采用相位位移与欧几里得距离判定，当神经元（粒子）的距离小于阈值时，自动绘制透明度衰减的连接线，完美具象化了 Transformer 的 QKV 张量矩阵。
*   **人类反馈强化学习 (RLHF)**：利用递归分形算法（Fractal Tree）绘制了深度达 9 层的隐式决策树，并在主干路径叠加动态高亮，隐喻 Reward Model 对发散概率的“安全修剪”。
*   **混合专家架构 (MoE)**：运用极坐标系动态计算激活节点，通过极速缓动函数模拟数据的稀疏路由（Sparse Routing）寻址过程。

---

## 🛠️ CS 深度剖析：性能调优与踩坑实录

作为一名 CS 专业的开发者，在构建这个高性能前端项目时，我遭遇并解决了一系列极具代表性的底层工程问题。特此记录，引以为戒：

### 1. 致命的 V8 GC 停顿与 GPU 上下文丢失
*   **背景**：在尝试将项目打包为“单文件绿色版”时，我尝试将 14.4MB 的背景音频强行 Base64 编码（体积膨胀至 19MB+）并注入 `<html>` 源码。
*   **事故现象**：GSAP 的 DOM 文字动画正常播放，但 Canvas 的背景粒子物理效果彻底死机（画面永久卡在第 3 幕）。
*   **Root Cause 分析**：
    浏览器解析并维护近 20MB 的连续字符串极大地阻塞了 JavaScript 的主线程，触发了 V8 引擎疯狂的垃圾回收（Garbage Collection）。内存和 CPU 的双重高压直接触发了浏览器的安全防御机制，导致 **WebGL/Canvas 2D 的 GPU 渲染上下文丢失 (Context Loss)**。
    最终，依赖于 GPU 刷新的 `requestAnimationFrame` 被迫中止，而依赖于 CPU 时钟的 GSAP 文字动画却在继续，造成了极其罕见的“字动图不动”的时空撕裂 Bug。
*   **破局方案**：坚决贯彻**关注点分离（Separation of Concerns）**。剥离重型媒体文件，使前端代码瞬间瘦身至 `20KB`，恢复了完美的 60fps 丝滑渲染。

### 2. 本地导出无损视频与 CORS 沙箱拦截
*   **背景**：为了避免传统的屏幕录制导致掉帧和画质压缩，最初我尝试在代码中植入 `MediaRecorder` API 配合 `canvas.captureStream(60)`，在浏览器底层直接将画面和 `AudioContext` 混流并渲染成 `.webm` 格式下载。
*   **事故现象**：画面成功录制，但音频死活无法写入，控制台抛出 Tainted Canvas 或跨域错误。
*   **Root Cause 分析**：在 `file:///` 本地文件协议下，受限于严格的同源安全策略，`AudioContext.createMediaElementSource()` 会直接拒绝抓取本地多媒体文件的音频缓冲（防范跨域数据窃取）。
*   **破局方案**：拥抱系统级硬件编码方案（如高码率的 Xbox Game Bar / OBS），不强求在前端沙箱内进行超额的媒体混流。

---

## 🚀 部署与运行

本项目极致轻量，不需要任何构建工具（Webpack/Vite）即可运行。

1. 克隆本项目：
   ```bash
   git clone https://github.com/wwwyh007/Vibe-GPT-Evolution.git
   ```
2. 直接在任意浏览器中双击打开 `index.html`。
3. 按下 `F11` 进入全屏沉浸模式，戴上耳机，点击 `PLAY` 开始体验！

> **"一切智能的表象，其底层依然只是高维概率空间中的掷骰子。"**
