# 侧栏 Window 二级导航设计

## 目标

在 TmuxAtlas 左侧 session 列表中直接展示并切换 session 下的 tmux window，避免用户必须打开 Command Palette，也不增加终端页面高度。

## 交互设计

- 每个 session 行提供展开/收起控制。
- 展开后显示该 session 的 window，标签包含 window 编号和名称。
- 当前 active window 高亮显示。
- 点击 window 调用现有 `/api/session/select-window` 接口。
- 切换后保持当前 session 页面，并通过状态刷新更新 active 标记。
- session 的展开状态由前端维护，状态刷新不重置。
- 侧栏收窄时隐藏二级 window 列表。

## 实现边界

复用现有 `Session.windows` 数据和 window 切换 API，不修改 tmux Agent、control mode 或 PTY 连接协议。错误沿用现有 runtime error 提示。

## 验证

- 侧栏测试覆盖展开/收起、window 展示、active 状态和点击切换请求。
- 运行相关前端测试与生产构建。
