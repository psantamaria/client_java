# Prometheus Java Client Benchmarks

## Run Information

- **Date:** 2026-06-08T07:55:00Z
- **Commit:** [`4b69f40`](https://github.com/psantamaria/client_java/commit/4b69f40bd4e616d69468ce99dc4323162287a577)
- **JDK:** 25.0.2 (OpenJDK 64-Bit Server VM)
- **Benchmark config:** 3 fork(s), 3 warmup, 5 measurement, 4 threads
- **Hardware:** AMD EPYC 7763 64-Core Processor, 4 cores, 16 GB RAM
- **OS:** Linux 6.17.0-1015-azure

## Results

### CounterBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusInc | 65.50K | ± 1.56K | ops/s | **fastest** |
| prometheusNoLabelsInc | 57.24K | ± 188.05 | ops/s | 1.1x slower |
| prometheusAdd | 51.27K | ± 98.50 | ops/s | 1.3x slower |
| codahaleIncNoLabels | 48.25K | ± 1.78K | ops/s | 1.4x slower |
| simpleclientNoLabelsInc | 6.61K | ± 12.98 | ops/s | 9.9x slower |
| simpleclientInc | 6.50K | ± 264.74 | ops/s | 10x slower |
| simpleclientAdd | 6.29K | ± 267.86 | ops/s | 10x slower |
| openTelemetryAdd | 1.40K | ± 294.95 | ops/s | 47x slower |
| openTelemetryInc | 1.39K | ± 205.16 | ops/s | 47x slower |
| openTelemetryIncNoLabels | 1.27K | ± 41.67 | ops/s | 52x slower |

### HistogramBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusClassic | 5.90K | ± 1.03K | ops/s | **fastest** |
| simpleclient | 4.44K | ± 65.99 | ops/s | 1.3x slower |
| prometheusNative | 2.99K | ± 350.45 | ops/s | 2.0x slower |
| openTelemetryClassic | 704.42 | ± 19.68 | ops/s | 8.4x slower |
| openTelemetryExponential | 587.20 | ± 20.01 | ops/s | 10x slower |

### TextFormatUtilBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| openMetricsWriteToNull | 497.17K | ± 1.70K | ops/s | **fastest** |
| prometheusWriteToNull | 495.99K | ± 2.30K | ops/s | 1.0x slower |
| prometheusWriteToByteArray | 491.75K | ± 3.52K | ops/s | 1.0x slower |
| openMetricsWriteToByteArray | 490.84K | ± 4.08K | ops/s | 1.0x slower |

### Raw Results

```
Benchmark                                            Mode  Cnt          Score        Error  Units
CounterBenchmark.codahaleIncNoLabels                thrpt   15      48254.452   ± 1781.728  ops/s
CounterBenchmark.openTelemetryAdd                   thrpt   15       1400.933    ± 294.947  ops/s
CounterBenchmark.openTelemetryInc                   thrpt   15       1389.651    ± 205.157  ops/s
CounterBenchmark.openTelemetryIncNoLabels           thrpt   15       1271.798     ± 41.668  ops/s
CounterBenchmark.prometheusAdd                      thrpt   15      51266.532     ± 98.504  ops/s
CounterBenchmark.prometheusInc                      thrpt   15      65499.924   ± 1559.127  ops/s
CounterBenchmark.prometheusNoLabelsInc              thrpt   15      57238.804    ± 188.047  ops/s
CounterBenchmark.simpleclientAdd                    thrpt   15       6292.393    ± 267.863  ops/s
CounterBenchmark.simpleclientInc                    thrpt   15       6499.284    ± 264.737  ops/s
CounterBenchmark.simpleclientNoLabelsInc            thrpt   15       6612.371     ± 12.976  ops/s
HistogramBenchmark.openTelemetryClassic             thrpt   15        704.421     ± 19.677  ops/s
HistogramBenchmark.openTelemetryExponential         thrpt   15        587.196     ± 20.008  ops/s
HistogramBenchmark.prometheusClassic                thrpt   15       5895.316   ± 1025.659  ops/s
HistogramBenchmark.prometheusNative                 thrpt   15       2991.371    ± 350.452  ops/s
HistogramBenchmark.simpleclient                     thrpt   15       4435.208     ± 65.991  ops/s
TextFormatUtilBenchmark.openMetricsWriteToByteArray  thrpt   15     490839.325   ± 4075.021  ops/s
TextFormatUtilBenchmark.openMetricsWriteToNull      thrpt   15     497170.348   ± 1696.474  ops/s
TextFormatUtilBenchmark.prometheusWriteToByteArray  thrpt   15     491748.985   ± 3522.905  ops/s
TextFormatUtilBenchmark.prometheusWriteToNull       thrpt   15     495993.254   ± 2298.789  ops/s
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
