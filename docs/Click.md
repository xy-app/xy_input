# 鼠标点击 (Click)

在当前鼠标光标所在位置或屏幕当前坐标执行单击、双击或多重连击操作。

## 平台与权限

* **支持平台**: `跨平台 (Windows / Linux / macOS)`
* **权限要求**: 普通用户权限（无需管理员提权；若目标程序具有管理员UIPI权限需同等权限）

## 运行参数

* **鼠标按键 (`button`)**
  * 类型: `MouseButton`
  * 默认值: `"Left"`
  * 描述: 触发的鼠标键位。常用预设：`Left` (左键), `Right` (右键), `Middle` (中键)。
* **点击次数 (`times`)**
  * 类型: `number`
  * 默认值: `1`
  * 描述: 连续点击次数。常用预设：`1` (单击), `2` (双击)。
* **点击间隔秒 (`interval`)**
  * 类型: `real`
  * 默认值: `0.05`
  * 描述: 连续点击间的间隔时间 (秒)。常用预设：`0.05`, `0.1`, `0.2`。
* **辅助修饰键 (`modifiers`)**
  * 类型: `KeySequence`
  * 默认值: `""`
  * 描述: 点击过程中同时按住的修饰键 (如 Ctrl, Shift)。常用预设：`""`, `Ctrl`, `Shift`, `Alt`, `Ctrl+Shift`。
* **驱动选择 (`driver`)**
  * 类型: `driver`
  * 默认值: `"Default"`
  * 描述: 输入驱动模式。常用预设：`Default`, `System`, `KMBox`。
    - Default: 全局硬件优先；若已连接 KMBox 则走硬件，未连接则降级系统软件模拟。
    - System: 强制使用操作系统原生底层 API 模拟。
    - KMBox: 强制使用 KMBox 物理硬件外设；若未连接则直接报错中断。

## 输出

* 类型: `bool`
* 描述: 鼠标点击执行状态。成功触发点击返回 `true`，失败返回 `false`。

## 使用示例

```json
{
    "tag": "Click",
    "button": "Left",
    "times": 1,
    "interval": 0.05,
    "modifiers": "",
    "driver": "Default"
}
```
