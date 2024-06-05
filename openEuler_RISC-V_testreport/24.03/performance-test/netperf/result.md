```json
{
    "id": "",
    "env": {
        "ip": "10.211.101.7",
        "username": "root",
        "port": 22,
        "testsuite_name": "netperf-performance",
        "os_version": "24.03",
        "arch": "riscv64"
    },
    "start": "2024-04-22 05:05:43",
    "console_log": "s3.dev.osssc.ac.cn/self-test/debugger/20240422/netperf-performance_20240422_053511.txt",
    "logs": {
        "oe_test_netperf-performance": {
            "log": "s3.dev.osssc.ac.cn/self-test/debugger/20240422/oe_test_netperf-performance_20240422_053513.txt"
        }
    },
    "passed_cases": [
        "oe_test_netperf-performance"
    ],
    "failed_cases": [],
    "total_case_num": 1,
    "passed_case_num": 1,
    "failed_case_num": 0,
    "exception_msg": "s3.dev.osssc.ac.cn/self-test/debugger/20240422/netperf-performance_20240422_053511.txt",
    "results": {
        "throughput": [
            {
                "protocol": "TCP",
                "packet_size": 1,
                "throughput": "432.47"
            },
            {
                "protocol": "TCP",
                "packet_size": 64,
                "throughput": "439.19"
            },
            {
                "protocol": "TCP",
                "packet_size": 128,
                "throughput": "415.48"
            },
            {
                "protocol": "TCP",
                "packet_size": 256,
                "throughput": "438.08"
            },
            {
                "protocol": "TCP",
                "packet_size": 512,
                "throughput": "436.08"
            },
            {
                "protocol": "TCP",
                "packet_size": 1024,
                "throughput": "437.49"
            },
            {
                "protocol": "TCP",
                "packet_size": 1500,
                "throughput": "435.26"
            },
            {
                "protocol": "TCP",
                "packet_size": 2048,
                "throughput": "434.48"
            },
            {
                "protocol": "TCP",
                "packet_size": 4096,
                "throughput": "429.49"
            },
            {
                "protocol": "TCP",
                "packet_size": 9000,
                "throughput": "433.89"
            },
            {
                "protocol": "TCP",
                "packet_size": 16384,
                "throughput": "437.79"
            },
            {
                "protocol": "TCP",
                "packet_size": 32768,
                "throughput": "438.90"
            },
            {
                "protocol": "UDP",
                "packet_size": 1,
                "throughput": "360.24"
            },
            {
                "protocol": "UDP",
                "packet_size": 64,
                "throughput": "357.00"
            },
            {
                "protocol": "UDP",
                "packet_size": 128,
                "throughput": "364.94"
            },
            {
                "protocol": "UDP",
                "packet_size": 256,
                "throughput": "365.37"
            },
            {
                "protocol": "UDP",
                "packet_size": 512,
                "throughput": "363.63"
            },
            {
                "protocol": "UDP",
                "packet_size": 1024,
                "throughput": "363.21"
            },
            {
                "protocol": "UDP",
                "packet_size": 1500,
                "throughput": "364.73"
            },
            {
                "protocol": "UDP",
                "packet_size": 2048,
                "throughput": "366.67"
            },
            {
                "protocol": "UDP",
                "packet_size": 4096,
                "throughput": "365.94"
            },
            {
                "protocol": "UDP",
                "packet_size": 9000,
                "throughput": "365.23"
            },
            {
                "protocol": "UDP",
                "packet_size": 16384,
                "throughput": "366.30"
            },
            {
                "protocol": "UDP",
                "packet_size": 32768,
                "throughput": "349.92"
            }
        ],
        "transfer_rate": [
            {
                "protocol": "TCP_RR",
                "transfer_rate": "1975.95"
            },
            {
                "protocol": "TCP_CRR",
                "transfer_rate": "890.07"
            },
            {
                "protocol": "UDP",
                "transfer_rate": "2004.47"
            }
        ],
        "logs": "s3.dev.osssc.ac.cn/self-test/debugger/20240422/netperf-performance_20240422_053514.txt"
    },
    "skipped_cases": [],
    "skipped_case_num": 0,
    "end": "2024-04-22 05:35:15",
    "time_delta": 1771.839536
}
```