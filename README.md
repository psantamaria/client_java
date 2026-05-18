# Prometheus Java Client Benchmarks

## Run Information

- **Date:** 2026-05-18T07:25:10Z
- **Commit:** [`4b69f40`](https://github.com/psantamaria/client_java/commit/4b69f40bd4e616d69468ce99dc4323162287a577)
- **JDK:** 25.0.2 (OpenJDK 64-Bit Server VM)
- **Benchmark config:** 3 fork(s), 3 warmup, 5 measurement, 4 threads
- **Hardware:** AMD EPYC 9V74 80-Core Processor, 4 cores, 16 GB RAM
- **OS:** Linux 6.17.0-1013-azure

## Results

### CounterBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusInc | 60.38K | ± 1.74K | ops/s | **fastest** |
| prometheusNoLabelsInc | 52.10K | ± 958.26 | ops/s | 1.2x slower |
| prometheusAdd | 48.44K | ± 1.73K | ops/s | 1.2x slower |
| codahaleIncNoLabels | 44.33K | ± 845.81 | ops/s | 1.4x slower |
| simpleclientNoLabelsInc | 6.13K | ± 264.09 | ops/s | 9.8x slower |
| simpleclientInc | 6.11K | ± 247.35 | ops/s | 9.9x slower |
| simpleclientAdd | 5.89K | ± 239.63 | ops/s | 10x slower |
| openTelemetryIncNoLabels | 1.54K | ± 123.19 | ops/s | 39x slower |
| openTelemetryAdd | 1.47K | ± 104.70 | ops/s | 41x slower |
| openTelemetryInc | 1.46K | ± 100.07 | ops/s | 41x slower |

### HistogramBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusClassic | 5.11K | ± 761.86 | ops/s | **fastest** |
| simpleclient | 4.32K | ± 48.24 | ops/s | 1.2x slower |
| prometheusNative | 2.95K | ± 230.68 | ops/s | 1.7x slower |
| openTelemetryClassic | 617.77 | ± 7.31 | ops/s | 8.3x slower |
| openTelemetryExponential | 536.61 | ± 35.08 | ops/s | 9.5x slower |

### TextFormatUtilBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusWriteToNull | 553.53K | ± 5.68K | ops/s | **fastest** |
| prometheusWriteToByteArray | 540.90K | ± 3.48K | ops/s | 1.0x slower |
| openMetricsWriteToNull | 539.19K | ± 6.92K | ops/s | 1.0x slower |
| openMetricsWriteToByteArray | 520.91K | ± 5.10K | ops/s | 1.1x slower |

### Raw Results

```
Benchmark                                            Mode  Cnt          Score        Error  Units
CounterBenchmark.codahaleIncNoLabels                thrpt   15      44331.919    ± 845.813  ops/s
CounterBenchmark.openTelemetryAdd                   thrpt   15       1465.139    ± 104.702  ops/s
CounterBenchmark.openTelemetryInc                   thrpt   15       1464.885    ± 100.070  ops/s
CounterBenchmark.openTelemetryIncNoLabels           thrpt   15       1541.263    ± 123.191  ops/s
CounterBenchmark.prometheusAdd                      thrpt   15      48443.649   ± 1732.512  ops/s
CounterBenchmark.prometheusInc                      thrpt   15      60383.134   ± 1739.303  ops/s
CounterBenchmark.prometheusNoLabelsInc              thrpt   15      52104.790    ± 958.258  ops/s
CounterBenchmark.simpleclientAdd                    thrpt   15       5885.843    ± 239.629  ops/s
CounterBenchmark.simpleclientInc                    thrpt   15       6106.492    ± 247.350  ops/s
CounterBenchmark.simpleclientNoLabelsInc            thrpt   15       6130.779    ± 264.094  ops/s
HistogramBenchmark.openTelemetryClassic             thrpt   15        617.766      ± 7.314  ops/s
HistogramBenchmark.openTelemetryExponential         thrpt   15        536.612     ± 35.081  ops/s
HistogramBenchmark.prometheusClassic                thrpt   15       5111.476    ± 761.857  ops/s
HistogramBenchmark.prometheusNative                 thrpt   15       2953.438    ± 230.681  ops/s
HistogramBenchmark.simpleclient                     thrpt   15       4316.734     ± 48.241  ops/s
TextFormatUtilBenchmark.openMetricsWriteToByteArray  thrpt   15     520909.762   ± 5099.071  ops/s
TextFormatUtilBenchmark.openMetricsWriteToNull      thrpt   15     539191.309   ± 6919.387  ops/s
TextFormatUtilBenchmark.prometheusWriteToByteArray  thrpt   15     540898.793   ± 3479.707  ops/s
TextFormatUtilBenchmark.prometheusWriteToNull       thrpt   15     553529.552   ± 5677.129  ops/s
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
