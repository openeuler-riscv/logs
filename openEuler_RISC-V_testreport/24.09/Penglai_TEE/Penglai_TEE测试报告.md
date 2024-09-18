蓬莱TEE特性由
1.	在 opensbi 固件中的集成
2.	蓬莱内核驱动模块
3.	蓬莱 SDK 运行时套件组成

固件集成完成兼容性测试
1. 集成蓬莱特性的 opensbi 可以按预期方式进行启动
2. 内核驱动模块通过 dkms 加载，可以成功加载在内核中
3. SDK 运行时套件可以正常安装使用。

在测试功能时，利用蓬莱提供的 7 个 demo 示例作为测试用例，进行了编译和运行测试，测试全部通过，并且按照预期方式运行。
| 项目   | 用例名 | 编译 | 运行 |
| ------ | ---- | ---- | ---- |
| prime  |prime  | pass   |  pass  |
| aes    | aes    | pass    |   pass  |
| mem    | mem    | pass    |  pass   |
| crypt  | crypt  | pass    |  pass   |
| deadloop | deadloop| pass    |  pass   |
| count  | count  |pass    |  pass   |
| gm_test_enclaves | test_random |pass,直接通过源码可正常编译   |  pass  |
| gm_test_enclaves | test_sm2 |pass,直接通过源码可正常编译   |  pass  |
| gm_test_enclaves | test_sm4_cbc |pass,直接通过源码可正常编译   |  pass  |
| gm_test_enclaves | test_sm4_ocb |pass,直接通过源码可正常编译   |  pass  |
| seal_data    | seal_data    |pass,直接通过源码可正常编译  |  pass   |
