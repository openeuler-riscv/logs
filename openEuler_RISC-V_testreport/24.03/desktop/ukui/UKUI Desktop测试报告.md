UKUI Desktop测试

| 测试项目 | 测试内容                                                     | 测试结果 | 备注                 |
| -------- | ------------------------------------------------------------ | -------- | -------------------- |
| 安装UKUI | 执行命令安装UKUI<br>sudo dnf update<br>sudo dnf install ukui<br>安装成功后以图形界面方式启动: systemctl set-default graphical.target<br>再执行 reboot 重启 | pass     |                      |
| 登录     | 输入用户名和密码登录                                         | pass     |                      |
| 桌面     | 桌面图标                                                     | pass     |                      |
|          | 右键菜单                                                     | pass     |                      |
| 任务栏   | 基本功能                                                     | pass     |                      |
|          | 多视图切换                                                   | pass     |                      |
|          | 预览窗口                                                     | pass     |                      |
|          | 侧边栏                                                       | pass     |                      |
|          | 侧边栏-通知中心                                              | pass     |                      |
|          | 侧边栏-剪切板                                                | NA       | 无该选项             |
|          | 托盘菜单                                                     | pass     |                      |
|          | 托盘菜单-输入法                                              | NA       | 无该图标选项         |
|          | 托盘菜单-U盘                                                 | pass     |                      |
|          | 托盘菜单-电源                                                | fail     |                      |
|          | 托盘菜单-网络                                                | pass     |                      |
|          | 托盘菜单-网络-无线网络                                       | NA       | SG2042不支持无线网络 |
|          | 托盘菜单-网络-有线网络                                       | pass     |                      |
|          | 托盘菜单-网络-网络设置                                       | pass     |                      |
|          | 托盘菜单-音量                                                | pass     |                      |
|          | 托盘菜单-日历                                                | pass     |                      |
|          | 托盘菜单-夜间模式                                            | fail     |                      |
|          | 高级设置                                                     | pass     |                      |
| 窗口     | 窗口管理器                                                   | pass     |                      |
|          | 窗口切换                                                     | pass     |                      |
| 开始菜单 | 基本功能                                                     | pass     |                      |
|          | 右侧分类菜单                                                 | pass     |                      |
|          | 右侧功能键                                                   | fail     |                      |
|          | 右侧功能键-用户头像                                          | NA       | 无该图标选项         |
|          | 右侧功能键-计算机                                            | NA       | 无该图标选项         |
|          | 右侧功能键-设置                                              | NA       | 无该图标选项         |
|          | 右侧功能键-电源                                              | pass     |                      |
|          | 右侧功能键-锁定屏幕                                          | pass     |                      |
|          | 右侧功能键-用户切换和注销                                    | pass     |                      |
|          | 关机与重启                                                   | pass     |                      |
|          | 高级设置                                                     | pass     |                      |
|          | 应用                                                         | pass     |                      |
| 快捷键   | F5                                                           | pass     |                      |
|          | F1                                                           | pass     |                      |
|          | Alt + Tab                                                    | pass     |                      |
|          | win                                                          | pass     |                      |
|          | Ctrl + Alt + L                                               | pass     |                      |
|          | Ctrl + Alt + Delete                                          | pass     |                      |



Issue List

| NO.  | Issue                                                        | Issue URL                                                    |
| ---- | ------------------------------------------------------------ | ------------------------------------------------------------ |
| 1    | Computer->Properties->System Summary，Version显示24.03(LTS)，CPU和User显示空白 | [I9SMH3](https://gitee.com/src-openeuler/ukui-panel/issues/I9SMH3) |
