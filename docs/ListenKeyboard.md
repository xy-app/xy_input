# 监听键盘事件 (ListenKeyboard)

在后台监听键盘按键，或设置全局快捷键触发流程

## 运行参数

* **按键名称/热键 (`input`)**
  * 类型: `string`
  * 默认值: `"F1"`
  * 描述: 监听的目标按键或组合热键。常用预设：`F1`, `F2`, `Ctrl+Shift+A`, `Space`, `Enter`。

## 输出

* 类型: `bool`
* 描述: 键盘事件或快捷键注册监听状态 (true 表示成功)。

## 使用示例

```json
{
    "tag":  "ListenKeyboard",
    "input":  "F1"
}
```
