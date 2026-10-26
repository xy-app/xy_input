# 监听键盘事件 (ListenKeyboard)

在后台监听键盘按键，或设置全局快捷键触发流程。

## 平台与权限

* **支持平台**: `跨平台 (Windows / Linux / macOS)`
* **权限要求**: 普通用户权限（无需管理员提权；若监听处于管理员权限的窗口需同等权限）

## 运行参数

* **按键名称/热键 (`input`)**
  * 类型: `string`
  * 默认值: `"F1"`
  * 描述: 监听的目标按键或组合热键。常用预设：`F1`, `F2`, `Ctrl+Shift+A`, `Space`, `Enter`, `all`。
* **拦截事件传递 (`block_event`)**
  * 类型: `string`
  * 默认值: `"none"`
  * 描述: 按键事件拦截模式：none（不拦截）、current（仅拦截当前监听的按键）、all（拦截所有按键，紧急停止键除外）。常用预设：`none`, `current`, `all`。

## 输出

* 类型: `bool`
* 描述: 键盘事件监听器或全局热键挂载状态。成功注册监听返回 `true`，热键冲突或注册失败返回 `false`。

## 使用示例

```json
{
    "tag": "ListenKeyboard",
    "input": "F1",
    "block_event": "none"
}
```
