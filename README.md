# Prometheus Java Client Benchmarks

## Run Information

- **Date:** 2026-04-21T06:02:26Z
- **Commit:** [`4b69f40`](https://github.com/psantamaria/client_java/commit/4b69f40bd4e616d69468ce99dc4323162287a577)
- **JDK:** 25.0.2 (OpenJDK 64-Bit Server VM)
- **Benchmark config:** 3 fork(s), 3 warmup, 5 measurement, 4 threads
- **Hardware:** AMD EPYC 9V74 80-Core Processor, 4 cores, 16 GB RAM
- **OS:** Linux 6.17.0-1010-azure

## Results

### CounterBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusInc | 50.59K | ± 1.74K | ops/s | **fastest** |
| prometheusNoLabelsInc | 43.77K | ± 403.22 | ops/s | 1.2x slower |
| prometheusAdd | 41.21K | ± 339.41 | ops/s | 1.2x slower |
| codahaleIncNoLabels | 36.39K | ± 1.41K | ops/s | 1.4x slower |
| simpleclientInc | 5.28K | ± 138.71 | ops/s | 9.6x slower |
| simpleclientAdd | 5.06K | ± 111.80 | ops/s | 10x slower |
| simpleclientNoLabelsInc | 5.00K | ± 86.07 | ops/s | 10x slower |
| openTelemetryIncNoLabels | 1.15K | ± 16.07 | ops/s | 44x slower |
| openTelemetryAdd | 1.14K | ± 21.56 | ops/s | 45x slower |
| openTelemetryInc | 1.09K | ± 26.51 | ops/s | 46x slower |

### HistogramBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusClassic | 5.01K | ± 1.31K | ops/s | **fastest** |
| simpleclient | 3.67K | ± 102.14 | ops/s | 1.4x slower |
| prometheusNative | 2.70K | ± 165.73 | ops/s | 1.9x slower |
| openTelemetryClassic | 566.94 | ± 28.21 | ops/s | 8.8x slower |
| openTelemetryExponential | 483.90 | ± 29.99 | ops/s | 10x slower |

### TextFormatUtilBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusWriteToNull | 503.59K | ± 5.60K | ops/s | **fastest** |
| prometheusWriteToByteArray | 495.07K | ± 3.07K | ops/s | 1.0x slower |
| openMetricsWriteToNull | 487.02K | ± 4.50K | ops/s | 1.0x slower |
| openMetricsWriteToByteArray | 474.04K | ± 5.31K | ops/s | 1.1x slower |

### Raw Results

```
Benchmark                                            Mode  Cnt          Score        Error  Units
CounterBenchmark.codahaleIncNoLabels                thrpt   15      36390.030   ± 1408.174  ops/s
CounterBenchmark.openTelemetryAdd                   thrpt   15       1135.190     ± 21.561  ops/s
CounterBenchmark.openTelemetryInc                   thrpt   15       1093.755     ± 26.506  ops/s
CounterBenchmark.openTelemetryIncNoLabels           thrpt   15       1152.892     ± 16.069  ops/s
CounterBenchmark.prometheusAdd                      thrpt   15      41209.728    ± 339.415  ops/s
CounterBenchmark.prometheusInc                      thrpt   15      50585.327   ± 1743.810  ops/s
CounterBenchmark.prometheusNoLabelsInc              thrpt   15      43771.451    ± 403.221  ops/s
CounterBenchmark.simpleclientAdd                    thrpt   15       5055.972    ± 111.798  ops/s
CounterBenchmark.simpleclientInc                    thrpt   15       5277.335    ± 138.714  ops/s
CounterBenchmark.simpleclientNoLabelsInc            thrpt   15       4999.763     ± 86.068  ops/s
HistogramBenchmark.openTelemetryClassic             thrpt   15        566.943     ± 28.212  ops/s
HistogramBenchmark.openTelemetryExponential         thrpt   15        483.901     ± 29.991  ops/s
HistogramBenchmark.prometheusClassic                thrpt   15       5009.545   ± 1313.415  ops/s
HistogramBenchmark.prometheusNative                 thrpt   15       2696.668    ± 165.732  ops/s
HistogramBenchmark.simpleclient                     thrpt   15       3666.180    ± 102.137  ops/s
TextFormatUtilBenchmark.openMetricsWriteToByteArray  thrpt   15     474043.400   ± 5310.272  ops/s
TextFormatUtilBenchmark.openMetricsWriteToNull      thrpt   15     487019.486   ± 4497.703  ops/s
TextFormatUtilBenchmark.prometheusWriteToByteArray  thrpt   15     495073.156   ± 3074.170  ops/s
TextFormatUtilBenchmark.prometheusWriteToNull       thrpt   15     503590.245   ± 5598.307  ops/s
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
