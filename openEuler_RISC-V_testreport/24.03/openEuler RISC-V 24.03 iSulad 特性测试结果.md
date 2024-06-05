openEuler RISC-V 24.03 iSulad 特性测试结果

### 1. 测试方法：

执行mugen测试套iSulad，smoke-iSulad

#### 2. 测试结果：

| 测试套       | 测试用例                                   | 测试结果 | 备注                                  |
| ------------ | ------------------------------------------ | -------- | ------------------------------------- |
| iSulad       | oe_test_iSulad_container                   | pass     |                                       |
| iSulad       | oe_test_iSulad_container01                 | pass     |                                       |
| iSulad       | oe_test_iSulad_container02                 | pass     |                                       |
| iSulad       | oe_test_iSulad_container03                 | pass     |                                       |
| iSulad       | oe_test_iSulad_container04                 | pass     |                                       |
| iSulad       | oe_test_iSulad_container05                 | pass     |                                       |
| iSulad       | oe_test_iSulad_resource_mapping            | pass     |                                       |
| iSulad       | oe_test_iSulad_resource_restriction_cgroup | pass     |                                       |
| iSulad       | oe_test_service_isulad                     | pass     |                                       |
| smoke-iSulad | oe_test_iSula_query_state_001              | pass     |                                       |
| smoke-iSulad | oe_test_iSula_attach_rename_001            | pass     |                                       |
| smoke-iSulad | oe_test_iSula_export_001                   | pass     |                                       |
| smoke-iSulad | oe_test_iSula_cp_001                       | pass     |                                       |
| smoke-iSulad | oe_test_iSula_create_start_001             | pass     |                                       |
| smoke-iSulad | oe_test_iSula_restart_stop_001             | pass     |                                       |
| smoke-iSulad | oe_test_iSula_search_info_001              | pass     |                                       |
| smoke-iSulad | oe_test_iSula_exec_cmd_001                 | pass     |                                       |
| smoke-iSulad | oe_test_iSula_install_deploy_001           | pass     |                                       |
| smoke-iSulad | oe_test_iSula_mkdir100_001                 | pass     |                                       |
| smoke-iSulad | oe_test_iSula_pause_resume_001             | pass     |                                       |
| smoke-iSulad | oe_test_isula-build_build_image            | fail     | 执行isula-build成功但推送到isulad失败 |

#### 3. Issue List

| NO.  | Issue                                 | Issue URL                                                    |
| ---- | ------------------------------------- | ------------------------------------------------------------ |
| 1    | 执行isula-build成功但推送到isulad失败 | [I9QSAQ](https://gitee.com/src-openeuler/isula-build/issues/I9QSAQ) |

