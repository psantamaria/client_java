# Prometheus Java Client Benchmarks

## Run Information

- **Date:** 2026-06-03T08:04:16Z
- **Commit:** [`4b69f40`](https://github.com/psantamaria/client_java/commit/4b69f40bd4e616d69468ce99dc4323162287a577)
- **JDK:** 25.0.2 (OpenJDK 64-Bit Server VM)
- **Benchmark config:** 3 fork(s), 3 warmup, 5 measurement, 4 threads
- **Hardware:** AMD EPYC 7763 64-Core Processor, 4 cores, 16 GB RAM
- **OS:** Linux 6.17.0-1015-azure

## Results

### CounterBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusInc | 66.68K | ± 535.33 | ops/s | **fastest** |
| prometheusNoLabelsInc | 55.94K | ± 1.20K | ops/s | 1.2x slower |
| prometheusAdd | 51.17K | ± 141.24 | ops/s | 1.3x slower |
| codahaleIncNoLabels | 47.15K | ± 127.41 | ops/s | 1.4x slower |
| simpleclientNoLabelsInc | 6.47K | ± 125.55 | ops/s | 10x slower |
| simpleclientInc | 6.31K | ± 292.93 | ops/s | 11x slower |
| simpleclientAdd | 6.09K | ± 121.56 | ops/s | 11x slower |
| openTelemetryInc | 1.38K | ± 207.52 | ops/s | 48x slower |
| openTelemetryIncNoLabels | 1.26K | ± 57.51 | ops/s | 53x slower |
| openTelemetryAdd | 1.21K | ± 47.50 | ops/s | 55x slower |

### HistogramBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusClassic | 5.74K | ± 1.34K | ops/s | **fastest** |
| simpleclient | 4.48K | ± 47.24 | ops/s | 1.3x slower |
| prometheusNative | 2.67K | ± 93.99 | ops/s | 2.2x slower |
| openTelemetryClassic | 681.82 | ± 10.28 | ops/s | 8.4x slower |
| openTelemetryExponential | 551.28 | ± 13.24 | ops/s | 10x slower |

### TextFormatUtilBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusWriteToNull | 490.56K | ± 1.15K | ops/s | **fastest** |
| prometheusWriteToByteArray | 489.49K | ± 1.59K | ops/s | 1.0x slower |
| openMetricsWriteToNull | 483.38K | ± 6.40K | ops/s | 1.0x slower |
| openMetricsWriteToByteArray | 473.14K | ± 5.41K | ops/s | 1.0x slower |

### Raw Results

```
Benchmark                                            Mode  Cnt          Score        Error  Units
CounterBenchmark.codahaleIncNoLabels                thrpt   15      47151.501    ± 127.413  ops/s
CounterBenchmark.openTelemetryAdd                   thrpt   15       1212.866     ± 47.503  ops/s
CounterBenchmark.openTelemetryInc                   thrpt   15       1384.321    ± 207.518  ops/s
CounterBenchmark.openTelemetryIncNoLabels           thrpt   15       1258.213     ± 57.513  ops/s
CounterBenchmark.prometheusAdd                      thrpt   15      51167.176    ± 141.238  ops/s
CounterBenchmark.prometheusInc                      thrpt   15      66681.483    ± 535.332  ops/s
CounterBenchmark.prometheusNoLabelsInc              thrpt   15      55943.703   ± 1201.963  ops/s
CounterBenchmark.simpleclientAdd                    thrpt   15       6089.880    ± 121.560  ops/s
CounterBenchmark.simpleclientInc                    thrpt   15       6307.260    ± 292.930  ops/s
CounterBenchmark.simpleclientNoLabelsInc            thrpt   15       6471.449    ± 125.545  ops/s
HistogramBenchmark.openTelemetryClassic             thrpt   15        681.821     ± 10.277  ops/s
HistogramBenchmark.openTelemetryExponential         thrpt   15        551.282     ± 13.244  ops/s
HistogramBenchmark.prometheusClassic                thrpt   15       5738.658   ± 1335.295  ops/s
HistogramBenchmark.prometheusNative                 thrpt   15       2667.227     ± 93.994  ops/s
HistogramBenchmark.simpleclient                     thrpt   15       4478.257     ± 47.241  ops/s
TextFormatUtilBenchmark.openMetricsWriteToByteArray  thrpt   15     473137.589   ± 5409.459  ops/s
TextFormatUtilBenchmark.openMetricsWriteToNull      thrpt   15     483381.264   ± 6400.190  ops/s
TextFormatUtilBenchmark.prometheusWriteToByteArray  thrpt   15     489492.669   ± 1591.794  ops/s
TextFormatUtilBenchmark.prometheusWriteToNull       thrpt   15     490555.161   ± 1149.564  ops/s
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
