# Prometheus Java Client Benchmarks

## Run Information

- **Date:** 2026-08-20T04:08:20Z
- **Commit:** [`4b69f40`](https://github.com/psantamaria/client_java/commit/4b69f40bd4e616d69468ce99dc4323162287a577)
- **JDK:** 25.0.2 (OpenJDK 64-Bit Server VM)
- **Benchmark config:** 3 fork(s), 3 warmup, 5 measurement, 4 threads
- **Hardware:** AMD EPYC 7763 64-Core Processor, 4 cores, 16 GB RAM
- **OS:** Linux 6.17.0-1022-azure

## Results

### CounterBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusInc | 66.03K | ± 285.52 | ops/s | **fastest** |
| prometheusNoLabelsInc | 56.32K | ± 1.07K | ops/s | 1.2x slower |
| codahaleIncNoLabels | 50.77K | ± 409.29 | ops/s | 1.3x slower |
| prometheusAdd | 50.73K | ± 1.50K | ops/s | 1.3x slower |
| simpleclientNoLabelsInc | 6.50K | ± 123.78 | ops/s | 10x slower |
| simpleclientInc | 6.42K | ± 352.19 | ops/s | 10x slower |
| simpleclientAdd | 6.05K | ± 334.37 | ops/s | 11x slower |
| openTelemetryAdd | 1.58K | ± 260.36 | ops/s | 42x slower |
| openTelemetryIncNoLabels | 1.46K | ± 160.12 | ops/s | 45x slower |
| openTelemetryInc | 1.26K | ± 43.42 | ops/s | 52x slower |

### HistogramBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusClassic | 4.57K | ± 484.90 | ops/s | **fastest** |
| simpleclient | 4.50K | ± 29.68 | ops/s | 1.0x slower |
| prometheusNative | 2.67K | ± 139.65 | ops/s | 1.7x slower |
| openTelemetryClassic | 672.49 | ± 7.80 | ops/s | 6.8x slower |
| openTelemetryExponential | 558.64 | ± 21.82 | ops/s | 8.2x slower |

### TextFormatUtilBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusWriteToNull | 495.29K | ± 4.56K | ops/s | **fastest** |
| openMetricsWriteToNull | 489.65K | ± 2.12K | ops/s | 1.0x slower |
| prometheusWriteToByteArray | 487.63K | ± 4.19K | ops/s | 1.0x slower |
| openMetricsWriteToByteArray | 484.84K | ± 3.72K | ops/s | 1.0x slower |

### Raw Results

```
Benchmark                                            Mode  Cnt          Score        Error  Units
CounterBenchmark.codahaleIncNoLabels                thrpt   15      50768.031    ± 409.295  ops/s
CounterBenchmark.openTelemetryAdd                   thrpt   15       1578.271    ± 260.359  ops/s
CounterBenchmark.openTelemetryInc                   thrpt   15       1259.989     ± 43.416  ops/s
CounterBenchmark.openTelemetryIncNoLabels           thrpt   15       1463.647    ± 160.115  ops/s
CounterBenchmark.prometheusAdd                      thrpt   15      50726.466   ± 1501.140  ops/s
CounterBenchmark.prometheusInc                      thrpt   15      66026.856    ± 285.517  ops/s
CounterBenchmark.prometheusNoLabelsInc              thrpt   15      56322.479   ± 1073.919  ops/s
CounterBenchmark.simpleclientAdd                    thrpt   15       6051.177    ± 334.375  ops/s
CounterBenchmark.simpleclientInc                    thrpt   15       6417.868    ± 352.185  ops/s
CounterBenchmark.simpleclientNoLabelsInc            thrpt   15       6495.453    ± 123.777  ops/s
HistogramBenchmark.openTelemetryClassic             thrpt   15        672.492      ± 7.798  ops/s
HistogramBenchmark.openTelemetryExponential         thrpt   15        558.645     ± 21.824  ops/s
HistogramBenchmark.prometheusClassic                thrpt   15       4573.423    ± 484.899  ops/s
HistogramBenchmark.prometheusNative                 thrpt   15       2672.220    ± 139.646  ops/s
HistogramBenchmark.simpleclient                     thrpt   15       4496.779     ± 29.685  ops/s
TextFormatUtilBenchmark.openMetricsWriteToByteArray  thrpt   15     484841.871   ± 3718.714  ops/s
TextFormatUtilBenchmark.openMetricsWriteToNull      thrpt   15     489649.894   ± 2115.737  ops/s
TextFormatUtilBenchmark.prometheusWriteToByteArray  thrpt   15     487630.480   ± 4191.512  ops/s
TextFormatUtilBenchmark.prometheusWriteToNull       thrpt   15     495289.037   ± 4556.770  ops/s
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
