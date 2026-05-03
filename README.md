# Prometheus Java Client Benchmarks

## Run Information

- **Date:** 2026-05-03T06:43:23Z
- **Commit:** [`4b69f40`](https://github.com/psantamaria/client_java/commit/4b69f40bd4e616d69468ce99dc4323162287a577)
- **JDK:** 25.0.2 (OpenJDK 64-Bit Server VM)
- **Benchmark config:** 3 fork(s), 3 warmup, 5 measurement, 4 threads
- **Hardware:** AMD EPYC 9V74 80-Core Processor, 4 cores, 16 GB RAM
- **OS:** Linux 6.17.0-1010-azure

## Results

### CounterBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusInc | 59.95K | ± 34.28 | ops/s | **fastest** |
| prometheusNoLabelsInc | 51.63K | ± 521.06 | ops/s | 1.2x slower |
| prometheusAdd | 45.38K | ± 3.44K | ops/s | 1.3x slower |
| codahaleIncNoLabels | 44.15K | ± 241.15 | ops/s | 1.4x slower |
| simpleclientInc | 6.31K | ± 34.45 | ops/s | 9.5x slower |
| simpleclientNoLabelsInc | 5.95K | ± 236.78 | ops/s | 10x slower |
| simpleclientAdd | 5.92K | ± 275.14 | ops/s | 10x slower |
| openTelemetryInc | 1.37K | ± 77.65 | ops/s | 44x slower |
| openTelemetryAdd | 1.31K | ± 22.03 | ops/s | 46x slower |
| openTelemetryIncNoLabels | 1.20K | ± 40.27 | ops/s | 50x slower |

### HistogramBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusClassic | 7.23K | ± 3.05K | ops/s | **fastest** |
| simpleclient | 4.52K | ± 21.09 | ops/s | 1.6x slower |
| prometheusNative | 3.14K | ± 34.33 | ops/s | 2.3x slower |
| openTelemetryClassic | 642.29 | ± 22.86 | ops/s | 11x slower |
| openTelemetryExponential | 517.57 | ± 22.02 | ops/s | 14x slower |

### TextFormatUtilBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusWriteToNull | 554.38K | ± 2.74K | ops/s | **fastest** |
| prometheusWriteToByteArray | 549.99K | ± 4.33K | ops/s | 1.0x slower |
| openMetricsWriteToNull | 537.15K | ± 3.77K | ops/s | 1.0x slower |
| openMetricsWriteToByteArray | 531.10K | ± 3.83K | ops/s | 1.0x slower |

### Raw Results

```
Benchmark                                            Mode  Cnt          Score        Error  Units
CounterBenchmark.codahaleIncNoLabels                thrpt   15      44147.514    ± 241.154  ops/s
CounterBenchmark.openTelemetryAdd                   thrpt   15       1314.116     ± 22.026  ops/s
CounterBenchmark.openTelemetryInc                   thrpt   15       1366.266     ± 77.646  ops/s
CounterBenchmark.openTelemetryIncNoLabels           thrpt   15       1195.757     ± 40.275  ops/s
CounterBenchmark.prometheusAdd                      thrpt   15      45384.117   ± 3443.931  ops/s
CounterBenchmark.prometheusInc                      thrpt   15      59948.077     ± 34.285  ops/s
CounterBenchmark.prometheusNoLabelsInc              thrpt   15      51627.300    ± 521.059  ops/s
CounterBenchmark.simpleclientAdd                    thrpt   15       5918.226    ± 275.138  ops/s
CounterBenchmark.simpleclientInc                    thrpt   15       6307.163     ± 34.445  ops/s
CounterBenchmark.simpleclientNoLabelsInc            thrpt   15       5949.176    ± 236.778  ops/s
HistogramBenchmark.openTelemetryClassic             thrpt   15        642.291     ± 22.856  ops/s
HistogramBenchmark.openTelemetryExponential         thrpt   15        517.573     ± 22.018  ops/s
HistogramBenchmark.prometheusClassic                thrpt   15       7226.946   ± 3046.739  ops/s
HistogramBenchmark.prometheusNative                 thrpt   15       3143.394     ± 34.329  ops/s
HistogramBenchmark.simpleclient                     thrpt   15       4519.182     ± 21.091  ops/s
TextFormatUtilBenchmark.openMetricsWriteToByteArray  thrpt   15     531100.762   ± 3828.998  ops/s
TextFormatUtilBenchmark.openMetricsWriteToNull      thrpt   15     537152.307   ± 3768.237  ops/s
TextFormatUtilBenchmark.prometheusWriteToByteArray  thrpt   15     549994.314   ± 4333.673  ops/s
TextFormatUtilBenchmark.prometheusWriteToNull       thrpt   15     554382.024   ± 2742.786  ops/s
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
