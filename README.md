# Prometheus Java Client Benchmarks

## Run Information

- **Date:** 2026-10-06T09:43:06Z
- **Commit:** [`4b69f40`](https://github.com/psantamaria/client_java/commit/4b69f40bd4e616d69468ce99dc4323162287a577)
- **JDK:** 25.0.2 (OpenJDK 64-Bit Server VM)
- **Benchmark config:** 3 fork(s), 3 warmup, 5 measurement, 4 threads
- **Hardware:** AMD EPYC 7763 64-Core Processor, 4 cores, 16 GB RAM
- **OS:** Linux 6.17.0-1022-azure

## Results

### CounterBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusInc | 65.29K | ± 1.20K | ops/s | **fastest** |
| prometheusNoLabelsInc | 56.12K | ± 1.24K | ops/s | 1.2x slower |
| prometheusAdd | 51.21K | ± 425.08 | ops/s | 1.3x slower |
| codahaleIncNoLabels | 44.10K | ± 8.13K | ops/s | 1.5x slower |
| simpleclientInc | 6.47K | ± 272.58 | ops/s | 10x slower |
| simpleclientNoLabelsInc | 6.43K | ± 162.10 | ops/s | 10x slower |
| simpleclientAdd | 6.16K | ± 239.28 | ops/s | 11x slower |
| openTelemetryAdd | 1.47K | ± 271.03 | ops/s | 44x slower |
| openTelemetryInc | 1.22K | ± 52.76 | ops/s | 53x slower |
| openTelemetryIncNoLabels | 1.04K | ± 62.21 | ops/s | 63x slower |

### HistogramBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusClassic | 5.32K | ± 1.91K | ops/s | **fastest** |
| simpleclient | 4.48K | ± 42.74 | ops/s | 1.2x slower |
| prometheusNative | 2.46K | ± 202.85 | ops/s | 2.2x slower |
| openTelemetryClassic | 646.06 | ± 40.73 | ops/s | 8.2x slower |
| openTelemetryExponential | 571.86 | ± 26.36 | ops/s | 9.3x slower |

### TextFormatUtilBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusWriteToByteArray | 455.24K | ± 4.65K | ops/s | **fastest** |
| prometheusWriteToNull | 454.95K | ± 5.27K | ops/s | 1.0x slower |
| openMetricsWriteToNull | 449.64K | ± 1.50K | ops/s | 1.0x slower |
| openMetricsWriteToByteArray | 444.91K | ± 5.97K | ops/s | 1.0x slower |

### Raw Results

```
Benchmark                                            Mode  Cnt          Score        Error  Units
CounterBenchmark.codahaleIncNoLabels                thrpt   15      44104.507   ± 8127.764  ops/s
CounterBenchmark.openTelemetryAdd                   thrpt   15       1471.516    ± 271.031  ops/s
CounterBenchmark.openTelemetryInc                   thrpt   15       1221.447     ± 52.761  ops/s
CounterBenchmark.openTelemetryIncNoLabels           thrpt   15       1043.543     ± 62.209  ops/s
CounterBenchmark.prometheusAdd                      thrpt   15      51207.621    ± 425.082  ops/s
CounterBenchmark.prometheusInc                      thrpt   15      65293.944   ± 1204.739  ops/s
CounterBenchmark.prometheusNoLabelsInc              thrpt   15      56124.712   ± 1240.275  ops/s
CounterBenchmark.simpleclientAdd                    thrpt   15       6163.394    ± 239.282  ops/s
CounterBenchmark.simpleclientInc                    thrpt   15       6473.072    ± 272.577  ops/s
CounterBenchmark.simpleclientNoLabelsInc            thrpt   15       6431.998    ± 162.096  ops/s
HistogramBenchmark.openTelemetryClassic             thrpt   15        646.060     ± 40.726  ops/s
HistogramBenchmark.openTelemetryExponential         thrpt   15        571.856     ± 26.362  ops/s
HistogramBenchmark.prometheusClassic                thrpt   15       5320.188   ± 1905.419  ops/s
HistogramBenchmark.prometheusNative                 thrpt   15       2456.794    ± 202.855  ops/s
HistogramBenchmark.simpleclient                     thrpt   15       4479.699     ± 42.743  ops/s
TextFormatUtilBenchmark.openMetricsWriteToByteArray  thrpt   15     444914.382   ± 5969.090  ops/s
TextFormatUtilBenchmark.openMetricsWriteToNull      thrpt   15     449635.722   ± 1496.636  ops/s
TextFormatUtilBenchmark.prometheusWriteToByteArray  thrpt   15     455235.388   ± 4651.094  ops/s
TextFormatUtilBenchmark.prometheusWriteToNull       thrpt   15     454948.647   ± 5266.311  ops/s
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
