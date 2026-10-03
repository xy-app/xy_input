# 释放按键 (ReleaseKey)

松开之前处于按住状态的键盘按键

## 运行参数

* **按键名称 (`input`)**
  * 类型: `string`
  * 默认值: `"Shift"`
  * 描述: 要松开的按键。常用预设：`Shift`, `Control`, `Alt`。

## 输出

* 类型: `bool`
* 描述: 按键释放执行状态 (true 表示成功)。

## 使用示例

```json
{
    "tag":  "ReleaseKey",
    "input":  "Shift"
}
```
