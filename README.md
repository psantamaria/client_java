# Prometheus Java Client Benchmarks

## Run Information

- **Date:** 2026-05-21T07:22:09Z
- **Commit:** [`4b69f40`](https://github.com/psantamaria/client_java/commit/4b69f40bd4e616d69468ce99dc4323162287a577)
- **JDK:** 25.0.2 (OpenJDK 64-Bit Server VM)
- **Benchmark config:** 3 fork(s), 3 warmup, 5 measurement, 4 threads
- **Hardware:** Intel(R) Xeon(R) Platinum 8370C CPU @ 2.80GHz, 4 cores, 16 GB RAM
- **OS:** Linux 6.17.0-1013-azure

## Results

### CounterBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusInc | 31.55K | ± 40.79 | ops/s | **fastest** |
| prometheusNoLabelsInc | 29.65K | ± 823.58 | ops/s | 1.1x slower |
| codahaleIncNoLabels | 28.52K | ± 512.86 | ops/s | 1.1x slower |
| prometheusAdd | 28.51K | ± 82.05 | ops/s | 1.1x slower |
| simpleclientInc | 6.92K | ± 32.16 | ops/s | 4.6x slower |
| simpleclientNoLabelsInc | 6.75K | ± 257.28 | ops/s | 4.7x slower |
| simpleclientAdd | 6.27K | ± 100.90 | ops/s | 5.0x slower |
| openTelemetryIncNoLabels | 1.41K | ± 90.08 | ops/s | 22x slower |
| openTelemetryAdd | 1.33K | ± 38.19 | ops/s | 24x slower |
| openTelemetryInc | 1.29K | ± 23.63 | ops/s | 24x slower |

### HistogramBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| simpleclient | 4.50K | ± 15.46 | ops/s | **fastest** |
| prometheusClassic | 2.73K | ± 179.27 | ops/s | 1.6x slower |
| prometheusNative | 2.05K | ± 247.42 | ops/s | 2.2x slower |
| openTelemetryClassic | 507.07 | ± 8.52 | ops/s | 8.9x slower |
| openTelemetryExponential | 392.30 | ± 15.33 | ops/s | 11x slower |

### TextFormatUtilBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusWriteToNull | 316.64K | ± 1.43K | ops/s | **fastest** |
| prometheusWriteToByteArray | 312.87K | ± 2.42K | ops/s | 1.0x slower |
| openMetricsWriteToNull | 297.97K | ± 2.52K | ops/s | 1.1x slower |
| openMetricsWriteToByteArray | 294.50K | ± 2.87K | ops/s | 1.1x slower |

### Raw Results

```
Benchmark                                            Mode  Cnt          Score        Error  Units
CounterBenchmark.codahaleIncNoLabels                thrpt   15      28519.720    ± 512.863  ops/s
CounterBenchmark.openTelemetryAdd                   thrpt   15       1332.426     ± 38.191  ops/s
CounterBenchmark.openTelemetryInc                   thrpt   15       1291.095     ± 23.627  ops/s
CounterBenchmark.openTelemetryIncNoLabels           thrpt   15       1405.818     ± 90.081  ops/s
CounterBenchmark.prometheusAdd                      thrpt   15      28505.585     ± 82.048  ops/s
CounterBenchmark.prometheusInc                      thrpt   15      31551.203     ± 40.794  ops/s
CounterBenchmark.prometheusNoLabelsInc              thrpt   15      29646.152    ± 823.584  ops/s
CounterBenchmark.simpleclientAdd                    thrpt   15       6273.871    ± 100.901  ops/s
CounterBenchmark.simpleclientInc                    thrpt   15       6920.897     ± 32.158  ops/s
CounterBenchmark.simpleclientNoLabelsInc            thrpt   15       6748.867    ± 257.277  ops/s
HistogramBenchmark.openTelemetryClassic             thrpt   15        507.069      ± 8.518  ops/s
HistogramBenchmark.openTelemetryExponential         thrpt   15        392.304     ± 15.334  ops/s
HistogramBenchmark.prometheusClassic                thrpt   15       2729.139    ± 179.271  ops/s
HistogramBenchmark.prometheusNative                 thrpt   15       2053.817    ± 247.416  ops/s
HistogramBenchmark.simpleclient                     thrpt   15       4498.843     ± 15.465  ops/s
TextFormatUtilBenchmark.openMetricsWriteToByteArray  thrpt   15     294501.404   ± 2865.980  ops/s
TextFormatUtilBenchmark.openMetricsWriteToNull      thrpt   15     297968.993   ± 2519.340  ops/s
TextFormatUtilBenchmark.prometheusWriteToByteArray  thrpt   15     312868.798   ± 2415.586  ops/s
TextFormatUtilBenchmark.prometheusWriteToNull       thrpt   15     316644.621   ± 1426.469  ops/s
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
