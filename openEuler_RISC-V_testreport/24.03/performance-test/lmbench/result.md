```json
{
    "id": "",
    "env": {
        "ip": "10.211.101.2",
        "username": "root",
        "port": 22,
        "testsuite_name": "lmbench",
        "os_version": "24.03",
        "arch": "riscv64"
    },
    "start": "2024-04-16 02:16:00",
    "console_log": "s3.dev.osssc.ac.cn/self-test/debugger/20240416/lmbench_20240416_134226.txt",
    "logs": {
        "oe_test_lmbench": {
            "log": "s3.dev.osssc.ac.cn/self-test/debugger/20240416/oe_test_lmbench_20240416_134229.txt"
        }
    },
    "passed_cases": [
        "oe_test_lmbench"
    ],
    "failed_cases": [],
    "total_case_num": 1,
    "passed_case_num": 1,
    "failed_case_num": 0,
    "exception_msg": "s3.dev.osssc.ac.cn/self-test/debugger/20240416/lmbench_20240416_134226.txt",
    "results": {
        "lmbench3.syscall.syscall.latency.us": {},
        "lmbench3.null_io": {},
        "lmbench3.syscall.stat.latency.us": {},
        "lmbench3.syscall.open/close.latency.us": {},
        "lmbench3.Select.100tcp.latency.us": {},
        "lmbench3.sig_inst": {},
        "lmbench3.sig_hndl": {},
        "lmbench3.fork_proc": {},
        "lmbench3.exec_proc": {},
        "lmbench3.sh_proc": {},
        "lmbench3.Process.fork+execve.latency.us": {
            "average": 0,
            "standard_deviation": 0.0
        },
        "lmbench3.Process.fork+/bin/sh.latency.us": {
            "average": 0,
            "standard_deviation": 0.0
        },
        "lmbench3.PIPE.bandwidth.MB/sec": {
            "average": 549.25,
            "standard_deviation": 179.78936088020973
        },
        "lmbench3.AF_UNIX.sock.stream.bandwidth.MB/sec": {
            "average": 555.75,
            "standard_deviation": 214.1319686548461
        },
        "lmbench3.TCP.socket.bandwidth.10MB.MB/sec": {
            "average": 371.25,
            "standard_deviation": 128.44315029281577
        },
        "lmbench3.FILE.read.bandwidth.MB/sec": {
            "average": 777.8142857142857,
            "standard_deviation": 292.7688304707967
        },
        "lmbench3.MMAP.read.bandwidth.MB/sec": {
            "average": 1567.1000000000001,
            "standard_deviation": 1046.506621097067
        },
        "lmbench3.BCOPY.libc.bandwidth.MB/sec": {
            "average": 2329.1749999999997,
            "standard_deviation": 979.801166053603
        },
        "lmbench3.BCOPY.hand.bandwidth.MB/sec": {
            "average": 2263.85,
            "standard_deviation": 1181.06911132003
        },
        "lmbench3.BCOPY.memory_read.bandwidth.MB/sec": {
            "average": 2141.75,
            "standard_deviation": 913.4330454781174
        },
        "lmbench3.BCOPY.memory_write.bandwidth.MB/sec": {
            "average": 6545.875,
            "standard_deviation": 598.6681497887027
        },
        "lmbench3.Local.CTX.2P.0K.latency.us": {
            "average": 22.792499999999997,
            "standard_deviation": 14.523887466613651
        },
        "lmbench3.PIPE.latency.us": {
            "average": 0,
            "standard_deviation": 0
        },
        "lmbench3.AF_UNIX.sock.stream.latency.us": {
            "average": 0,
            "standard_deviation": 0
        },
        "lmbench3.UDP.usinglocalhost.latency.us": {
            "average": 223.0,
            "standard_deviation": 133.73171437086802
        },
        "lmbench3.RPC.UDP.usinglocalhost.latency.us": {
            "average": 216.01999999999998,
            "standard_deviation": 71.13284754598259
        },
        "lmbench3.TCP.usinglocalhost.latency.us": {
            "average": 373.15,
            "standard_deviation": 239.29169885906433
        },
        "lmbench3.RPC.TCP.usinglocalhost.latency.us": {
            "average": 407.7,
            "standard_deviation": 230.98258808836653
        },
        "lmbench3.TCP.CONNECT.localhost.latency.us": {
            "average": 1097.875,
            "standard_deviation": 1150.9644946118638
        },
        "lmbench3.CTX.2P.0K.latency.us": {
            "average": 22.792499999999997,
            "standard_deviation": 14.523887466613651
        },
        "lmbench3.CTX.2P.16K.latency.us": {
            "average": 30.277499999999996,
            "standard_deviation": 21.05982074947458
        },
        "lmbench3.CTX.2P.64K.latency.us": {
            "average": 37.48625,
            "standard_deviation": 29.505827481315325
        },
        "lmbench3.CTX.8P.16K.latency.us": {
            "average": 42.9,
            "standard_deviation": 19.14792043911968
        },
        "lmbench3.CTX.8P.64K.latency.us": {
            "average": 58.025,
            "standard_deviation": 27.33776822325794
        },
        "lmbench3.CTX.16P.16K.latency.us": {
            "average": 52.63750000000001,
            "standard_deviation": 25.598210735462406
        },
        "lmbench3.CTX.16P.64K.latency.us": {
            "average": 76.8,
            "standard_deviation": 38.31527110696204
        },
        "lmbench3.Mmap_Latency": {
            "average": 228600.0,
            "standard_deviation": 36825.06910089531
        },
        "lmbench3.Prot_Fault": {
            "average": 0,
            "standard_deviation": 0
        },
        "lmbench3.Select.100fd.latency.us": {
            "average": 0,
            "standard_deviation": 0
        },
        "lmbench3.L1_$": {
            "average": 1.6464999999999999,
            "standard_deviation": 0.017986105748604948
        },
        "lmbench3.L2_$": {
            "average": 34.35,
            "standard_deviation": 32.68869835279465
        },
        "lmbench3.Main_mem": {
            "average": 63.96666666666666,
            "standard_deviation": 36.287885949262275
        },
        "lmbench3.Rand_mem": {
            "average": 105.71666666666665,
            "standard_deviation": 53.91442911379723
        }
    },
    "skipped_cases": [],
    "skipped_case_num": 0,
    "end": "2024-04-16 13:42:31",
    "time_delta": 41190.908202
}
```