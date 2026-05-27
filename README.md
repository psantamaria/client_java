# Prometheus Java Client Benchmarks

## Run Information

- **Date:** 2026-05-27T07:31:58Z
- **Commit:** [`4b69f40`](https://github.com/psantamaria/client_java/commit/4b69f40bd4e616d69468ce99dc4323162287a577)
- **JDK:** 25.0.2 (OpenJDK 64-Bit Server VM)
- **Benchmark config:** 3 fork(s), 3 warmup, 5 measurement, 4 threads
- **Hardware:** AMD EPYC 7763 64-Core Processor, 4 cores, 16 GB RAM
- **OS:** Linux 6.17.0-1013-azure

## Results

### CounterBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusInc | 65.69K | ± 1.82K | ops/s | **fastest** |
| prometheusNoLabelsInc | 56.97K | ± 380.81 | ops/s | 1.2x slower |
| prometheusAdd | 51.32K | ± 217.58 | ops/s | 1.3x slower |
| codahaleIncNoLabels | 48.72K | ± 1.32K | ops/s | 1.3x slower |
| simpleclientInc | 6.58K | ± 201.11 | ops/s | 10.0x slower |
| simpleclientNoLabelsInc | 6.50K | ± 192.95 | ops/s | 10x slower |
| simpleclientAdd | 6.24K | ± 189.85 | ops/s | 11x slower |
| openTelemetryAdd | 1.32K | ± 41.17 | ops/s | 50x slower |
| openTelemetryIncNoLabels | 1.28K | ± 238.96 | ops/s | 51x slower |
| openTelemetryInc | 1.25K | ± 74.86 | ops/s | 52x slower |

### HistogramBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusClassic | 4.88K | ± 695.73 | ops/s | **fastest** |
| simpleclient | 4.41K | ± 16.06 | ops/s | 1.1x slower |
| prometheusNative | 3.18K | ± 61.12 | ops/s | 1.5x slower |
| openTelemetryClassic | 690.26 | ± 40.22 | ops/s | 7.1x slower |
| openTelemetryExponential | 555.95 | ± 17.17 | ops/s | 8.8x slower |

### TextFormatUtilBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusWriteToNull | 490.83K | ± 5.99K | ops/s | **fastest** |
| prometheusWriteToByteArray | 475.98K | ± 9.28K | ops/s | 1.0x slower |
| openMetricsWriteToByteArray | 468.63K | ± 6.83K | ops/s | 1.0x slower |
| openMetricsWriteToNull | 463.97K | ± 4.75K | ops/s | 1.1x slower |

### Raw Results

```
Benchmark                                            Mode  Cnt          Score        Error  Units
CounterBenchmark.codahaleIncNoLabels                thrpt   15      48721.164   ± 1316.220  ops/s
CounterBenchmark.openTelemetryAdd                   thrpt   15       1321.128     ± 41.172  ops/s
CounterBenchmark.openTelemetryInc                   thrpt   15       1252.200     ± 74.860  ops/s
CounterBenchmark.openTelemetryIncNoLabels           thrpt   15       1276.072    ± 238.960  ops/s
CounterBenchmark.prometheusAdd                      thrpt   15      51322.073    ± 217.583  ops/s
CounterBenchmark.prometheusInc                      thrpt   15      65690.491   ± 1816.680  ops/s
CounterBenchmark.prometheusNoLabelsInc              thrpt   15      56974.165    ± 380.808  ops/s
CounterBenchmark.simpleclientAdd                    thrpt   15       6241.766    ± 189.846  ops/s
CounterBenchmark.simpleclientInc                    thrpt   15       6582.982    ± 201.114  ops/s
CounterBenchmark.simpleclientNoLabelsInc            thrpt   15       6504.621    ± 192.950  ops/s
HistogramBenchmark.openTelemetryClassic             thrpt   15        690.264     ± 40.216  ops/s
HistogramBenchmark.openTelemetryExponential         thrpt   15        555.955     ± 17.175  ops/s
HistogramBenchmark.prometheusClassic                thrpt   15       4878.899    ± 695.726  ops/s
HistogramBenchmark.prometheusNative                 thrpt   15       3180.490     ± 61.120  ops/s
HistogramBenchmark.simpleclient                     thrpt   15       4414.836     ± 16.060  ops/s
TextFormatUtilBenchmark.openMetricsWriteToByteArray  thrpt   15     468628.648   ± 6834.089  ops/s
TextFormatUtilBenchmark.openMetricsWriteToNull      thrpt   15     463972.811   ± 4754.198  ops/s
TextFormatUtilBenchmark.prometheusWriteToByteArray  thrpt   15     475983.764   ± 9275.731  ops/s
TextFormatUtilBenchmark.prometheusWriteToNull       thrpt   15     490831.501   ± 5990.814  ops/s
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
