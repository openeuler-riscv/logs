```json
{
    "id": "",
    "env": {
        "ip": "10.211.101.8",
        "username": "root",
        "port": 22,
        "testsuite_name": "fio-test",
        "os_version": "24.03",
        "arch": "riscv64"
    },
    "start": "2024-04-16 02:56:44",
    "console_log": "s3.dev.osssc.ac.cn/self-test/debugger/20240416/fio-test_20240416_030039.txt",
    "logs": {
        "oe_test_fio": {
            "log": "s3.dev.osssc.ac.cn/self-test/debugger/20240416/oe_test_fio_20240416_030042.txt"
        }
    },
    "passed_cases": [
        "oe_test_fio"
    ],
    "failed_cases": [],
    "total_case_num": 1,
    "passed_case_num": 1,
    "failed_case_num": 0,
    "exception_msg": "s3.dev.osssc.ac.cn/self-test/debugger/20240416/fio-test_20240416_030039.txt",
    "results": {
        "IOPS": {
            "bs": [
                "4KB",
                "16KB",
                "32KB",
                "64KB",
                "128KB",
                "256KB",
                "512KB",
                "1024KB"
            ],
            "read": [
                23.5,
                4695.0,
                3685.0,
                2322.0,
                1338.0,
                868.0,
                512.0,
                283.0
            ],
            "write": [
                29.2,
                5131.0,
                2533.0,
                1096.0,
                518.0,
                259.0,
                155.0,
                101.0
            ],
            "randread": [
                7887.0,
                3065.0,
                2289.0,
                1563.0,
                1132.0,
                819.0,
                514.0,
                275.0
            ],
            "randwrite": [
                8578.0,
                3102.0,
                2625.0,
                1078.0,
                520.0,
                461.0,
                277.0,
                139.0
            ],
"randrw": [
                4693.0,
                2694.0,
                1614.0,
                995.0,
                689.0,
                397.0,
                274.0,
                147.0
            ]
        },
        "bw": {
            "bs": [
                "4KB",
                "16KB",
                "32KB",
                "64KB",
                "128KB",
                "256KB",
                "512KB",
                "1024KB"
            ],
            "read": [
                91.7,
                73.4,
                115.0,
                145.0,
                167.0,
                217.0,
                256.0,
                284.0
            ],
            "write": [
                114.0,
                80.2,
                79.2,
                68.5,
                64.8,
                65.0,
                77.9,
                102.0
            ],
            "randread": [
                30.8,
                47.9,
                71.5,
                97.7,
                142.0,
                205.0,
                257.0,
                275.0
            ],
            "randwrite": [
                33.5,
                48.5,
                82.0,
                67.4,
                65.1,
                115.0,
                139.0,
                140.0
            ],
            "randrw": [
                18.3,
                42.1,
                50.5,
                62.2,
                86.2,
                99.4,
                137.0,
                148.0
            ]
        },
"lat(msec)": {
            "bs": [
                "4KB",
                "16KB",
                "32KB",
                "64KB",
                "128KB",
                "256KB",
                "512KB",
                "1024KB"
            ],
            "read": [
                4256.95,
                21287.21,
                27123.26,
                43033.14,
                74.67,
                115.09,
                195.13,
                351.42
            ],
            "write": [
                3420.48,
                19473.83,
                39225.11,
                91029.53,
                192.79,
                384.4,
                641.47,
                976.35
            ],
            "randread": [
                12670.16,
                32607.62,
                43653.46,
                63940.01,
                88246.53,
                121.86,
                194.29,
                362.47
            ],
            "randwrite": [
                11637.0,
                32205.2,
                38073.87,
                92634.88,
                191817.1,
                216.22,
                359.48,
                708.52
            ],
            "randrw": [
                14167.29,
                25664.28,
                41825.22,
                69521.36,
                96291.32,
                165.67,
                264.06,
                448.57
            ]
        }
    },
    "skipped_cases": [],
    "skipped_case_num": 0,
    "end": "2024-04-16 03:23:12",
    "time_delta": 1587.997646
}
```