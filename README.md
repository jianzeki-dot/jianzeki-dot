# 建则ki · jianzeki-dot

> 室内设计从业者，业余写 ComfyUI 节点。喜欢把「反复手动做的事」拆成算法，做成一个能拖进画布的节点。

## 当前项目

### [comfyui-ki-nodes](https://github.com/jianzeki-dot/comfyui-ki-nodes) · 19 个 ComfyUI 自定义节点合集

把 9 个独立插件合并成一包，节点 ID 与前端扩展名全部保持不变，旧工作流不用重连。零 pip 依赖，只用 ComfyUI 自带环境。

| 方向 | 节点 | 做了什么 |
|---|---|---|
| **H3 音视频** | `ki_MiniMaxH3ReferenceToVideo`<br>`ki_MiniMaxH3LongVideoContinuation` | 按短边分级的参考图尺寸；把上一段 latent 尾部按 17k+5 时间网格钉到新片段开头，实现长视频续接 |
| **显存管理** | `ki_H3_Force_RAM_Offload`<br>`ki_Force_Ref_Evict` | 分 5 档强度强制模型回退系统内存，避免 VRAM>95% 时 GPU stall |
| **采样加速** | `KiZImageBoost` | 拦截 `DIFFUSION_MODEL`，用最小二乘轨迹外推替代可跳过的采样步，被跳步不产生前向计算 |
| **渐进采样** | `KiSelfLiftH3Sampler`<br>`KiSelfLiftImageSampler` | 低分辨率前缀 + Artifact-Aware Consistency Lift + 重新加噪，全分辨率续跑 |
| **视频调色** | `KiLoadVideoColorGrade`<br>`KiVideoCombineColorGrade` | 白平衡→曝光→对比度→影调→曲线→HSL→饱和度→LUT 的固定管线，255 个内置 LUT，实时预览 |
| **图像排版** | `ki_宫格拼图简易版`<br>`ki_宫格拼图高阶版2.0`<br>`ki_单图标注加载` | 槽位编辑器与固定 C×R 网格两套装配模式，三种奇数末张布局 |
| **全景与标注** | `Ki360PanoramaViewer`<br>`KiCameraMarker`<br>`ki_CreateBoundingBoxes` | Three.js 球面全景预览、PS 式机位图标编辑、老渲染器下的边界框编辑器 |

## 技术关注

`ComfyUI` · `PyTorch` · `扩散采样器` · `显存调度` · `色彩科学 / LUT` · `Three.js` · `Python`

## 一点说明

所有节点都是自用需求驱动：为了让 16GB 显卡跑得动 H3 长视频、为了不用开达芬奇就能给生成视频调色、为了把分镜图拼成一张能直接看的预览。代码优先保证「不破坏 ComfyUI 原有行为」，再谈加速。
