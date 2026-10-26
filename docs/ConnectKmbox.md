# 连接硬件外设盒子 (ConnectKmbox)

连接 KMBox (B+串口 / Net网络) 或 Makcu (ESP32-S3串口) 硬件级键鼠模拟外设，支持超时重试与断线自动重连，提供原生物理硬件模拟与高兼容性外设控制；连接成功后 xy_input 中所有点击、移动、按键动作将自动通过物理硬件发送；支持断开以切回系统软件模拟。

## 平台与权限

* **支持平台**: `跨平台 (Windows / Linux / macOS)`
* **权限要求**: 普通用户权限（标准免驱 USB HID 复合设备通信，无需系统底层驱动或管理员权限）

## 运行参数

* **设备类型 (`device_type`)**
  * 类型: `string`
  * 默认值: `"Serial"`
  * 描述: 连接类型。常用预设：`Serial` (KMBox B/B+ 串口模式), `Net` (KMBox Net 网络模式), `Makcu` (Makcu ESP32-S3 串口模式)。
* **串口名称 (`port_name`)**
  * 类型: `string`
  * 默认值: `"COM3"`
  * 描述: KMBox B/B+ 或 Makcu 串口通信端口。常用预设：`COM3`, `COM4`, `COM5`, `/dev/ttyUSB0`。
* **波特率 (`baud_rate`)**
  * 类型: `number`
  * 默认值: `115200`
  * 描述: 串口波特率。KMBox 默认 115200，Makcu 支持 115200 与 4000000 (4M)。常用预设：`115200`, `4000000`, `9600`。
* **网络地址 (`remote_addr`)**
  * 类型: `string`
  * 默认值: `"192.168.2.188:1234"`
  * 描述: KMBox Net 远程 IP 和端口（仅在 device_type 为 Net 时生效）。常用预设：`192.168.2.188:1234`。
* **UUID / MAC (`mac`)**
  * 类型: `string`
  * 默认值: `"12345678"`
  * 描述: KMBox Net 通信校验 MAC（8位十六进制字符串）。
* **断开切回系统 (`disconnect`)**
  * 类型: `bool`
  * 默认值: `false`
  * 描述: false 表示连接/启用硬件盒子，true 表示断开并切回系统软件模拟。常用预设：`false`, `true`。
* **断线自动重连 (`auto_reconnect`)**
  * 类型: `bool`
  * 默认值: `true`
  * 描述: 通信断开或丢包时是否自动尝试多轮重连。常用预设：`true`, `false`。
* **超时毫秒数 (`timeout_ms`)**
  * 类型: `number`
  * 默认值: `1000`
  * 描述: 硬件握手与通信超时耗时（毫秒）。常用预设：`500`, `1000`, `2000`, `3000`。

## 输出

* 类型: `void`
* 描述: 无返回值。连接成功后全局硬件驱动实例激活生效，后续所有输入动作在 Default 驱动模式下自动走硬件通道；若通信握手失败则抛出错误。

## 使用示例

```json
{
    "tag": "ConnectKmbox",
    "device_type": "Serial",
    "port_name": "COM3",
    "baud_rate": 115200,
    "remote_addr": "192.168.2.188:1234",
    "mac": "12345678",
    "disconnect": false,
    "auto_reconnect": true,
    "timeout_ms": 1000
}
```
