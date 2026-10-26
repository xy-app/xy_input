# 获取按键状态 (GetKeyState)

检测 CapsLock / NumLock 开关锁定状态，或检测修饰键与按键是否正被物理按下，便于自动化流程做状态防御与环境复位。

## 平台与权限

* **支持平台**: `跨平台 (Windows / Linux / macOS)`
* **权限要求**: 普通用户权限（无需管理员提权）

## 运行参数

* **检测按键 (`key`)**
  * 类型: `string`
  * 默认值: `"CapsLock"`
  * 描述: 待检测的按键名称。常用预设：`CapsLock`, `NumLock`, `ScrollLock`, `Ctrl`, `Shift`, `Alt`, `Win`, `Space`, `Escape`, `Enter`。
* **检测类型 (`check_type`)**
  * 类型: `string`
  * 默认值: `"ToggleState"`
  * 描述: 检测类型。常用预设：`ToggleState` (检测大小写锁定等开关状态), `Pressed` (检测按键当前是否被物理按住)。

## 输出

* 类型: `bool`
* 描述: 按键状态判断布尔值。ToggleState 模式下开关开启返回 `true`；Pressed 模式下按键正被按下返回 `true`，否则返回 `false`。

## 使用示例

```json
{
    "tag": "GetKeyState",
    "key": "CapsLock",
    "check_type": "ToggleState"
}
```
