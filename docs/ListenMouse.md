# 监听鼠标事件 (ListenMouse)

在后台监听鼠标的点击或移动事件，并在触发时执行相应操作。

## 平台与权限

* **支持平台**: `跨平台 (Windows / Linux / macOS)`
* **权限要求**: 普通用户权限（无需管理员提权；若拦截全系统事件需安装底层钩子）

## 运行参数

* **监听键位 (`button`)**
  * 类型: `string`
  * 默认值: `"left"`
  * 描述: 待捕获的鼠标按键。常用预设：`left`, `right`, `middle`, `x1`, `x2`, `any`。
* **事件类型 (`event_type`)**
  * 类型: `string`
  * 默认值: `"down"`
  * 描述: 鼠标事件类型。常用预设：`down`, `up`, `click`, `double_click`, `any`。
* **拦截事件传递 (`block_event`)**
  * 类型: `string`
  * 默认值: `"none"`
  * 描述: 鼠标事件拦截模式：none（不拦截）、current（仅拦截当前监听的按键/事件）、all（拦截所有鼠标事件，受保护的应用窗口除外）。常用预设：`none`, `current`, `all`。

## 输出

* 类型: `bool`
* 描述: 鼠标全局监听钩子安装或事件配置状态。成功安装返回 `true`，失败返回 `false`。

## 使用示例

```json
{
    "tag": "ListenMouse",
    "button": "left",
    "event_type": "down",
    "block_event": "none"
}
```
