# 按下按键 (PressKey)

按下指定按键并持续保持按住状态（不自动松开）

## 运行参数

* **按键名称 (`key`)**
  * 类型: `string`
  * 默认值: `"Shift"`
  * 描述: 要按住不放的按键。常用预设：`Shift`, `Control`, `Alt`, `W`, `A`, `S`, `D`。

## 输出

* 类型: `bool`
* 描述: 按键持续按下状态 (true 表示成功)。

## 使用示例

```json
{
    "tag":  "PressKey",
    "key":  "Shift"
}
```
