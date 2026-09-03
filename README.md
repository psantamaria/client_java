# Prometheus Java Client Benchmarks

## Run Information

- **Date:** 2026-09-03T08:02:03Z
- **Commit:** [`4b69f40`](https://github.com/psantamaria/client_java/commit/4b69f40bd4e616d69468ce99dc4323162287a577)
- **JDK:** 25.0.2 (OpenJDK 64-Bit Server VM)
- **Benchmark config:** 3 fork(s), 3 warmup, 5 measurement, 4 threads
- **Hardware:** INTEL(R) XEON(R) PLATINUM 8573C, 4 cores, 16 GB RAM
- **OS:** Linux 6.17.0-1022-azure

## Results

### CounterBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| codahaleIncNoLabels | 26.79K | ± 143.42 | ops/s | **fastest** |
| prometheusNoLabelsInc | 25.76K | ± 191.44 | ops/s | 1.0x slower |
| prometheusInc | 25.57K | ± 291.72 | ops/s | 1.0x slower |
| prometheusAdd | 24.97K | ± 285.86 | ops/s | 1.1x slower |
| simpleclientInc | 6.48K | ± 61.88 | ops/s | 4.1x slower |
| simpleclientNoLabelsInc | 6.42K | ± 39.11 | ops/s | 4.2x slower |
| simpleclientAdd | 6.27K | ± 157.67 | ops/s | 4.3x slower |
| openTelemetryIncNoLabels | 1.06K | ± 110.63 | ops/s | 25x slower |
| openTelemetryAdd | 1.06K | ± 86.86 | ops/s | 25x slower |
| openTelemetryInc | 1.04K | ± 100.91 | ops/s | 26x slower |

### HistogramBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| simpleclient | 4.25K | ± 60.11 | ops/s | **fastest** |
| prometheusClassic | 3.49K | ± 1.33K | ops/s | 1.2x slower |
| prometheusNative | 2.11K | ± 110.21 | ops/s | 2.0x slower |
| openTelemetryClassic | 372.82 | ± 17.45 | ops/s | 11x slower |
| openTelemetryExponential | 318.33 | ± 12.31 | ops/s | 13x slower |

### TextFormatUtilBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusWriteToNull | 287.99K | ± 1.38K | ops/s | **fastest** |
| prometheusWriteToByteArray | 287.30K | ± 1.61K | ops/s | 1.0x slower |
| openMetricsWriteToNull | 270.09K | ± 1.51K | ops/s | 1.1x slower |
| openMetricsWriteToByteArray | 268.12K | ± 1.08K | ops/s | 1.1x slower |

### Raw Results

```
Benchmark                                            Mode  Cnt          Score        Error  Units
CounterBenchmark.codahaleIncNoLabels                thrpt   15      26792.723    ± 143.418  ops/s
CounterBenchmark.openTelemetryAdd                   thrpt   15       1058.797     ± 86.863  ops/s
CounterBenchmark.openTelemetryInc                   thrpt   15       1042.793    ± 100.906  ops/s
CounterBenchmark.openTelemetryIncNoLabels           thrpt   15       1064.668    ± 110.634  ops/s
CounterBenchmark.prometheusAdd                      thrpt   15      24966.753    ± 285.857  ops/s
CounterBenchmark.prometheusInc                      thrpt   15      25573.817    ± 291.716  ops/s
CounterBenchmark.prometheusNoLabelsInc              thrpt   15      25757.101    ± 191.437  ops/s
CounterBenchmark.simpleclientAdd                    thrpt   15       6266.737    ± 157.668  ops/s
CounterBenchmark.simpleclientInc                    thrpt   15       6475.814     ± 61.878  ops/s
CounterBenchmark.simpleclientNoLabelsInc            thrpt   15       6417.138     ± 39.115  ops/s
HistogramBenchmark.openTelemetryClassic             thrpt   15        372.821     ± 17.452  ops/s
HistogramBenchmark.openTelemetryExponential         thrpt   15        318.334     ± 12.313  ops/s
HistogramBenchmark.prometheusClassic                thrpt   15       3492.847   ± 1327.640  ops/s
HistogramBenchmark.prometheusNative                 thrpt   15       2114.863    ± 110.206  ops/s
HistogramBenchmark.simpleclient                     thrpt   15       4251.957     ± 60.107  ops/s
TextFormatUtilBenchmark.openMetricsWriteToByteArray  thrpt   15     268116.537   ± 1083.579  ops/s
TextFormatUtilBenchmark.openMetricsWriteToNull      thrpt   15     270088.078   ± 1506.918  ops/s
TextFormatUtilBenchmark.prometheusWriteToByteArray  thrpt   15     287304.028   ± 1609.916  ops/s
TextFormatUtilBenchmark.prometheusWriteToNull       thrpt   15     287987.843   ± 1384.038  ops/s
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
