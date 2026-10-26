# 模拟文本输入 (SendText)

向当前的输入框模拟敲击键盘输入一段文本内容。

## 平台与权限

* **支持平台**: `跨平台 (Windows / Linux / macOS)`
* **权限要求**: 普通用户权限（无需管理员提权；若受控程序拥有管理员UIPI权限需同等权限）

## 运行参数

* **输入文本内容 (`text`)**
  * 类型: `string`
  * 默认值: `""`
  * 描述: 要输入的文本内容。
* **文本输入模式 (`input_mode`)**
  * 类型: `string`
  * 默认值: `"Hardware"`
  * 描述: 文本输入模式。常用预设：`Hardware` (模拟物理敲击键盘), `Clipboard` (剪贴板复制粘贴，推荐大段文本与中文), `Simulate` (驱动注入)。
* **输入前自动清空 (`clear_before_input`)**
  * 类型: `bool`
  * 默认值: `false`
  * 描述: 输入前是否自动全选并清空输入框已有内容 (Ctrl+A -> Backspace)。常用预设：`true`, `false`。
* **输入后自动回车 (`enter_key`)**
  * 类型: `bool`
  * 默认值: `false`
  * 描述: 输入完成是否附带敲击回车键。常用预设：`true`, `false`。
* **驱动选择 (`driver`)**
  * 类型: `driver`
  * 默认值: `"Default"`
  * 描述: 输入驱动模式。常用预设：`Default`, `System`, `KMBox`。
    - Default: 全局硬件优先；若已连接 KMBox 则走硬件，未连接则降级系统软件模拟。
    - System: 强制使用操作系统原生底层 API 模拟。
    - KMBox: 强制使用 KMBox 物理硬件外设；若未连接则直接报错中断。

## 输出

* 类型: `bool`
* 描述: 文本字符串键入完成状态。成功录入所有字符返回 `true`，失败返回 `false`。

## 使用示例

```json
{
    "tag": "SendText",
    "text": "Hello, world!",
    "input_mode": "Hardware",
    "clear_before_input": false,
    "enter_key": false,
    "driver": "Default"
}
```
