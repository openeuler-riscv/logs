```json
{
    "id": "",
    "env": {
        "ip": "10.213.5.75",
        "username": "root",
        "port": 22,
        "testsuite_name": "lmbench",
        "os_version": "24.03",
        "arch": "riscv64"
    },
    "start": "2024-05-08 23:15:08",
    "console_log": "",
    "logs": {
        "oe_test_lmbench": {
            "log": "s3.dev.osssc.ac.cn/self-test/debugger/20240508/oe_test_lmbench_20240509_123948.txt"
        }
    },
    "passed_cases": [
        "oe_test_lmbench"
    ],
    "failed_cases": [],
    "total_case_num": 1,
    "passed_case_num": 1,
    "failed_case_num": 0,
    "exception_msg": "",
    "results": {
        "lmbench3.syscall.syscall.latency.us": {
            "average": 0.3525,
            "standard_deviation": 0.004629100498862762
        },
        "lmbench3.null_io": {
            "average": 0.6912499999999999,
            "standard_deviation": 0.006408699444616535
        },
        "lmbench3.syscall.stat.latency.us": {
            "average": 8.29875,
            "standard_deviation": 0.09062284480195922
        },
        "lmbench3.syscall.open/close.latency.us": {
            "average": 18.875,
            "standard_deviation": 0.5311712126450912
        },
        "lmbench3.Select.100tcp.latency.us": {
            "average": 13.125000000000002,
            "standard_deviation": 1.1961246948852304
        },
        "lmbench3.sig_inst": {
            "average": 0.8625,
            "standard_deviation": 0.010350983390135323
        },
        "lmbench3.sig_hndl": {
            "average": 7.1925,
            "standard_deviation": 0.1465556939479714
        },
        "lmbench3.fork_proc": {
            "average": 3928.0,
            "standard_deviation": 306.5858071451729
        },
        "lmbench3.exec_proc": {
            "average": 12625.0,
            "standard_deviation": 1922.6098333849673
        },
        "lmbench3.sh_proc": {
            "average": 18125.0,
            "standard_deviation": 2850.438562747845
        },
        "lmbench3.Process.fork+execve.latency.us": {
            "average": 16553.0,
            "standard_deviation": 1946.9009806796616
        },
        "lmbench3.Process.fork+/bin/sh.latency.us": {
            "average": 22053.0,
            "standard_deviation": 2866.87894009197
        },
        "lmbench3.PIPE.bandwidth.MB/sec": {
            "average": 1047.75,
            "standard_deviation": 135.0573952066306
        },
        "lmbench3.AF_UNIX.sock.stream.bandwidth.MB/sec": {
            "average": 1443.125,
            "standard_deviation": 194.48866107234704
        },
        "lmbench3.TCP.socket.bandwidth.10MB.MB/sec": {
            "average": 688.25,
            "standard_deviation": 33.39268525547816
        },
        "lmbench3.FILE.read.bandwidth.MB/sec": {
            "average": 2055.871428571428,
            "standard_deviation": 33.71308916359318
        },
        "lmbench3.MMAP.read.bandwidth.MB/sec": {
            "average": 5633.971428571428,
            "standard_deviation": 193.08907887540505
        },
        "lmbench3.BCOPY.libc.bandwidth.MB/sec": {
            "average": 3069.8999999999996,
            "standard_deviation": 144.8889821306546
        },
        "lmbench3.BCOPY.hand.bandwidth.MB/sec": {
            "average": 3248.7250000000004,
            "standard_deviation": 233.99314855659463
        },
        "lmbench3.BCOPY.memory_read.bandwidth.MB/sec": {
            "average": 6269.375,
            "standard_deviation": 32.46069051285614
        },
        "lmbench3.BCOPY.memory_write.bandwidth.MB/sec": {
            "average": 3119.375,
            "standard_deviation": 178.03445693781543
        },
        "lmbench3.Local.CTX.2P.0K.latency.us": {
            "average": 15.86375,
            "standard_deviation": 8.543017094178646
        },
        "lmbench3.PIPE.latency.us": {
            "average": 52.9125,
            "standard_deviation": 11.412454036834372
        },
        "lmbench3.AF_UNIX.sock.stream.latency.us": {
            "average": 89.01249999999999,
            "standard_deviation": 18.299838992265947
        },
        "lmbench3.UDP.usinglocalhost.latency.us": {
            "average": 109.87500000000001,
            "standard_deviation": 10.298231470916322
        },
        "lmbench3.RPC.UDP.usinglocalhost.latency.us": {
            "average": 160.3625,
            "standard_deviation": 39.11020829472969
        },
        "lmbench3.TCP.usinglocalhost.latency.us": {
            "average": 136.35,
            "standard_deviation": 6.209439818304296
        },
        "lmbench3.RPC.TCP.usinglocalhost.latency.us": {
            "average": 166.7875,
            "standard_deviation": 14.062761108687017
        },
        "lmbench3.TCP.CONNECT.localhost.latency.us": {
            "average": 352.25,
            "standard_deviation": 94.02697181432266
        },
        "lmbench3.CTX.2P.0K.latency.us": {
            "average": 15.86375,
            "standard_deviation": 8.543017094178646
        },
        "lmbench3.CTX.2P.16K.latency.us": {
            "average": 7.942499999999999,
            "standard_deviation": 4.618892105874989
        },
        "lmbench3.CTX.2P.64K.latency.us": {
            "average": 13.761249999999999,
            "standard_deviation": 7.315588908039364
        },
        "lmbench3.CTX.8P.16K.latency.us": {
            "average": 10.92875,
            "standard_deviation": 2.0067844748680486
        },
        "lmbench3.CTX.8P.64K.latency.us": {
            "average": 17.91875,
            "standard_deviation": 8.252529374163329
        },
        "lmbench3.CTX.16P.16K.latency.us": {
            "average": 8.185,
            "standard_deviation": 1.5694858120689446
        },
        "lmbench3.CTX.16P.64K.latency.us": {
            "average": 18.25,
            "standard_deviation": 5.22849336397617
        },
        "lmbench3.Mmap_Latency": {
            "average": 129187.5,
            "standard_deviation": 12658.41758334294
        },
        "lmbench3.Prot_Fault": {
            "average": 0.6453749999999999,
            "standard_deviation": 0.15236416667220112
        },
        "lmbench3.Select.100fd.latency.us": {
            "average": 5.2562500000000005,
            "standard_deviation": 0.03852179346069658
        },
        "lmbench3.L1_$": {
            "average": 1.504375,
            "standard_deviation": 0.0007440238091428323
        },
        "lmbench3.L2_$": {
            "average": 6.37525,
            "standard_deviation": 0.21166601049767064
        },
        "lmbench3.Main_mem": {
            "average": 24.3125,
            "standard_deviation": 0.13562026818605427
        },
        "lmbench3.Rand_mem": {
            "average": 198.62500000000003,
            "standard_deviation": 0.36547425158474683
        }
    },
    "skipped_cases": [],
    "skipped_case_num": 0,
    "end": "2024-05-09 12:39:51",
    "time_delta": 48282.889935
}
```