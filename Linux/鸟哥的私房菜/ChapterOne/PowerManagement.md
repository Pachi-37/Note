[首页](../README.md)

[返回](One.md)

# 电源管理



### `APM` 和 `ACPI` 两种电源管理方案



##### `APM` （`Advanced Power Management`）

`APM` 是一种基于 `BIOS` 的电源系统管理方案，提供 `CPU` 和 外设电源管理并通过设备工作超时设定来将设备切换至低功耗模式

##### 电源状态

- 就绪
- 挂起
- 休眠
- 关闭



> 由于新老 `BIOS` 之间的不兼容性，无法判断电源管理命令是否由用户发起还是 `BIOS` 发起
>
> 主要不足：
>
> 代码缺乏一致性；系统进入挂起的原因无法判断；无法识别部分设备



##### `ACPI` `Advanced Configuration Power Interface`

