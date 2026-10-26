# ⌨️ 官方鼠标与键盘外设输入套件 (Mouse & Keyboard Input Suite)

[![Plugin Version](https://img.shields.io/badge/version-0.53.0-blue.svg)](manifest.json)
[![Group](https://img.shields.io/badge/group-Input-blue.svg)](#)
[![Platform](https://img.shields.io/badge/platform-All-green.svg)](#)
[![License](https://img.shields.io/badge/license-Freeware-brightgreen.svg)](#)
[![Discord](https://img.shields.io/discord/832082456727257118?label=Discord&logo=discord&logoColor=white&color=5865F2)](https://discord.gg/g5Fh3FtfGx)

专为桌面自动化、RPA 机器人与游戏自动化测试设计的系统级外设输入套件。提供精确的鼠标绝对/相对移动、连击、平滑拖拽、滚轮滚动、键盘独立敲击与长按释放、系统全局快捷键广播、文本输入模拟、全局键鼠事件监听，以及 **KMBox 硬件级外设盒子直通（反作弊防御绕过）**。

---

## 📖 简介 (Overview)

`xy_input` 提供了跨平台的低延迟、高拟真键鼠外设控制能力：
- **精确鼠标交互**：支持屏幕绝对像素坐标平移与相对微调（`MovePointer`）、定点点击（`ClickAt`）、基于窗口/客户区的相对点击（`ClickWindowRelative`）、光标位置读取与瞬移（`PointerPosition`）、平滑时间曲线拖拽（`DragPointer`）以及多键位自定义频次连击（`Click`、`CellsClick`）。
- **滚轮与多向滚动**：支持滚轮正反向滚动步数及滚动间隔控制（`WheelMouse`）。
- **全键盘仿真与打字输入**：支持复合按键控制（`HoldKey`，集成单键保持、长按按下与按键释放）、快捷键状态防御检测（`GetKeyState`，检查大写锁定/数字键锁定/修饰键物理按下）、组合快捷键一键发送（`SendKey`）与字符串流式键入（`SendText`）。
- **事件监听与流程拦截**：提供系统全局鼠标监听（`ListenMouse`，支持阻断下发）、全局热键监听（`ListenKeyboard`）及按键同步阻塞等待（`WaitKey`）。
- **硬件级外设仿真 (KMBox / Makcu)**：提供硬件模拟盒子连接（`ConnectKmbox`），通过物理 USB HID 协议向主机直接注入键鼠输入，提供原生物理级键鼠模拟；支持动作属性级驱动重写（`driver`: `Default` / `System` / `KMBox`）。

---

## ✨ 核心特性 (Features)

- **硬件盒子直通与原生物理模拟**：原生集成 KMBox B+ 串口、KMBox Net UDP 网络硬件盒子与 Makcu ESP32-S3 串口外设，实现完全免驱的真实物理键鼠输入注入。
- **动作属性级驱动路由 (Plan C: Driver Override)**：每个键鼠动作均支持 `driver` 属性（`Default`: 优先硬件未连降级系统；`System`: 强制系统原生；`KMBox`: 强制硬件外设），兼顾普通自动化与对抗性测试场景。
- **全外设键位覆盖**：支持鼠标左键 (`left`)、右键 (`right`)、中键 (`middle`) 以及侧键扩展 (`x1`, `x2`)。
- **高拟真拖拽与平滑移动**：内置 `duration` 平滑耗时参数，避免瞬移式触发引起的系统或安全防御风控。
- **灵活的键盘状态机**：`HoldKey` 整合按下保持 (Hold)、持续按下 (Down) 与按键释放 (Up)，配合 `GetKeyState` 状态防御，完美满足游戏操作与快捷键环境复位。
- **系统全局事件监听**：原生监听系统鼠标与键盘事件，支持 `block_event` 拦截下发，可用于制作全局快捷键控制台或自动化紧急制动开关。
- **安全等待机制**：支持设定超时等待特定按键响应（`WaitKey`），方便人机协同（HITL）交互。

---

## 🛠️ 动作指令全景速查 (Action Catalog)

| 动作标识 (Tag) | 功能名称 | 描述 | 输出类型 |
| :--- | :--- | :--- | :--- |
| `CellsClick` | 单元格点击 | 在指定的网格或单元格坐标区域自动执行鼠标点击 | `bool` |
| `Click` | 鼠标点击 | 在当前光标位置或指定坐标执行单击、双击或连击 | `bool` |
| `ClickAt` | 定点点击 | 将鼠标移动到指定绝对坐标并执行单击、双击或连击（支持瞬移或平滑轨迹） | `bool` |
| `ClickWindowRelative` | 窗口相对点击 | 基于目标窗口或工作客户区相对坐标执行点击，免疫窗口移动与 DPI 缩放 | `bool` |
| `ConnectKmbox` | 连接硬件外设盒子 | 连接 KMBox (B+串口/Net网络) 或 Makcu (ESP32-S3串口) 硬件外设盒子，支持原生物理硬件模拟并自动路由键鼠操作 | `void` |
| `DragPointer` | 鼠标拖拽 | 按住指定鼠标键从当前位置平滑拖拽至目标偏移坐标 | `bool` |
| `GetKeyState` | 获取按键状态 | 检测按键锁定状态（CapsLock/NumLock）或物理按下状态（Ctrl/Shift 等） | `bool` |
| `HoldKey` | 复合按键控制 | 统一的键盘状态控制，支持敲击保持 (Hold)、持续按住 (Down) 或释放 (Up) | `bool` |
| `ListenKeyboard` | 监听键盘事件 | 注册全局键盘按键监听与系统热键绑定 | `bool` |
| `ListenMouse` | 监听鼠标事件 | 设置全局鼠标事件监听钩子并触发回调，支持事件拦截 | `bool` |
| `MovePointer` | 鼠标光标移动 | 将鼠标光标绝对定位到指定像素位置，或基于当前光标相对偏移微调 | `bool` |
| `PointerPosition` | 获取/设置光标位置 | 读取当前光标所在的绝对坐标或即时瞬移至指定物理坐标 | `Point` |
| `SendKey` | 发送组合快捷键 | 向当前焦点窗口快速发送标准组合快捷键指令 | `bool` |
| `SendText` | 模拟文本输入 | 向当前焦点输入框模拟敲击输入完整文本内容 | `bool` |
| `WaitKey` | 等待按键触发 | 阻塞等待用户按下特定键盘按键或超时返回 | `bool` |
| `WheelMouse` | 滚动鼠标滚轮 | 模拟鼠标滚轮向前(上)或向后(下)滚动指定步数 | `bool` |

---

## 📚 详细参数说明与参考 (Detailed Reference)

### 1. 鼠标控制与移动 (Mouse Movement & Actions)

#### `MovePointer` - 鼠标光标移动
- **输入参数：**
  | 参数名 (Field) | 显示名称 | 类型 | 默认值 | 预设推荐值 | 说明 |
  | :--- | :--- | :--- | :--- | :--- | :--- |
  | `xy` | 目标坐标/偏移量 (X, Y) | `string` | `100,100` | `0,0`, `100,100`, `500,500`, `10,0`, `-10,0` | 绝对模式为目标绝对坐标；相对模式为位移增量 |
  | `mode` | 移动模式 | `string` | `Absolute` | `Absolute`, `Relative` | `Absolute`(绝对坐标定位), `Relative`(相对当前光标位移) |
  | `driver` | 驱动选择 | `driver` | `Default` | `Default`, `System`, `KMBox` | `Default`(硬件优先/未连降级), `System`(强制系统), `KMBox`(强制硬件) |
- **输出类型：** `bool`

#### `ClickAt` - 定点点击
- **输入参数：**
  | 参数名 (Field) | 显示名称 | 类型 | 默认值 | 预设推荐值 | 说明 |
  | :--- | :--- | :--- | :--- | :--- | :--- |
  | `xy` | 目标屏幕坐标 (X, Y) | `string` | `100,100` | `100,100`, `500,500`, `960,540` | 目标屏幕物理绝对坐标 |
  | `button` | 鼠标按键 | `string` | `left` | `left`, `right`, `middle` | 触发点击的鼠标键位 |
  | `times` | 点击次数 | `number` | `1` | `1` (单击), `2` (双击), `3` (三击) | 连续点击次数 |
  | `interval` | 点击间隔 (毫秒) | `number` | `50` | `50`, `100`, `200` | 多次点击之间的缓冲间隔 |
  | `move_duration` | 移动平滑耗时 (毫秒) | `number` | `0` | `0`, `100`, `200`, `500` | `0` 为即时瞬移；大于 0 时平滑移动 |
  | `driver` | 驱动选择 | `driver` | `Default` | `Default`, `System`, `KMBox` | `Default`(硬件优先/未连降级), `System`(强制系统), `KMBox`(强制硬件) |
- **输出类型：** `bool`

#### `ClickWindowRelative` - 窗口相对点击
- **输入参数：**
  | 参数名 (Field) | 显示名称 | 类型 | 默认值 | 预设推荐值 | 说明 |
  | :--- | :--- | :--- | :--- | :--- | :--- |
  | `wnd` | 目标窗口 | `Wnd` / `string` | `0` | - | 目标窗口对象或句柄整数 |
  | `offset` | 相对偏移坐标 (X, Y) | `string` | `10,10` | `10,10`, `50,50`, `100,100` | 相对窗口基准原点的像素偏移量 |
  | `coord_base` | 坐标基准 | `string` | `Client` | `Client`, `Window` | `Client`(客户区左上角), `Window`(窗口整体左上角) |
  | `activate` | 点击前激活窗口 | `bool` | `true` | `true`, `false` | 点击前是否自动置顶并激活目标窗口 |
  | `button` | 鼠标按键 | `string` | `left` | `left`, `right`, `middle` | 触发点击的鼠标键位 |
  | `times` | 点击次数 | `number` | `1` | `1` (单击), `2` (双击) | 连续点击次数 |
  | `interval` | 点击间隔 (毫秒) | `number` | `50` | `50`, `100` | 多次点击之间的间隔 |
  | `driver` | 驱动选择 | `driver` | `Default` | `Default`, `System`, `KMBox` | `Default`(硬件优先/未连降级), `System`(强制系统), `KMBox`(强制硬件) |
- **输出类型：** `bool`

#### `PointerPosition` - 获取/设置光标位置
- **输入参数：**
  | 参数名 (Field) | 显示名称 | 类型 | 默认值 | 预设推荐值 | 说明 |
  | :--- | :--- | :--- | :--- | :--- | :--- |
  | `action` | 操作类型 | `string` | `Get` | `Get`, `Set` | `Get`(读取当前光标位置), `Set`(瞬移光标到指定位置) |
  | `xy` | 目标坐标 (X, Y) | `string` | `0,0` | `0,0`, `500,500`, `960,540` | 仅在 `action` 为 `Set` 时生效的绝对物理坐标 |
  | `driver` | 驱动选择 | `driver` | `Default` | `Default`, `System`, `KMBox` | `Default`(硬件优先/未连降级), `System`(强制系统), `KMBox`(强制硬件) |
- **输出类型：** `Point` (对象包装，包含当前/更新后的 x, y 坐标)

#### `Click` - 鼠标点击
- **输入参数：**
  | 参数名 (Field) | 显示名称 | 类型 | 默认值 | 预设推荐值 | 说明 |
  | :--- | :--- | :--- | :--- | :--- | :--- |
  | `button` | 鼠标按键 | `string` | `left` | `left`, `right`, `middle` | 触发点击的按键 |
  | `times` | 点击次数 | `number` | `1` | `1` (单击), `2` (双击) | 连续点击次数 |
  | `interval` | 点击间隔 (毫秒) | `number` | `50` | `50`, `100` | 连续点击间的缓冲间隔 |
  | `driver` | 驱动选择 | `driver` | `Default` | `Default`, `System`, `KMBox` | `Default`(硬件优先/未连降级), `System`(强制系统), `KMBox`(强制硬件) |
- **输出类型：** `bool`

#### `CellsClick` - 单元格点击
- **输入参数：**
  | 参数名 (Field) | 显示名称 | 类型 | 默认值 | 预设推荐值 | 说明 |
  | :--- | :--- | :--- | :--- | :--- | :--- |
  | `target` | 目标网格区域 | `Rect` | `0, 0, 0, 0` | `0, 0, 1920, 1080`, `100, 100, 800, 600` | 目标屏幕网格矩形区域 (x, y, w, h) |
  | `grid` | 网格行列数 | `Size` | `3, 3` | `3, 3`, `4, 6`, `12, 12` | 划分网格的列数与行数 |
  | `delay` | 点击间隔延时 (秒) | `Real` | `0.05` | `0.05`, `0.1`, `0.2` | 依次点击每个单元格之间的间隔延迟时间 (秒) |
  | `button` | 鼠标按键 | `MouseButton` | `Left` | `Left`, `Right`, `Middle`, `DoubleClick`, `None` | 触发点击的鼠标键位 |
  | `driver` | 驱动选择 | `driver` | `Default` | `Default`, `System`, `KMBox` | `Default`(硬件优先/未连降级), `System`(强制系统), `KMBox`(强制硬件) |
- **输出类型：** `bool`

#### `DragPointer` - 鼠标拖拽
- **输入参数：**
  | 参数名 (Field) | 显示名称 | 类型 | 默认值 | 预设推荐值 | 说明 |
  | :--- | :--- | :--- | :--- | :--- | :--- |
  | `button` | 拖拽按键 | `string` | `left` | `left`, `right` | 拖拽过程中持续按下的键位 |
  | `offset` | 偏移坐标 (X, Y) | `string` | `100,0` | `100,0`, `0,100`, `100,100` | 终点相对于起点的偏移量 |
  | `duration` | 拖拽持续时间 (毫秒) | `number` | `200` | `100`, `200`, `500` | 平滑移动全程消耗时间 |
  | `driver` | 驱动选择 | `driver` | `Default` | `Default`, `System`, `KMBox` | `Default`(硬件优先/未连降级), `System`(强制系统), `KMBox`(强制硬件) |
- **输出类型：** `bool`

#### `WheelMouse` - 滚动鼠标滚轮
- **输入参数：**
  | 参数名 (Field) | 显示名称 | 类型 | 默认值 | 预设推荐值 | 说明 |
  | :--- | :--- | :--- | :--- | :--- | :--- |
  | `direction` | 滚动方向 | `string` | `down` | `up`, `down` | `up`: 向上/前; `down`: 向下/后 |
  | `times` | 滚动格数 | `number` | `3` | `1`, `3`, `5`, `10` | 滚轮滚动的刻度单位数 |
  | `interval` | 每次间隔 (毫秒) | `number` | `50` | `20`, `50`, `100` | 多格滚动间的停顿耗时 |
  | `driver` | 驱动选择 | `driver` | `Default` | `Default`, `System`, `KMBox` | `Default`(硬件优先/未连降级), `System`(强制系统), `KMBox`(强制硬件) |
- **输出类型：** `bool`

---

### 2. 键盘模拟与按键操作 (Keyboard Actions & Typing)

#### `HoldKey` - 复合按键控制
- **输入参数：**
  | 参数名 (Field) | 显示名称 | 类型 | 默认值 | 预设推荐值 | 说明 |
  | :--- | :--- | :--- | :--- | :--- | :--- |
  | `key` | 目标按键 | `string` | `A` | `A`, `W`, `S`, `D`, `Space`, `Enter`, `Shift`, `Ctrl` | 待操作的键盘按键名称 |
  | `mode` | 按键控制模式 | `string` | `Hold` | `Hold`, `Down`, `Up` | `Hold`(敲击保持), `Down`(长按不放), `Up`(按键释放) |
  | `duration_ms` | 保持时长 (毫秒) | `number` | `50` | `20`, `50`, `100`, `200`, `500` | 仅在 `Hold` 模式下生效的持续按下毫秒数 |
  | `driver` | 驱动选择 | `driver` | `Default` | `Default`, `System`, `KMBox` | `Default`(硬件优先/未连降级), `System`(强制系统), `KMBox`(强制硬件) |
- **输出类型：** `bool`

#### `GetKeyState` - 获取按键状态
- **输入参数：**
  | 参数名 (Field) | 显示名称 | 类型 | 默认值 | 预设推荐值 | 说明 |
  | :--- | :--- | :--- | :--- | :--- | :--- |
  | `key` | 目标按键 | `string` | `CapsLock` | `CapsLock`, `NumLock`, `ScrollLock`, `Ctrl`, `Shift`, `Alt` | 待检测状态的按键名称 |
  | `check_type` | 检测模式 | `string` | `ToggleState` | `ToggleState`, `Pressed` | `ToggleState`(检测是否处于锁定开启状态), `Pressed`(检测是否物理按下) |
- **输出类型：** `bool` (若开启或按下返回 `true`，否则返回 `false`)

#### `SendKey` - 发送组合快捷键
- **输入参数：**
  | 参数名 (Field) | 显示名称 | 类型 | 默认值 | 预设推荐值 | 说明 |
  | :--- | :--- | :--- | :--- | :--- | :--- |
  | `shortcut` | 快捷键组合 | `string` | `Ctrl+C` | `Ctrl+C`, `Ctrl+V`, `Ctrl+A`, `Ctrl+S`, `Alt+Tab` | 组合按键字符串 |
  | `driver` | 驱动选择 | `driver` | `Default` | `Default`, `System`, `KMBox` | `Default`(硬件优先/未连降级), `System`(强制系统), `KMBox`(强制硬件) |
- **输出类型：** `bool`

#### `SendText` - 模拟文本输入
- **输入参数：**
  | 参数名 (Field) | 显示名称 | 类型 | 默认值 | 预设选项 | 说明 |
  | :--- | :--- | :--- | :--- | :--- | :--- |
  | `text` | 输入文本内容 | `string` | `""` | - | 待输入的文本字符串 |
  | `enter_key` | 输入后自动回车 | `bool` | `false` | `true`, `false` | 输入完毕后是否自动模拟敲击 Enter |
  | `driver` | 驱动选择 | `driver` | `Default` | `Default`, `System`, `KMBox` | `Default`(硬件优先/未连降级), `System`(强制系统), `KMBox`(强制硬件) |
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

### 4. 硬件级外设直通与防检测 (Hardware Box Bypass & Driver Routing)

#### `ConnectKmbox` - 连接硬件外设盒子
- **输入参数：**
  | 参数名 (Field) | 显示名称 | 类型 | 默认值 | 预设推荐值 | 说明 |
  | :--- | :--- | :--- | :--- | :--- | :--- |
  | `device_type` | 设备类型 | `string` | `Serial` | `Serial`, `Net`, `Makcu` | `Serial`: KMBox B/B+ 串口模式；`Net`: KMBox Net UDP 网络模式；`Makcu`: Makcu ESP32-S3 串口模式 |
  | `port_name` | 串口名称 | `string` | `COM3` | `COM3`, `COM4`, `COM5`, `/dev/ttyUSB0` | KMBox B/B+ 或 Makcu 串口端口 |
  | `baud_rate` | 波特率 | `number` | `115200` | `115200`, `4000000`, `9600` | 串口通信波特率（KMBox 常用 115200，Makcu 支持 4000000 极速） |
  | `remote_addr` | 网络地址 | `string` | `192.168.2.188:1234` | `192.168.2.188:1234` | KMBox Net 远程 IP 与端口 |
  | `mac` | UUID / MAC | `string` | `12345678` | `12345678` | KMBox Net 通信校验硬件 MAC (8位十六进制) |
  | `disconnect` | 断开切回系统 | `number` | `0` | `0`, `1` | `0`: 激活/连接硬件；`1`: 断开并平滑恢复系统模拟 |
- **输出类型：** `void`

#### 驱动模式说明 (Driver Modes)
- **`Default` (默认智能路由)**：优先通过已连接的 KMBox / Makcu 硬件外设发送；若当前未连接硬件外设，自动无缝降级为系统原生软件模拟。适合绝大多数通用流程。
- **`System` (强制系统软件模拟)**：忽略任何已连接的硬件盒子，强制使用操作系统原生 API（如 Windows `SendInput`、macOS Quartz、Linux X11/uinput）执行。
- **`KMBox` (强制硬件外设)**：必须通过物理硬件外设发送；若硬件尚未连接或意外断开，该动作将立即返回错误并熔断流程，绝不降级至系统软件模拟，严防因驱动降级引发反作弊检测与账号封禁。

---

## 📦 插件清单定义 (Manifest Reference)

```json
{
  "plugin_id": "xy_input",
  "name": "鼠标与键盘操作 (Mouse & Keyboard)",
  "version": "0.51.1",
  "group": "Input",
  "group_icon": "⌨",
  "description": "提供平滑拟人化鼠标移动、点击、拖拽滑动、滚轮滚动、键盘输入打字、快捷键触发与按键监听功能",
  "actions": [...]
}
```

---

## 📄 许可证 (License)

本插件遵循免费专有许可协议 (Freeware)。供 小友+ 用户免费下载与使用，未经官方书面授权，严禁对二进制文件进行逆向工程、反编译或二次打包转售。
