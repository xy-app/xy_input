# 发送组合快捷键 (SendKey)

向当前活动窗口发送一组快捷键组合（如 Ctrl+C、Enter 等）

## 运行参数

* **快捷键组合 (`shortcut`)**
  * 类型: `string`
  * 默认值: `"Ctrl+C"`
  * 描述: 标准快捷键字符串。常用预设：`Ctrl+C`, `Ctrl+V`, `Ctrl+A`, `Ctrl+S`, `Alt+Tab`。

## 输出

* 类型: `bool`
* 描述: 组合快捷键发送状态 (true 表示成功)。

## 使用示例

```json
{
    "tag":  "SendKey",
    "shortcut":  "Ctrl+C"
}
```
