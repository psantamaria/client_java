# Prometheus Java Client Benchmarks

## Run Information

- **Date:** 2026-08-11T04:54:19Z
- **Commit:** [`4b69f40`](https://github.com/psantamaria/client_java/commit/4b69f40bd4e616d69468ce99dc4323162287a577)
- **JDK:** 25.0.2 (OpenJDK 64-Bit Server VM)
- **Benchmark config:** 3 fork(s), 3 warmup, 5 measurement, 4 threads
- **Hardware:** INTEL(R) XEON(R) PLATINUM 8573C, 4 cores, 16 GB RAM
- **OS:** Linux 6.17.0-1020-azure

## Results

### CounterBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusNoLabelsInc | 30.13K | ± 169.07 | ops/s | **fastest** |
| prometheusInc | 30.01K | ± 268.44 | ops/s | 1.0x slower |
| codahaleIncNoLabels | 29.84K | ± 1.92K | ops/s | 1.0x slower |
| prometheusAdd | 29.38K | ± 281.76 | ops/s | 1.0x slower |
| simpleclientInc | 7.57K | ± 78.77 | ops/s | 4.0x slower |
| simpleclientNoLabelsInc | 7.52K | ± 72.93 | ops/s | 4.0x slower |
| simpleclientAdd | 7.47K | ± 139.68 | ops/s | 4.0x slower |
| openTelemetryAdd | 1.28K | ± 101.12 | ops/s | 23x slower |
| openTelemetryInc | 1.22K | ± 8.77 | ops/s | 25x slower |
| openTelemetryIncNoLabels | 1.17K | ± 59.12 | ops/s | 26x slower |

### HistogramBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| simpleclient | 4.91K | ± 54.99 | ops/s | **fastest** |
| prometheusClassic | 2.64K | ± 248.51 | ops/s | 1.9x slower |
| prometheusNative | 2.31K | ± 330.77 | ops/s | 2.1x slower |
| openTelemetryClassic | 383.93 | ± 16.44 | ops/s | 13x slower |
| openTelemetryExponential | 336.29 | ± 14.13 | ops/s | 15x slower |

### TextFormatUtilBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusWriteToNull | 318.89K | ± 7.00K | ops/s | **fastest** |
| prometheusWriteToByteArray | 314.40K | ± 4.28K | ops/s | 1.0x slower |
| openMetricsWriteToByteArray | 297.51K | ± 3.05K | ops/s | 1.1x slower |
| openMetricsWriteToNull | 296.36K | ± 3.16K | ops/s | 1.1x slower |

### Raw Results

```
Benchmark                                            Mode  Cnt          Score        Error  Units
CounterBenchmark.codahaleIncNoLabels                thrpt   15      29837.256   ± 1922.070  ops/s
CounterBenchmark.openTelemetryAdd                   thrpt   15       1283.964    ± 101.119  ops/s
CounterBenchmark.openTelemetryInc                   thrpt   15       1224.249      ± 8.768  ops/s
CounterBenchmark.openTelemetryIncNoLabels           thrpt   15       1171.892     ± 59.122  ops/s
CounterBenchmark.prometheusAdd                      thrpt   15      29378.402    ± 281.762  ops/s
CounterBenchmark.prometheusInc                      thrpt   15      30008.691    ± 268.435  ops/s
CounterBenchmark.prometheusNoLabelsInc              thrpt   15      30134.066    ± 169.072  ops/s
CounterBenchmark.simpleclientAdd                    thrpt   15       7474.521    ± 139.685  ops/s
CounterBenchmark.simpleclientInc                    thrpt   15       7571.960     ± 78.770  ops/s
CounterBenchmark.simpleclientNoLabelsInc            thrpt   15       7523.678     ± 72.926  ops/s
HistogramBenchmark.openTelemetryClassic             thrpt   15        383.931     ± 16.438  ops/s
HistogramBenchmark.openTelemetryExponential         thrpt   15        336.288     ± 14.134  ops/s
HistogramBenchmark.prometheusClassic                thrpt   15       2639.897    ± 248.510  ops/s
HistogramBenchmark.prometheusNative                 thrpt   15       2307.895    ± 330.769  ops/s
HistogramBenchmark.simpleclient                     thrpt   15       4914.873     ± 54.989  ops/s
TextFormatUtilBenchmark.openMetricsWriteToByteArray  thrpt   15     297507.912   ± 3047.672  ops/s
TextFormatUtilBenchmark.openMetricsWriteToNull      thrpt   15     296363.262   ± 3160.328  ops/s
TextFormatUtilBenchmark.prometheusWriteToByteArray  thrpt   15     314403.292   ± 4279.681  ops/s
TextFormatUtilBenchmark.prometheusWriteToNull       thrpt   15     318891.306   ± 7000.566  ops/s
```

## Notes

- **Score** = Throughput in operations per second (higher is better)
- **Error** = 99.9% confidence interval

## Benchmark Descriptions

| Benchmark | Description |
|:----------|:------------|
| **CounterBenchmark** | Counter increment performance: Prometheus, OpenTelemetry, simpleclient, Codahale |
| **HistogramBenchmark** | Histogram observation performance (classic vs native/exponential) |
| **TextFormatUtilBenchmark** | Metric exposition format writing speed |
