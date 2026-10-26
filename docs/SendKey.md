# 发送组合快捷键 (SendKey)

向当前活动窗口发送一组快捷键组合（如 Ctrl+C、Enter 等）。

## 平台与权限

* **支持平台**: `跨平台 (Windows / Linux / macOS)`
* **权限要求**: 普通用户权限（无需管理员提权；若受控程序拥有管理员UIPI权限需同等权限）

## 运行参数

* **快捷键组合 (`shortcut`)**
  * 类型: `string`
  * 默认值: `"Ctrl+C"`
  * 描述: 标准快捷键字符串。常用预设：`Ctrl+C`, `Ctrl+V`, `Ctrl+A`, `Ctrl+S`, `Alt+Tab`。
* **驱动选择 (`driver`)**
  * 类型: `driver`
  * 默认值: `"Default"`
  * 描述: 输入驱动模式。常用预设：`Default`, `System`, `KMBox`。
    - Default: 全局硬件优先；若已连接 KMBox 则走硬件，未连接则降级系统软件模拟。
    - System: 强制使用操作系统原生底层 API 模拟。
    - KMBox: 强制使用 KMBox 物理硬件外设；若未连接则直接报错中断。

## 输出

* 类型: `bool`
* 描述: 组合快捷键发送状态。成功向目标前台窗口派发按键序列返回 `true`，失败返回 `false`。

## 使用示例

```json
{
    "tag": "SendKey",
    "shortcut": "Ctrl+C",
    "driver": "Default"
}
```
