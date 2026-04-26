# Prometheus Java Client Benchmarks

## Run Information

- **Date:** 2026-04-26T06:12:27Z
- **Commit:** [`4b69f40`](https://github.com/psantamaria/client_java/commit/4b69f40bd4e616d69468ce99dc4323162287a577)
- **JDK:** 25.0.2 (OpenJDK 64-Bit Server VM)
- **Benchmark config:** 3 fork(s), 3 warmup, 5 measurement, 4 threads
- **Hardware:** Intel(R) Xeon(R) Platinum 8370C CPU @ 2.80GHz, 4 cores, 16 GB RAM
- **OS:** Linux 6.17.0-1010-azure

## Results

### CounterBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusNoLabelsInc | 30.48K | ± 1.03K | ops/s | **fastest** |
| prometheusInc | 30.35K | ± 1.24K | ops/s | 1.0x slower |
| codahaleIncNoLabels | 29.26K | ± 967.71 | ops/s | 1.0x slower |
| prometheusAdd | 28.01K | ± 766.37 | ops/s | 1.1x slower |
| simpleclientInc | 6.93K | ± 40.37 | ops/s | 4.4x slower |
| simpleclientNoLabelsInc | 6.89K | ± 41.26 | ops/s | 4.4x slower |
| simpleclientAdd | 6.56K | ± 159.04 | ops/s | 4.6x slower |
| openTelemetryIncNoLabels | 1.40K | ± 111.05 | ops/s | 22x slower |
| openTelemetryAdd | 1.36K | ± 53.58 | ops/s | 22x slower |
| openTelemetryInc | 1.30K | ± 58.74 | ops/s | 23x slower |

### HistogramBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| simpleclient | 4.41K | ± 49.05 | ops/s | **fastest** |
| prometheusClassic | 3.05K | ± 471.79 | ops/s | 1.4x slower |
| prometheusNative | 2.17K | ± 113.99 | ops/s | 2.0x slower |
| openTelemetryClassic | 521.69 | ± 18.63 | ops/s | 8.5x slower |
| openTelemetryExponential | 395.88 | ± 4.21 | ops/s | 11x slower |

### TextFormatUtilBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusWriteToNull | 316.57K | ± 2.19K | ops/s | **fastest** |
| prometheusWriteToByteArray | 312.40K | ± 2.42K | ops/s | 1.0x slower |
| openMetricsWriteToNull | 297.87K | ± 1.42K | ops/s | 1.1x slower |
| openMetricsWriteToByteArray | 294.51K | ± 3.23K | ops/s | 1.1x slower |

### Raw Results

```
Benchmark                                            Mode  Cnt          Score        Error  Units
CounterBenchmark.codahaleIncNoLabels                thrpt   15      29259.345    ± 967.709  ops/s
CounterBenchmark.openTelemetryAdd                   thrpt   15       1364.447     ± 53.584  ops/s
CounterBenchmark.openTelemetryInc                   thrpt   15       1300.257     ± 58.743  ops/s
CounterBenchmark.openTelemetryIncNoLabels           thrpt   15       1398.624    ± 111.052  ops/s
CounterBenchmark.prometheusAdd                      thrpt   15      28007.908    ± 766.370  ops/s
CounterBenchmark.prometheusInc                      thrpt   15      30346.319   ± 1243.651  ops/s
CounterBenchmark.prometheusNoLabelsInc              thrpt   15      30484.159   ± 1033.318  ops/s
CounterBenchmark.simpleclientAdd                    thrpt   15       6562.535    ± 159.041  ops/s
CounterBenchmark.simpleclientInc                    thrpt   15       6927.820     ± 40.373  ops/s
CounterBenchmark.simpleclientNoLabelsInc            thrpt   15       6893.238     ± 41.257  ops/s
HistogramBenchmark.openTelemetryClassic             thrpt   15        521.689     ± 18.630  ops/s
HistogramBenchmark.openTelemetryExponential         thrpt   15        395.880      ± 4.207  ops/s
HistogramBenchmark.prometheusClassic                thrpt   15       3046.788    ± 471.795  ops/s
HistogramBenchmark.prometheusNative                 thrpt   15       2169.977    ± 113.987  ops/s
HistogramBenchmark.simpleclient                     thrpt   15       4412.283     ± 49.048  ops/s
TextFormatUtilBenchmark.openMetricsWriteToByteArray  thrpt   15     294505.652   ± 3230.907  ops/s
TextFormatUtilBenchmark.openMetricsWriteToNull      thrpt   15     297868.575   ± 1422.195  ops/s
TextFormatUtilBenchmark.prometheusWriteToByteArray  thrpt   15     312397.576   ± 2418.307  ops/s
TextFormatUtilBenchmark.prometheusWriteToNull       thrpt   15     316567.873   ± 2187.042  ops/s
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
