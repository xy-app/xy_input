# 监听鼠标事件 (ListenMouse)

在后台监听鼠标的点击或移动事件，并在触发时执行相应操作

## 运行参数

* **监听键位 (`button`)**
  * 类型: `string`
  * 默认值: `"left"`
  * 描述: 待捕获的鼠标按键。常用预设：`left`, `right`, `middle`, `x1`, `x2`。
* **事件类型 (`event_type`)**
  * 类型: `string`
  * 默认值: `"down"`
  * 描述: 鼠标事件类型。常用预设：`down`, `up`, `click`, `double_click`。
* **拦截事件传递 (`block_event`)**
  * 类型: `bool`
  * 默认值: `false`
  * 描述: 是否阻止事件传递给下层窗口。常用预设：`true`, `false`。

## 输出

* 类型: `bool`
* 描述: 鼠标事件监听配置状态 (true 表示成功)。

## 使用示例

```json
{
    "tag":  "ListenMouse",
    "button":  "left",
    "event_type":  "down",
    "block_event":  false
}
```
