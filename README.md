# Literature Review Mapper

这是一个 Flask + pywebview 打包的 Windows 桌面文献综述映射工具。完整使用教程请见 [`Read.md`](./Read.md)。

## 快速开始

1. 双击 `LiteratureReviewMapper.exe` 启动应用。
2. 左侧点击 **1 检索元信息**，输入关键词、选择 OpenAlex / Scopus 数据源，并点击 start。
3. 点击 **2 信息筛选**，选择年份、文献类型和语义归类方式。
4. 在第三步切换：
   - 总体引用网络图
   - 数据 / 方法 / 理论三圆聚合图
   - 共参考重叠网络图
5. 通过右上方详情入口查看聚合详情、核心文献和演化分析。

## 重要说明

- API Key 输入框默认没有写入任何个人 Key；Key 仅在本次请求中使用。
- 总体引用网络和共参考重叠网络依赖文献的 `referenced_works` 字段。
  - OpenAlex 直接提供该字段。
  - Scopus 通过 Abstract Retrieval API（`view=FULL`）解析参考文献列表中的 SGR ID，可生成 Scopus 文献之间的引用边和共参考边。
  - 如果 Scopus Abstract Retrieval 未能获取参考文献（例如权限不足或网络超时），则只选 Scopus 时网络图可能只有节点没有边。
- 图区域上方有节点大小滑块，可实时调整节点直径（50%～250%）。
- 拖动节点时周围节点会产生泡泡式避让效果：相邻节点弹性跟随，非相邻节点碰撞排斥。
- 三圆分析依赖摘要和语义归类，目前仍不稳定，建议作为辅助探索结果并人工复核。

## 打包分发

请分发整个 `dist/LiteratureReviewMapper` 文件夹或 `outputs/LiteratureReviewMapper.zip`，不要只分发单个 exe。应用运行依赖 `_internal` 文件夹中的静态资源和 Python 运行库。
