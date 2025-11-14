## GUIDE Test Report – Baoyi Lin

## 运行环境
- Apple M1 Max 
- Apple GPU 使用 Metal 框架 做加速，而 不支持 CUDA。因此，wanglabhkust/guide:v0.1 在 本设备 上 **GPU 加速无法使用，只能退回 CPU**。

<img width="280" height="499" alt="image" src="https://github.com/user-attachments/assets/549689b0-93e0-4449-b272-c5151a494254" />
<img width="699" height="229" alt="image" src="https://github.com/user-attachments/assets/da09f4f2-033f-48e8-b93f-c2e30c409824" />

## 遇到的问题/建议
1. GUIDE 可以增加 R package 版本，降低使用门槛。
2. **问题**：如果 Docker 内存不足， Docker 容器会崩溃退出:```time="2025-11-14T13:41:47+08:00" level=error msg="error waiting for container: unexpected EOF"```。\
   **建议**：建议在`GUIDE Docker Testing Manual`教程最开始处，指导仅支持CPU的设备修改Docker Memory Limit，调大到至少12GB(默认Docker Memory Limit< 10 GB)。\
   *参考：一张片子（CGGA_P87.svs，～1G），运行时占用的内存峰值（RAM）～32GB, 允许最多用 10 个 CPU 核的情况下CPU 峰值占用率～90%。* \
   **操作步骤**：
	1.	打开 Docker Desktop
	2.	Settings → Resources
	3.	调整：
 	  ```
    Memory: 12 GB（越大越好）
    CPUs: 8 以上
    ```
<img width="1270" height="721" alt="image" src="https://github.com/user-attachments/assets/fc9be386-4c00-4332-bb6b-6a001c781066" />





    
 
