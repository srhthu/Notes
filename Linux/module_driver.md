Find the driver of a specific device
```
ls -l /sys/class/net/eno1/device/driver
../../../bus/pci/drivers/e1000e
```
the `/sys/class/net/eno1/device` point to the device in the `/sys/devices/pci0000:00/0000:00:1f.6`

## pci 外设地址
0000:00:1f.1
- part1: 16位，表示域
- part2: 8位，总线编号
- part3: 5位，设备编号
- part4: 3位，功能号

总线之间用桥（bridge）连接
driver 位置：`/sys/bus/pci/drivers`
| pci 位置 | device 设备 | driver 驱动 |
| - | - | - |
|b3:00.0 | Samsung memory controller | nvme |
|17:00.0| nvidia titan xp | nvidia |
| 02:00.0 | USB3.1 controller ASMedia Tech | xhci_hcd |

## 驱动、设备含义
|Driver| name | desc | device |
|-|-|-| -|
|ioatdma| io at DMA| for DMA(Direct Memory Access)  | 00:04.0-7 |
| xhci_hcd | eXtensible Host Controller Interface | driver for USB 1.x, 2.0 and 3.x | 00:14, 02:00, 03:00, ... |
| ahci | Advanced hci | SATA | 00:17.0
| mei_me | unkonwn|
| pcieport | 
| iwlwifi | wifi driver | for network controller|
|e1000e| Gigabit ehternet| for ethernet controller|


