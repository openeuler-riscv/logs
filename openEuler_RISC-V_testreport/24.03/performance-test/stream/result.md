
```json
{
    "id": "",
    "env": {
        "ip": "10.211.101.5",
        "username": "root",
        "port": 22,
        "testsuite_name": "stream",
        "os_version": "24.03",
        "arch": "riscv64"
    },
    "start": "2024-04-16 02:20:38",
    "console_log": "s3.dev.osssc.ac.cn/self-test/debugger/20240416/stream_20240416_022351.txt",
    "logs": {
        "oe_test_stream": {
            "log": "s3.dev.osssc.ac.cn/self-test/debugger/20240416/oe_test_stream_20240416_022353.txt"
        }
    },
    "passed_cases": [
        "oe_test_stream"
    ],
    "failed_cases": [],
    "total_case_num": 1,
    "passed_case_num": 1,
    "failed_case_num": 0,
    "exception_msg": "s3.dev.osssc.ac.cn/self-test/debugger/20240416/stream_20240416_022351.txt",
    "results": {
        "Copy": {
            "best_rate": "8523.3 MB/s",
            "avg_time": "0.018898",
            "min_time": "0.018772",
            "max_time": "0.019016"
        },
        "Scale": {
            "best_rate": "8349.9 MB/s",
            "avg_time": "0.019590",
            "min_time": "0.019162",
            "max_time": "0.021867"
        },
        "Add": {
            "best_rate": "6211.3 MB/s",
            "avg_time": "0.039694",
            "min_time": "0.038639",
            "max_time": "0.046332"
        },
        "Triad": {
            "best_rate": "6282.4 MB/s",
            "avg_time": "0.039336",
            "min_time": "0.038202",
            "max_time": "0.046551"
        },
        "logs": "s3.dev.osssc.ac.cn/self-test/debugger/20240416/stream_log_20240416_022354.txt"
    },
    "skipped_cases": [],
    "skipped_case_num": 0,
    "end": "2024-04-16 02:23:55",
    "time_delta": 196.09306
}
```

# out.log
```log
-------------------------------------------------------------
STREAM version $Revision: 5.10 $
-------------------------------------------------------------
This system uses 8 bytes per array element.
-------------------------------------------------------------
Array size = 10000000 (elements), Offset = 0 (elements)
Memory per array = 76.3 MiB (= 0.1 GiB).
Total memory required = 228.9 MiB (= 0.2 GiB).
Each kernel will be executed 10 times.
 The *best* time for each kernel (excluding the first iteration)
 will be used to compute the reported bandwidth.
-------------------------------------------------------------
Number of Threads requested = 4
Number of Threads counted = 4
-------------------------------------------------------------
Your clock granularity/precision appears to be 1 microseconds.
Each test below will take on the order of 19845 microseconds.
   (= 19845 clock ticks)
Increase the size of the arrays if this shows that
you are not getting at least 20 clock ticks per test.
-------------------------------------------------------------
WARNING -- The above is only a rough guideline.
For best results, please be sure you know the
precision of your system timer.
-------------------------------------------------------------
Function    Best Rate MB/s  Avg time     Min time     Max time
Copy:            8523.3     0.018898     0.018772     0.019016
Scale:           8349.9     0.019590     0.019162     0.021867
Add:             6211.3     0.039694     0.038639     0.046332
Triad:           6282.4     0.039336     0.038202     0.046551
-------------------------------------------------------------
Solution Validates: avg error less than 1.000000e-13 on all three arrays
-------------------------------------------------------------
```
