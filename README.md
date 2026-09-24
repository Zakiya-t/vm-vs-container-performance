# VM vs Container Performance Experiment

A controlled performance comparison between an Ubuntu virtual machine running under VMware and a Docker container with closely matched CPU and memory limits.

## Objective

The experiment compares:

- CPU performance
- CPU scalability
- Memory throughput
- Disk bandwidth and IOPS
- Network throughput
- Application throughput and latency
- Application startup time
- API scalability

## Experimental Environment

### Virtual Machine

- Platform: VMware
- vCPU: 4
- RAM: approximately 4.8 GiB
- Swap: 4 GiB

### Docker Container

- CPU limit: 4 CPUs
- Memory limit: 5101731840 bytes (~4.75 GiB)
- Docker image: vm-container-benchmark

## Benchmark Workloads

### CPU
Sysbench was used with 4 threads and a prime limit of 20000.
Ten repeated runs were collected for both environments.

CPU scalability was tested using 1, 2, 4 and 8 threads.

### Memory
Memory throughput was measured over ten runs.

The workload was:
- Block size: 1 MiB
- Total size: 2 GiB
- Threads: 4

The 2 GiB workload was used because the VM had approximately 4.8 GiB RAM.

### Disk
fio was used for:
- Sequential read
- Sequential write
- Random read
- Random write

Both bandwidth and IOPS were recorded.

### Network
iperf3 was used for two tests:
- iperf3
- iperf3_P4

These measurements represent the configured local/virtual network path.

### Application
ApacheBench was used for:
- health
- compute

Metrics:
- Requests per second
- Mean time per request

### Startup
Application-ready time was measured over five runs.

### API Scalability
Workload levels of 1, 2, 4 and 8 were tested.

Metrics:
- Requests per second
- Average latency

## Results

### Average CPU Performance

| System | Events/sec |
|---|---:|
| VM | 5522.52 |
| Container | 5552.60 |

### Average Memory Performance

| System | MiB/sec |
|---|---:|
| VM | 66625.29 |
| Container | 46467.34 |

### Average Startup Time

| System | Milliseconds |
|---|---:|
| VM | 350.00 |
| Container | 635.00 |

### Application Results

| Endpoint | Metric | VM | Container |
|---|---|---:|---:|
| health | Requests/sec | 2212.07 | 2496.18 |
| health | Latency (ms) | 45.21 | 40.06 |
| compute | Requests/sec | 34.94 | 30.84 |
| compute | Latency (ms) | 286.20 | 324.28 |

## Project Structure

```text
vm-vs-container-performance/
├── analysis/
├── docs/
├── results/
│   ├── raw/
│   ├── processed/
│   └── figures/
└── README.md
