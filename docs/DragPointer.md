# 鼠标拖拽 (DragPointer)

按住鼠标从当前位置平滑拖拽移动到目标位置，常用于滑块验证码滑动或拖动文件与窗口。

## 平台与权限

* **支持平台**: `跨平台 (Windows / Linux / macOS)`
* **权限要求**: 普通用户权限（无需管理员提权；若目标程序具有管理员UIPI权限需同等权限）

## 运行参数

* **拖拽按键 (`button`)**
  * 类型: `MouseButton`
  * 默认值: `"Left"`
  * 描述: 拖拽过程中按住的鼠标键位。常用预设：`Left`, `Right`。
* **偏移坐标 (`offset`)**
  * 类型: `Point`
  * 默认值: `"100,0"`
  * 描述: 相对当前光标位置的偏移量 (dx, dy)。常用预设：`100,0`, `0,100`, `100,100`。
* **拖拽持续时间 (毫秒) (`duration`)**
  * 类型: `number`
  * 默认值: `200`
  * 描述: 平滑移动插值耗时（毫秒）。常用预设：`100`, `200`, `500`。
* **辅助修饰键 (`modifiers`)**
  * 类型: `KeySequence`
  * 默认值: `""`
  * 描述: 拖拽过程中同时按住的修饰键 (如 Ctrl, Shift)。常用预设：`""`, `Ctrl`, `Shift`, `Alt`, `Ctrl+Shift`。
* **驱动选择 (`driver`)**
  * 类型: `driver`
  * 默认值: `"Default"`
  * 描述: 输入驱动模式。常用预设：`Default`, `System`, `KMBox`。
    - Default: 全局硬件优先；若已连接 KMBox 则走硬件，未连接则降级系统软件模拟。
    - System: 强制使用操作系统原生底层 API 模拟。
    - KMBox: 强制使用 KMBox 物理硬件外设；若未连接则直接报错中断。

## 输出

* 类型: `bool`
* 描述: 鼠标按住拖拽滑动完成状态。成功执行按下、平滑位移与松开全过程返回 `true`，失败返回 `false`。

## 使用示例

```json
{
    "tag": "DragPointer",
    "button": "Left",
    "offset": "100,0",
    "duration": 200,
    "modifiers": "",
    "driver": "Default"
}
```
