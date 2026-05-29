# Prometheus Java Client Benchmarks

## Run Information

- **Date:** 2026-05-29T07:25:27Z
- **Commit:** [`4b69f40`](https://github.com/psantamaria/client_java/commit/4b69f40bd4e616d69468ce99dc4323162287a577)
- **JDK:** 25.0.2 (OpenJDK 64-Bit Server VM)
- **Benchmark config:** 3 fork(s), 3 warmup, 5 measurement, 4 threads
- **Hardware:** AMD EPYC 9V74 80-Core Processor, 4 cores, 16 GB RAM
- **OS:** Linux 6.17.0-1015-azure

## Results

### CounterBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusInc | 59.91K | ± 56.02 | ops/s | **fastest** |
| prometheusNoLabelsInc | 51.29K | ± 589.77 | ops/s | 1.2x slower |
| prometheusAdd | 47.91K | ± 528.99 | ops/s | 1.3x slower |
| codahaleIncNoLabels | 43.10K | ± 1.15K | ops/s | 1.4x slower |
| simpleclientInc | 6.20K | ± 115.95 | ops/s | 9.7x slower |
| simpleclientNoLabelsInc | 6.11K | ± 121.89 | ops/s | 9.8x slower |
| simpleclientAdd | 6.07K | ± 168.72 | ops/s | 9.9x slower |
| openTelemetryIncNoLabels | 1.45K | ± 67.14 | ops/s | 41x slower |
| openTelemetryAdd | 1.36K | ± 33.49 | ops/s | 44x slower |
| openTelemetryInc | 1.31K | ± 19.01 | ops/s | 46x slower |

### HistogramBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusClassic | 5.02K | ± 553.89 | ops/s | **fastest** |
| simpleclient | 4.35K | ± 86.27 | ops/s | 1.2x slower |
| prometheusNative | 2.84K | ± 106.21 | ops/s | 1.8x slower |
| openTelemetryClassic | 586.06 | ± 17.59 | ops/s | 8.6x slower |
| openTelemetryExponential | 508.71 | ± 13.79 | ops/s | 9.9x slower |

### TextFormatUtilBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusWriteToNull | 548.83K | ± 2.53K | ops/s | **fastest** |
| prometheusWriteToByteArray | 539.19K | ± 8.84K | ops/s | 1.0x slower |
| openMetricsWriteToNull | 535.82K | ± 2.95K | ops/s | 1.0x slower |
| openMetricsWriteToByteArray | 520.03K | ± 6.04K | ops/s | 1.1x slower |

### Raw Results

```
Benchmark                                            Mode  Cnt          Score        Error  Units
CounterBenchmark.codahaleIncNoLabels                thrpt   15      43102.689   ± 1151.665  ops/s
CounterBenchmark.openTelemetryAdd                   thrpt   15       1359.512     ± 33.493  ops/s
CounterBenchmark.openTelemetryInc                   thrpt   15       1305.062     ± 19.006  ops/s
CounterBenchmark.openTelemetryIncNoLabels           thrpt   15       1446.994     ± 67.138  ops/s
CounterBenchmark.prometheusAdd                      thrpt   15      47910.038    ± 528.989  ops/s
CounterBenchmark.prometheusInc                      thrpt   15      59907.154     ± 56.015  ops/s
CounterBenchmark.prometheusNoLabelsInc              thrpt   15      51291.665    ± 589.767  ops/s
CounterBenchmark.simpleclientAdd                    thrpt   15       6073.874    ± 168.723  ops/s
CounterBenchmark.simpleclientInc                    thrpt   15       6197.618    ± 115.951  ops/s
CounterBenchmark.simpleclientNoLabelsInc            thrpt   15       6109.911    ± 121.886  ops/s
HistogramBenchmark.openTelemetryClassic             thrpt   15        586.056     ± 17.595  ops/s
HistogramBenchmark.openTelemetryExponential         thrpt   15        508.713     ± 13.787  ops/s
HistogramBenchmark.prometheusClassic                thrpt   15       5021.233    ± 553.891  ops/s
HistogramBenchmark.prometheusNative                 thrpt   15       2836.759    ± 106.211  ops/s
HistogramBenchmark.simpleclient                     thrpt   15       4345.254     ± 86.273  ops/s
TextFormatUtilBenchmark.openMetricsWriteToByteArray  thrpt   15     520026.958   ± 6036.133  ops/s
TextFormatUtilBenchmark.openMetricsWriteToNull      thrpt   15     535817.131   ± 2949.671  ops/s
TextFormatUtilBenchmark.prometheusWriteToByteArray  thrpt   15     539187.610   ± 8840.816  ops/s
TextFormatUtilBenchmark.prometheusWriteToNull       thrpt   15     548827.125   ± 2526.645  ops/s
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
