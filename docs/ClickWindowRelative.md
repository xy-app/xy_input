# 窗口相对点击 (ClickWindowRelative)

以指定窗口或其客户区左上角为基准，按相对像素偏移坐标执行鼠标点击，免疫窗口移动位置变化与 DPI 缩放影响。

## 平台与权限

* **支持平台**: `跨平台 (Windows / Linux / macOS)`
* **权限要求**: 普通用户权限（无需管理员提权；若目标程序具有管理员UIPI权限需同等权限）

## 运行参数

* **目标窗口 (`window`)**
  * 类型: `Wnd`
  * 默认值: `"Foreground"`
  * 描述: 目标窗口对象或预设标识。常用预设：`Foreground` (前台活动窗口), `Desktop` (桌面)。
* **相对坐标偏移 (`offset`)**
  * 类型: `Point`
  * 默认值: `"10,10"`
  * 描述: 相对窗口基准原点的像素偏移坐标 (x, y)。常用预设：`10,10`, `50,50`, `100,100`, `200,150`。
* **基准区域 (`coord_base`)**
  * 类型: `string`
  * 默认值: `"Client"`
  * 描述: 坐标原点基准模式。常用预设：`Client` (客户区内部左上角，推荐), `Window` (窗口外边框左上角)。
* **置顶激活窗口 (`activate`)**
  * 类型: `bool`
  * 默认值: `true`
  * 描述: 点击前是否自动将目标窗口置顶并激活到前台获取焦点。
* **鼠标按键 (`button`)**
  * 类型: `MouseButton`
  * 默认值: `"Left"`
  * 描述: 触发点击的鼠标键位。常用预设：`Left`, `Right`, `Middle`。
* **点击次数 (`times`)**
  * 类型: `number`
  * 默认值: `1`
  * 描述: 连续点击次数。常用预设：`1` (单击), `2` (双击)。
* **点击间隔秒 (`interval`)**
  * 类型: `real`
  * 默认值: `0.05`
  * 描述: 连续点击间的间隔时间（秒）。常用预设：`0.05`, `0.1`, `0.2`。
* **辅助修饰键 (`modifiers`)**
  * 类型: `KeySequence`
  * 默认值: `""`
  * 描述: 点击过程中同时按住的修饰键 (如 Ctrl, Shift)。常用预设：`""`, `Ctrl`, `Shift`, `Alt`, `Ctrl+Shift`。
* **驱动模式 (`driver`)**
  * 类型: `driver`
  * 默认值: `"Default"`
  * 描述: 输入驱动模式。常用预设：`Default`, `System`, `KMBox`。
    - Default: 全局硬件优先；若已连接 KMBox 则走硬件，未连接则降级系统软件模拟。
    - System: 强制使用操作系统原生底层 API 模拟。
    - KMBox: 强制使用 KMBox 物理硬件外设；若未连接则直接报错中断。

## 输出

* 类型: `bool`
* 描述: 窗口相对点击执行状态。成功计算绝对坐标并完成点击返回 `true`，窗口无效或点击失败返回 `false`。

## 使用示例

```json
{
    "tag": "ClickWindowRelative",
    "window": "Foreground",
    "offset": "50,50",
    "coord_base": "Client",
    "activate": true,
    "button": "Left",
    "times": 1,
    "interval": 0.05,
    "modifiers": "",
    "driver": "Default"
}
```
