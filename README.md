# ⌨️ 官方鼠标与键盘外设输入套件 (Mouse & Keyboard Input Suite)

[![Plugin Version](https://img.shields.io/badge/version-0.50.5-blue.svg)](manifest.json)
[![Group](https://img.shields.io/badge/group-Input-blue.svg)](#)
[![Platform](https://img.shields.io/badge/platform-All-green.svg)](#)
[![License](https://img.shields.io/badge/license-Freeware-brightgreen.svg)](#)

专为桌面自动化、RPA 机器人与游戏自动化测试设计的系统级外设输入套件。提供精确的鼠标绝对/相对移动、连击、平滑拖拽、滚轮滚动、键盘独立敲击与长按释放、系统全局快捷键广播、文本输入模拟以及全局键鼠事件监听。

---

## 📖 简介 (Overview)

`xy_input` 提供了跨平台的低延迟、高拟真键鼠外设控制能力：
- **精确鼠标交互**：支持屏幕绝对像素坐标平移（`MovePointer`）、基于当前位置的相对微调（`MoveOffset`）、平滑时间曲线拖拽（`DragPointer`）以及多键位自定义频次连击（`Click`、`CellsClick`）。
- **滚轮与多向滚动**：支持滚轮正反向滚动步数及滚动间隔控制（`WheelMouse`）。
- **全键盘仿真与打字输入**：支持敲击单键（`PressAndReleaseKey`）、长按不放（`PressKey`）、显式释放（`ReleaseKey`）、组合快捷键一键发送（`SendKey`）与字符串流式键入（`SendText`）。
- **事件监听与流程拦截**：提供系统全局鼠标监听（`ListenMouse`，支持阻断下发）、全局热键监听（`ListenKeyboard`）及按键同步阻塞等待（`WaitKey`）。

---

## ✨ 核心特性 (Features)

- **全外设键位覆盖**：支持鼠标左键 (`left`)、右键 (`right`)、中键 (`middle`) 以及侧键扩展 (`x1`, `x2`)。
- **高拟真拖拽与平滑移动**：内置 `duration` 平滑耗时参数，避免瞬移式触发引起的系统或安全防御风控。
- **灵活的键盘状态机**：支持按键按下不放（KeyDown）与按键释放（KeyUp）拆分控制，适用于游戏移动（WASD）或复杂快捷键组合持续按压。
- **系统全局事件监听**：原生监听系统鼠标与键盘事件，支持 `block_event` 拦截下发，可用于制作全局快捷键控制台或自动化紧急制动开关。
- **安全等待机制**：支持设定超时等待特定按键响应（`WaitKey`），方便人机协同（HITL）交互。

---

## 🛠️ 动作指令全景速查 (Action Catalog)

| 动作标识 (Tag) | 功能名称 | 描述 | 输出类型 |
| :--- | :--- | :--- | :--- |
| `MovePointer` | 鼠标绝对定位移动 | 将鼠标光标直接平移到屏幕上的指定绝对像素坐标 | `bool` |
| `MoveOffset` | 鼠标相对偏移移动 | 相对当前光标位置移动指定的水平与垂直像素距离 | `bool` |
| `Click` | 鼠标点击 | 在当前光标位置或指定坐标执行单击、双击或连击 | `bool` |
| `CellsClick` | 单元格点击 | 在指定的网格或单元格坐标区域自动执行鼠标点击 | `bool` |
| `DragPointer` | 鼠标拖拽 | 按住指定鼠标键从当前位置平滑拖拽至目标偏移坐标 | `bool` |
| `WheelMouse` | 滚动鼠标滚轮 | 模拟鼠标滚轮向前(上)或向后(下)滚动指定步数 | `bool` |
| `ListenMouse` | 监听鼠标事件 | 设置全局鼠标事件监听钩子并触发回调，支持事件拦截 | `bool` |
| `PressAndReleaseKey` | 敲击按键 | 模拟按下并在保持指定毫秒时长后释放单键 | `bool` |
| `PressKey` | 按下按键 | 按下指定按键并持续保持按下状态（不自动释放） | `bool` |
| `ReleaseKey` | 释放按键 | 释放处于按下状态的键盘按键 | `bool` |
| `SendKey` | 发送组合快捷键 | 向当前焦点窗口快速发送标准组合快捷键指令 | `bool` |
| `SendText` | 模拟文本输入 | 向当前焦点输入框模拟敲击输入完整文本内容 | `bool` |
| `ListenKeyboard` | 监听键盘事件 | 注册全局键盘按键监听与系统热键绑定 | `bool` |
| `WaitKey` | 等待按键触发 | 阻塞等待用户按下特定键盘按键或超时返回 | `bool` |

---

## 📚 详细参数说明与参考 (Detailed Reference)

### 1. 鼠标控制与移动 (Mouse Movement & Actions)

#### `MovePointer` - 鼠标绝对定位移动
- **输入参数：**
  | 参数名 (Field) | 显示名称 | 类型 | 默认值 | 预设推荐值 | 说明 |
  | :--- | :--- | :--- | :--- | :--- | :--- |
  | `xy` | 目标屏幕坐标 (X, Y) | `string` | `100,100` | `0,0`, `100,100`, `500,500` | 屏幕绝对像素物理坐标 |
- **输出类型：** `bool`

#### `MoveOffset` - 鼠标相对偏移移动
- **输入参数：**
  | 参数名 (Field) | 显示名称 | 类型 | 默认值 | 预设推荐值 | 说明 |
  | :--- | :--- | :--- | :--- | :--- | :--- |
  | `offset` | 偏移量 (X, Y) | `string` | `10,0` | `10,0`, `0,10`, `-10,0`, `0,-10` | 相对当前坐标的水平/垂直位移 |
- **输出类型：** `bool`

#### `Click` - 鼠标点击
- **输入参数：**
  | 参数名 (Field) | 显示名称 | 类型 | 默认值 | 预设推荐值 | 说明 |
  | :--- | :--- | :--- | :--- | :--- | :--- |
  | `button` | 鼠标按键 | `string` | `left` | `left`, `right`, `middle` | 触发点击的按键 |
  | `times` | 点击次数 | `number` | `1` | `1` (单击), `2` (双击) | 连续点击次数 |
  | `interval` | 点击间隔 (毫秒) | `number` | `50` | `50`, `100` | 连续点击间的缓冲间隔 |
- **输出类型：** `bool`

#### `CellsClick` - 单元格点击
- **输入参数：**
  | 参数名 (Field) | 显示名称 | 类型 | 默认值 | 预设推荐值 | 说明 |
  | :--- | :--- | :--- | :--- | :--- | :--- |
  | `target` | 目标网格区域 | `Rect` | `0, 0, 0, 0` | `0, 0, 1920, 1080`, `100, 100, 800, 600` | 目标屏幕网格矩形区域 (x, y, w, h) |
  | `grid` | 网格行列数 | `Size` | `3, 3` | `3, 3`, `4, 6`, `12, 12` | 划分网格的列数与行数 |
  | `delay` | 点击间隔延时 (秒) | `Real` | `0.05` | `0.05`, `0.1`, `0.2` | 依次点击每个单元格之间的间隔延迟时间 (秒) |
  | `button` | 鼠标按键 | `MouseButton` | `Left` | `Left`, `Right`, `Middle`, `DoubleClick`, `None` | 触发点击的鼠标键位 |
- **输出类型：** `bool`

#### `DragPointer` - 鼠标拖拽
- **输入参数：**
  | 参数名 (Field) | 显示名称 | 类型 | 默认值 | 预设推荐值 | 说明 |
  | :--- | :--- | :--- | :--- | :--- | :--- |
  | `button` | 拖拽按键 | `string` | `left` | `left`, `right` | 拖拽过程中持续按下的键位 |
  | `offset` | 偏移坐标 (X, Y) | `string` | `100,0` | `100,0`, `0,100`, `100,100` | 终点相对于起点的偏移量 |
  | `duration` | 拖拽持续时间 (毫秒) | `number` | `200` | `100`, `200`, `500` | 平滑移动全程消耗时间 |
- **输出类型：** `bool`

#### `WheelMouse` - 滚动鼠标滚轮
- **输入参数：**
  | 参数名 (Field) | 显示名称 | 类型 | 默认值 | 预设推荐值 | 说明 |
  | :--- | :--- | :--- | :--- | :--- | :--- |
  | `direction` | 滚动方向 | `string` | `down` | `up`, `down` | `up`: 向上/前; `down`: 向下/后 |
  | `times` | 滚动格数 | `number` | `3` | `1`, `3`, `5`, `10` | 滚轮滚动的刻度单位数 |
  | `interval` | 每次间隔 (毫秒) | `number` | `50` | `20`, `50`, `100` | 多格滚动间的停顿耗时 |
- **输出类型：** `bool`

---

### 2. 键盘模拟与按键操作 (Keyboard Actions & Typing)

#### `PressAndReleaseKey` - 敲击按键
- **输入参数：**
  | 参数名 (Field) | 显示名称 | 类型 | 默认值 | 预设推荐值 | 说明 |
  | :--- | :--- | :--- | :--- | :--- | :--- |
  | `key` | 按键名称 | `string` | `Enter` | `Enter`, `Tab`, `Space`, `Escape`, `Backspace` | 单个按键标识 |
  | `time` | 保持时长 (毫秒) | `number` | `50` | `20`, `50`, `100` | 按下到释放的物理持续时长 |
- **输出类型：** `bool`

#### `PressKey` 与 `ReleaseKey` - 按键状态控制
- **`PressKey`**：按下指定按键保持不放（如游戏长按 `W` 或组合辅助键 `Shift`）。
  - 参数：`key`（按键名称，如 `Shift`, `Control`, `Alt`, `W`, `A`, `S`, `D`）
- **`ReleaseKey`**：松开先前按下的按键。
  - 参数：`input`（按键名称，如 `Shift`, `Control`, `Alt`）
- **输出类型：** `bool`

#### `SendKey` - 发送组合快捷键
- **输入参数：**
  | 参数名 (Field) | 显示名称 | 类型 | 默认值 | 预设推荐值 | 说明 |
  | :--- | :--- | :--- | :--- | :--- | :--- |
  | `shortcut` | 快捷键组合 | `string` | `Ctrl+C` | `Ctrl+C`, `Ctrl+V`, `Ctrl+A`, `Ctrl+S`, `Alt+Tab` | 组合按键字符串 |
- **输出类型：** `bool`

#### `SendText` - 模拟文本输入
- **输入参数：**
  | 参数名 (Field) | 显示名称 | 类型 | 默认值 | 预设选项 | 说明 |
  | :--- | :--- | :--- | :--- | :--- | :--- |
  | `text` | 输入文本内容 | `string` | `""` | - | 待输入的文本字符串 |
  | `enter_key` | 输入后自动回车 | `bool` | `false` | `true`, `false` | 输入完毕后是否自动模拟敲击 Enter |
- **输出类型：** `bool`

---

### 3. 全局事件监听与同步 (Global Hook & Event Synchronization)

#### `ListenMouse` - 监听鼠标事件
- **输入参数：**
  | 参数名 (Field) | 显示名称 | 类型 | 默认值 | 预设推荐值 | 说明 |
  | :--- | :--- | :--- | :--- | :--- | :--- |
  | `button` | 监听键位 | `string` | `left` | `left`, `right`, `middle`, `x1`, `x2` | 目标按键 |
  | `event_type` | 事件类型 | `string` | `down` | `down`, `up`, `click`, `double_click` | 触发事件形式 |
  | `block_event` | 拦截事件传递 | `bool` | `false` | `true`, `false` | 若为 `true` 则截获并阻止下发至目标窗口 |
- **输出类型：** `bool`

#### `ListenKeyboard` - 监听键盘事件
- **输入参数：**
  | 参数名 (Field) | 显示名称 | 类型 | 默认值 | 预设推荐值 | 说明 |
  | :--- | :--- | :--- | :--- | :--- | :--- |
  | `input` | 按键名称/热键 | `string` | `F1` | `F1`, `F2`, `Ctrl+Shift+A`, `Space`, `Enter` | 监听的目标按键或组合热键 |
- **输出类型：** `bool`

#### `WaitKey` - 等待按键触发
- **输入参数：**
  | 参数名 (Field) | 显示名称 | 类型 | 默认值 | 预设推荐值 | 说明 |
  | :--- | :--- | :--- | :--- | :--- | :--- |
  | `key` | 目标按键 | `KeySequence` | `Enter` | `Enter`, `Escape`, `Space`, `F1`, `F2` | 期待触发的按键 |
  | `timeout` | 超时时间 (秒) | `real` | `5.0` | `1.0`, `3.0`, `5.0`, `0.0` | 阻塞超时限制；`0.0` 为永久等待 |
- **输出类型：** `bool`

---

## 📦 插件清单定义 (Manifest Reference)

```json
{
  "plugin_id": "xy_input",
  "name": "鼠标与键盘操作 (Mouse & Keyboard)",
  "version": "0.50.5",
  "group": "Input",
  "group_icon": "⌨",
  "description": "提供平滑拟人化鼠标移动、点击、拖拽滑动、滚轮滚动、键盘输入打字、快捷键触发与按键监听功能",
  "actions": [...]
}
```

---

## 📄 许可证 (License)

本插件遵循免费专有许可协议 (Freeware)。供 小友+ 用户免费下载与使用，未经官方书面授权，严禁对二进制文件进行逆向工程、反编译或二次打包转售。
