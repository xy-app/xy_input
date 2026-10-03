# 敲击按键 (PressAndReleaseKey)

按下某个按键并在保持指定时间后松开

## 运行参数

* **按键名称 (`key`)**
  * 类型: `string`
  * 默认值: `"Enter"`
  * 描述: 要模拟敲击的按键。常用预设：`Enter`, `Tab`, `Space`, `Escape`, `Backspace`。
* **保持时长 (毫秒) (`time`)**
  * 类型: `number`
  * 默认值: `50`
  * 描述: 按键按住到松开的时间。常用预设：`20`, `50`, `100`。

## 输出

* 类型: `bool`
* 描述: 按键敲击执行状态 (true 表示成功)。

## 使用示例

```json
{
    "tag":  "PressAndReleaseKey",
    "key":  "Enter",
    "time":  50
}
```
