# 基础学科

- 反射加载器 [ https://github.com/monoxgas/sRDI ]
- 调用栈伪造 [ https://github.com/WithSecureLabs/CallStackSpoofer , https://github.com/Barracudach/CallStack-Spoofer ]
- Wow64 进程执行 64 位代码 [ https://github.com/rwfpl/rewolf-wow64ext ]
- 别人写好的shellcode 弹calc,这样我就不用写了 [ https://github.com/peterferrie/win-exec-calc-shellcode ]
# 常见终端绕过（或检测）技术

## Bypass UAC

- [通过环境变量(DLL)劫持 iscsicpl, 不支持 win7](https://github.com/zha0gongz1/iscsicpl_bypassUAC)
- ICMLuaUtil 接口(通杀 win7-win11 墙裂推荐 ⭐)
	- [ShellExecute 版本](https://github.com/0xlane/BypassUAC/blob/master/BypassUAC/main.cpp)
	- [LaunchInf 版本](https://github.com/dro/uac-launchinf-poc/blob/master/poc.c)

## CS(SHELLCODE) 内存检测

- https://github.com/thefLink/Hunt-Sleeping-Beacons

## CS(SHELLCODE) 加载器

- [ AceLdr 具备`shellcode`运行时加解密, 调用栈伪造等特性 (TitanLdr 框架 + FOLIAGE + RET_ADDR_SPOOFING)](https://github.com/kyleavery/AceLdr)
- [TitanLdr 原版 D2H 的`shellcode`加载器, 粗略看过一遍]( https://github.com/kyleavery/TitanLdr )

## Bypass ETW
- <https://github.com/Allevon412/BreadBear/blob/4f1f5da39b423f0655df9338e01c8b733c6d1152/stage1/Evasion.c>
