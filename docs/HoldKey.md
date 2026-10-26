# 按键控制 (HoldKey)

按下并保持指定毫秒后释放、单向按下保持不放或松开指定按键，支持灵活的按键生命周期控制。

## 平台与权限

* **支持平台**: `跨平台 (Windows / Linux / macOS)`
* **权限要求**: 普通用户权限（无需管理员提权；若目标程序具有管理员UIPI权限需同等权限）

## 运行参数

* **按键名称 (`key`)**
  * 类型: `KeySequence`
  * 默认值: `"Enter"`
  * 描述: 目标按键或组合快捷键。常用预设：`Enter`, `Space`, `Tab`, `Escape`, `Backspace`, `Ctrl`, `Shift`, `Alt`, `W`, `A`, `S`, `D`。
* **操作模式 (`mode`)**
  * 类型: `string`
  * 默认值: `"Hold"`
  * 描述: 按键操作模式。常用预设：`Hold` (按住并延时后释放), `Down` (仅按下保持不放), `Up` (释放抬起按键)。
* **保持时长毫秒 (`duration_ms`)**
  * 类型: `number`
  * 默认值: `50`
  * 描述: 按住保持时长（毫秒，仅在 mode 为 Hold 时生效）。常用预设：`20`, `50`, `100`, `200`, `500`, `1000`。
* **驱动模式 (`driver`)**
  * 类型: `driver`
  * 默认值: `"Default"`
  * 描述: 输入驱动模式。常用预设：`Default`, `System`, `KMBox`。
    - Default: 全局硬件优先；若已连接 KMBox 则走硬件，未连接则降级系统软件模拟。
    - System: 强制使用操作系统原生底层 API 模拟。
    - KMBox: 强制使用 KMBox 物理硬件外设；若未连接则直接报错中断。

## 输出

* 类型: `string`
* 描述: 按键操作执行结果描述文本（如 `"ok"` 表示按键动作已成功派发至目标系统或硬件）。

## 使用示例

```json
{
    "tag": "HoldKey",
    "key": "Enter",
    "mode": "Hold",
    "duration_ms": 50,
    "driver": "Default"
}
```
