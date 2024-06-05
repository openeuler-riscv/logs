```json
{
    "id": "",
    "env": {
        "ip": "10.211.101.4",
        "username": "root",
        "port": 22,
        "testsuite_name": "nmap_test",
        "os_version": "24.03",
        "arch": "riscv64"
    },
    "start": "2024-04-22 06:16:14",
    "console_log": "s3.dev.osssc.ac.cn/self-test/debugger/20240422/nmap_test_20240422_061952.txt",
    "logs": {
        "oe_test_nmap_port_scan": {
            "log": "s3.dev.osssc.ac.cn/self-test/debugger/20240422/oe_test_nmap_port_scan_20240422_061955.txt"
        }
    },
    "passed_cases": [
        "oe_test_nmap_port_scan"
    ],
    "failed_cases": [],
    "total_case_num": 1,
    "passed_case_num": 1,
    "failed_case_num": 0,
    "exception_msg": "s3.dev.osssc.ac.cn/self-test/debugger/20240422/nmap_test_20240422_061952.txt",
    "results": {
        "ports": [
            {
                "ports": "22/tcp",
                "status": "open",
                "service": "ssh"
            },
            {
                "ports": "111/tcp",
                "status": "open",
                "service": "rpcbind"
            },
            {
                "ports": "68/udp",
                "status": "open|filtered",
                "service": "dhcpc"
            },
            {
                "ports": "111/udp",
                "status": "open",
                "service": "rpcbind"
            }
        ]
    },
    "skipped_cases": [],
    "skipped_case_num": 0,
    "end": "2024-04-22 06:19:55",
    "time_delta": 221.130269
}
```