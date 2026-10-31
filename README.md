<div align="center">
  <h1>🎬 Attention Is All You Need — Opus Vibe Generative Cinema</h1>
  <p><b>一部献给 2017 年那篇论文的五分钟生成式电影</b></p>
  <p>✨ <i>Single-File HTML · Canvas 2D · WebAudio Synthesized Score · Zero Dependencies (fonts aside)</i> ✨</p>
</div>

---

## 📖 项目概述 (Overview)

本项目是一部纯前端实现的交互式纪录短片，将 Vaswani 等人 2017 年的论文《Attention Is All You Need》（arXiv:1706.03762）拍成了一部 5 分钟的视觉电影：从穿入 T 字星核的第一帧，到八位作者逐一登场，再到万亿星系全貌的终章。全程由**确定性时间轴 render(t)** 驱动，每一帧都可复现；声音不使用任何音频文件，钢琴颗粒音效与呼吸感配乐全部由 **WebAudio 实时合成**。

打开仓库主页即可观看，**点击页面上的声音开关**开启完整声画体验。

## 🎮 交互方式 (Controls)

本片是一部可以操作的电影，播放器控件全部可用：

* **⏸ 暂停 / 继续**：随时定格，慢慢看每一帧的细节
* **🎹 声音开关**：开启后启用钢琴颗粒音效 + 呼吸感合成配乐（浏览器自动播放策略要求手动开启）
* **⏩ -2s / +2s 与进度条**：自由跳转，拖动进度条即时定位
* **🎞 章节按钮**：十个场景一键直达（见下方分镜表）

## 🎞 分镜表 (Scenes)

| # | 时间 | 场景 |
|---|------|------|
| ① | 0:00 | 穿入 T 字星核 |
| ② | 0:14 | 3D 手稿与黑胶声波 |
| ③ | 0:46 | 记忆灰烬 vs 引力连线 |
| ④ | 1:32 | 3D 晶格并行风暴 |
| ⑤ | 2:06 | #1 Vaswani 双核 |
| ⑥ | 2:20 | #2 Shazeer 27 亿回旋镖 |
| ⑦ | 2:48 | #4 Uszkoreit 3D-RNA 螺旋 |
| ⑧ | 3:02 | #5 Jones 东京鱼群流体 |
| ⑨ | 3:16 | #6 Gomez 实习生 70 亿超新星 |
| ⑩ | 3:58 | 万亿星系全貌与终章 |

## 💡 核心视效与底层算法 (Core Algorithms)

* **确定性时间轴 (Deterministic Timeline)**：全片抽象为纯函数 `render(t)`，任意时刻的画面只由时间 t 决定，拖动进度条零状态污染，也便于逐帧捕获与合成。
* **合成音景 (Synthesized Soundscape)**：钢琴颗粒以 WebAudio 振荡器与噪声缓冲实时合成，音符与画面事件对齐；配乐以呼吸式包络调制音量与滤波，拒绝单调循环。
* **引力连线 (Attention Web)**：粒子间以欧几里得距离判定连接，透明度随距离衰减，具象化自注意力机制的 QKV 关联矩阵。
* **分场调色 (Per-Scene Palettes)**：暖曜石与金色为主基调，每个场景拥有独立色彩脚本，告别全程深蓝的压抑感。

## 🛠️ CS 深度剖析：从 14.4MB 到 88KB

本仓库的前作版本曾把 14.4MB 的背景音乐塞进仓库，并一度尝试 Base64 内嵌音频，结果撞上了 V8 垃圾回收停顿与 GPU 上下文丢失。最终版给出了根治方案：

* **零音频资产**：声音全部实时合成，仓库里不再躺任何媒体文件，整部电影只剩一个 **88 KB** 的 HTML。
* **单文件分发**：除 Google Fonts 外零外部依赖，下载即播，离线可用（字体自动降级）。
* **帧纯函数化**：`render(t)` 的确定性设计同时解决了进度拖动、章节跳转与逐帧导出三个问题。

## 📼 前作版本 (Legacy Edition)

本仓库的第一版作品《运气的形状 (The Shape of AGI)》完整保留，记录着这条创作线最初的技术探索与全部踩坑原貌：

* **[legacy.html](legacy.html)**：初版《Vibe 知识大赏 - 进化的形状》本体，GPT 进化史编年动画（Canvas + GSAP），依赖同目录的 `bgm.mp4` 作为背景音乐
* **[README_v1.md](README_v1.md)**：初版 README 原文，包含完整的算法说明与“致命的 V8 GC 停顿”等工程事故复盘

## 📜 许可与声明 (License & Disclaimer)

* 本项目代码以 **MIT 许可证**开源，详见 [LICENSE](LICENSE)。
* 本片为独立教育作品，与 Google 及论文作者无隶属关系；论文《Attention Is All You Need》版权归原作者所有。

---

<div align="center">
  <p><i>Google invented the future, then gave it away.</i></p>
  <p>论文引用：Vaswani et al., "Attention Is All You Need", NeurIPS 2017, arXiv:1706.03762</p>
</div>
