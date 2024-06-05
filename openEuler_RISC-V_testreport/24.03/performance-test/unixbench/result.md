```json
{
    "id": "",
    "env": {
        "ip": "10.211.101.3",
        "username": "root",
        "port": 22,
        "testsuite_name": "unixbench",
        "os_version": "24.03",
        "arch": "riscv64"
    },
    "start": "2024-04-16 02:21:59",
    "console_log": "s3.dev.osssc.ac.cn/self-test/debugger/20240416/unixbench_20240416_115317.txt",
    "logs": {
        "oe_test_unixbench": {
            "log": "s3.dev.osssc.ac.cn/self-test/debugger/20240416/oe_test_unixbench_20240416_115319.txt"
        }
    },
    "passed_cases": [
        "oe_test_unixbench"
    ],
    "failed_cases": [],
    "total_case_num": 1,
    "passed_case_num": 1,
    "failed_case_num": 0,
    "exception_msg": "s3.dev.osssc.ac.cn/self-test/debugger/20240416/unixbench_20240416_115317.txt",
    "results": {
        "CPU_core_1unixbench.Dhrystone_2_using_register_variables": {
            "average": 13907408.560000002,
            "standard_deviation": "1563.521832402941982",
            "datas": [
                "13908139.6",
                "13906093.5",
                "13910816.3",
                "13906081.5",
                "13906156.0",
                "13906620.5",
                "13906558.0",
                "13909203.5",
                "13906069.7",
                "13908347.0"
            ]
        },
        "CPU_core_1unixbench.Double-Precision_Whetstone": {
            "average": 2644.2,
            "standard_deviation": "0.282842712474651",
            "datas": [
                "2644.1",
                "2643.6",
                "2644.5",
                "2644.3",
                "2644.5",
                "2644.5",
                "2644.0",
                "2643.9",
                "2644.3",
                "2644.3"
            ]
        },
        "CPU_core_1unixbench.Execl_Throughput": {
            "average": 428.5799999999999,
            "standard_deviation": "1.081480466767649",
            "datas": [
                "427.1",
                "428.6",
                "427.3",
                "427.1",
                "430.2",
                "428.8",
                "429.7",
                "429.9",
                "428.6",
                "428.5"
            ]
        },
        "CPU_core_1unixbench.File_Copy_1024_bufsize_2000_maxblocks": {
            "average": 137851.24,
            "standard_deviation": "1859.524744229016051",
            "datas": [
                "138784.1",
                "134404.2",
                "138511.2",
                "135488.8",
                "135910.7",
                "137514.8",
                "138712.9",
                "140363.8",
                "139480.4",
                "139341.5"
            ]
        },
        "CPU_core_1unixbench.File_Copy_256_bufsize_500_maxblocks": {
            "average": 36692.369999999995,
            "standard_deviation": "247.552422933002020",
            "datas": [
                "36345.8",
                "37107.0",
                "36671.9",
                "36784.1",
                "36910.2",
                "36957.1",
                "36305.7",
                "36661.9",
                "36482.7",
                "36697.3"
            ]
        },
        "CPU_core_1unixbench.File_Copy_4096_bufsize_8000_maxblocks": {
            "average": 448373.17000000004,
            "standard_deviation": "7565.038571620109906",
            "datas": [
                "444134.6",
                "457443.8",
                "454397.7",
                "442565.8",
                "454719.8",
                "440097.6",
                "447859.1",
                "459849.0",
                "435757.2",
                "446907.1"
            ]
        },
        "CPU_core_1unixbench.Pipe_Throughput": {
            "average": 261408.71000000002,
            "standard_deviation": "639.264801862262061",
            "datas": [
                "260996.4",
                "261461.2",
                "262709.8",
                "260906.6",
                "260547.4",
                "261524.6",
                "261280.6",
                "261810.7",
                "262144.3",
                "260705.5"
            ]
        },
        "CPU_core_1unixbench.Pipe-based_Context_Switching": {
            "average": 21385.420000000002,
            "standard_deviation": "496.983409783465049",
            "datas": [
                "20905.5",
                "21578.4",
                "21436.5",
                "20501.4",
                "21176.9",
                "21521.1",
                "21998.8",
                "20878.3",
                "21671.0",
                "22186.3"
            ]
        },
        "CPU_core_1unixbench.Process_Creation": {
            "average": 806.2699999999999,
            "standard_deviation": "6.476580888092117",
            "datas": [
                "804.3",
                "815.4",
                "805.6",
                "807.2",
                "809.3",
                "817.1",
                "804.1",
                "794.9",
                "797.9",
                "806.9"
            ]
        },
        "CPU_core_1unixbench.Shell_Scripts_(1_concurrent)": {
            "average": 1087.2900000000002,
            "standard_deviation": "1.488254010577494",
            "datas": [
                "1085.0",
                "1087.6",
                "1088.0",
                "1085.6",
                "1086.1",
                "1087.3",
                "1089.8",
                "1089.3",
                "1088.0",
                "1086.2"
            ]
        },
        "CPU_core_1unixbench.Shell_Scripts_(8_concurrent)": {
            "average": 256.69999999999993,
            "standard_deviation": "0.354964786985976",
            "datas": [
                "256.9",
                "257.1",
                "256.7",
                "256.1",
                "256.0",
                "256.8",
                "256.7",
                "257.1",
                "256.7",
                "256.9"
            ]
        },
        "CPU_core_1unixbench.System_Call_Overhead": {
            "average": 336151.57,
            "standard_deviation": "665.998373946962033",
            "datas": [
                "335076.1",
                "335415.5",
                "337459.6",
                "336359.3",
                "336237.3",
                "335394.0",
                "336473.5",
                "336690.3",
                "336237.9",
                "336172.2"
            ]
        },
        "CPU_core_1unixbench.System_Benchmarks_Index_Score": {
            "average": 250.18999999999997,
            "standard_deviation": "0.736817480791547",
            "datas": [
                "249.2",
                "250.7",
                "250.8",
                "248.6",
                "250.1",
                "250.3",
                "250.7",
                "250.5",
                "249.9",
                "251.1"
            ]
        },
        "CPU_core_4unixbench.Dhrystone_2_using_register_variables": {
            "average": 54679807.73,
            "standard_deviation": "32381.246901194313978",
            "datas": [
                "54699208.7",
                "54707682.2",
                "54640988.1",
                "54630886.9",
                "54700804.8",
                "54655611.3",
                "54686151.8",
                "54641277.6",
                "54716310.0",
                "54719155.9"
            ]
        },
        "CPU_core_4unixbench.Double-Precision_Whetstone": {
            "average": 10565.139999999998,
            "standard_deviation": "0.946784030283395",
            "datas": [
                "10563.7",
                "10565.5",
                "10563.8",
                "10565.9",
                "10566.3",
                "10563.9",
                "10566.3",
                "10565.3",
                "10565.2",
                "10565.5"
            ]
        },
        "CPU_core_4unixbench.Execl_Throughput": {
            "average": 1036.52,
            "standard_deviation": "2.662254683534222",
            "datas": [
                "1033.6",
                "1043.1",
                "1035.7",
                "1038.3",
                "1034.7",
                "1034.5",
                "1036.0",
                "1037.7",
                "1034.2",
                "1037.4"
            ]
        },
        "CPU_core_4unixbench.File_Copy_1024_bufsize_2000_maxblocks": {
            "average": 379964.64999999997,
            "standard_deviation": "1516.869871313952217",
            "datas": [
                "382233.6",
                "382089.2",
                "378836.3",
                "378418.8",
                "378508.4",
                "379361.0",
                "379510.0",
                "380819.0",
                "381704.4",
                "378165.8"
            ]
        },
        "CPU_core_4unixbench.File_Copy_256_bufsize_500_maxblocks": {
            "average": 99286.44,
            "standard_deviation": "711.434396413329864",
            "datas": [
                "98248.5",
                "99532.0",
                "98455.3",
                "99344.1",
                "99930.0",
                "99448.0",
                "99908.3",
                "100275.5",
                "99590.4",
                "98132.3"
            ]
        },
        "CPU_core_4unixbench.File_Copy_4096_bufsize_8000_maxblocks": {
            "average": 973701.65,
            "standard_deviation": "9616.138618827195387",
            "datas": [
                "976020.0",
                "962826.9",
                "968157.6",
                "957311.9",
                "972248.1",
                "974188.1",
                "982257.5",
                "986643.7",
                "988905.4",
                "968457.3"
            ]
        },
         "CPU_core_4unixbench.Pipe_Throughput": {
            "average": 1001932.0599999999,
            "standard_deviation": "2538.906935356227223",
            "datas": [
                "998159.9",
                "1001320.7",
                "999297.6",
                "1002487.5",
                "1004257.7",
                "998730.1",
                "1005710.0",
                "1000754.3",
                "1004128.2",
                "1004474.6"
            ]
        },
        "CPU_core_4unixbench.Pipe-based_Context_Switching": {
            "average": 147100.8,
            "standard_deviation": "19044.621693958637479",
            "datas": [
                "94857.3",
                "167512.1",
                "156940.5",
                "156318.0",
                "143608.3",
                "142216.9",
                "147599.2",
                "145622.0",
                "160977.1",
                "155356.6"
            ]
        },
        "CPU_core_4unixbench.Process_Creation": {
            "average": 2092.2,
            "standard_deviation": "6.906953018516930",
            "datas": [
                "2074.1",
                "2094.1",
                "2092.9",
                "2101.1",
                "2088.6",
                "2097.6",
                "2090.0",
                "2093.7",
                "2094.0",
                "2095.9"
            ]
        },
        "CPU_core_4unixbench.Shell_Scripts_(1_concurrent)": {
            "average": 1953.4299999999998,
            "standard_deviation": "3.069543940066660",
            "datas": [
                "1949.2",
                "1955.1",
                "1955.7",
                "1953.6",
                "1953.1",
                "1950.3",
                "1952.5",
                "1954.2",
                "1950.3",
                "1960.3"
            ]
        },
         "CPU_core_4unixbench.Shell_Scripts_(8_concurrent)": {
            "average": 279.37,
            "standard_deviation": "0.576281181368953",
            "datas": [
                "280.7",
                "279.0",
                "279.4",
                "279.2",
                "279.5",
                "279.6",
                "278.6",
                "278.9",
                "278.9",
                "279.9"
            ]
        },
        "CPU_core_4unixbench.System_Call_Overhead": {
            "average": 1280588.63,
            "standard_deviation": "1560.830844806707091",
            "datas": [
                "1279007.5",
                "1278044.7",
                "1281249.6",
                "1279654.0",
                "1282227.3",
                "1281778.2",
                "1278516.3",
                "1282224.9",
                "1282297.1",
                "1280886.7"
            ]
        },
        "CPU_core_4unixbench.System_Benchmarks_Index_Score": {
            "average": 717.79,
            "standard_deviation": "9.195265085901532",
            "datas": [
                "691.7",
                "726.3",
                "721.1",
                "721.0",
                "717.0",
                "716.2",
                "719.2",
                "719.3",
                "725.1",
                "721.0"
            ]
        }
    },
    "skipped_cases": [],
    "skipped_case_num": 0,
    "end": "2024-04-16 11:53:29",
    "time_delta": 34290.247651
}
```