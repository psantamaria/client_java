# Prometheus Java Client Benchmarks

## Run Information

- **Date:** 2026-08-16T04:10:55Z
- **Commit:** [`4b69f40`](https://github.com/psantamaria/client_java/commit/4b69f40bd4e616d69468ce99dc4323162287a577)
- **JDK:** 25.0.2 (OpenJDK 64-Bit Server VM)
- **Benchmark config:** 3 fork(s), 3 warmup, 5 measurement, 4 threads
- **Hardware:** AMD EPYC 9V74 80-Core Processor, 4 cores, 16 GB RAM
- **OS:** Linux 6.17.0-1022-azure

## Results

### CounterBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusInc | 59.31K | ± 3.29K | ops/s | **fastest** |
| prometheusNoLabelsInc | 50.92K | ± 748.60 | ops/s | 1.2x slower |
| prometheusAdd | 48.05K | ± 507.33 | ops/s | 1.2x slower |
| codahaleIncNoLabels | 43.95K | ± 153.09 | ops/s | 1.3x slower |
| simpleclientInc | 6.28K | ± 8.56 | ops/s | 9.4x slower |
| simpleclientNoLabelsInc | 6.11K | ± 237.67 | ops/s | 9.7x slower |
| simpleclientAdd | 5.79K | ± 326.34 | ops/s | 10x slower |
| openTelemetryIncNoLabels | 1.42K | ± 111.59 | ops/s | 42x slower |
| openTelemetryAdd | 1.37K | ± 99.89 | ops/s | 43x slower |
| openTelemetryInc | 1.29K | ± 79.46 | ops/s | 46x slower |

### HistogramBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusClassic | 5.45K | ± 1.58K | ops/s | **fastest** |
| simpleclient | 4.51K | ± 34.16 | ops/s | 1.2x slower |
| prometheusNative | 3.01K | ± 249.22 | ops/s | 1.8x slower |
| openTelemetryClassic | 600.63 | ± 12.14 | ops/s | 9.1x slower |
| openTelemetryExponential | 477.98 | ± 17.08 | ops/s | 11x slower |

### TextFormatUtilBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusWriteToNull | 552.34K | ± 3.40K | ops/s | **fastest** |
| prometheusWriteToByteArray | 544.55K | ± 7.18K | ops/s | 1.0x slower |
| openMetricsWriteToNull | 532.23K | ± 2.88K | ops/s | 1.0x slower |
| openMetricsWriteToByteArray | 516.84K | ± 4.69K | ops/s | 1.1x slower |

### Raw Results

```
Benchmark                                            Mode  Cnt          Score        Error  Units
CounterBenchmark.codahaleIncNoLabels                thrpt   15      43946.431    ± 153.091  ops/s
CounterBenchmark.openTelemetryAdd                   thrpt   15       1367.289     ± 99.893  ops/s
CounterBenchmark.openTelemetryInc                   thrpt   15       1291.362     ± 79.463  ops/s
CounterBenchmark.openTelemetryIncNoLabels           thrpt   15       1422.044    ± 111.589  ops/s
CounterBenchmark.prometheusAdd                      thrpt   15      48046.636    ± 507.333  ops/s
CounterBenchmark.prometheusInc                      thrpt   15      59308.022   ± 3292.979  ops/s
CounterBenchmark.prometheusNoLabelsInc              thrpt   15      50916.835    ± 748.602  ops/s
CounterBenchmark.simpleclientAdd                    thrpt   15       5790.577    ± 326.335  ops/s
CounterBenchmark.simpleclientInc                    thrpt   15       6281.694      ± 8.561  ops/s
CounterBenchmark.simpleclientNoLabelsInc            thrpt   15       6111.092    ± 237.670  ops/s
HistogramBenchmark.openTelemetryClassic             thrpt   15        600.627     ± 12.143  ops/s
HistogramBenchmark.openTelemetryExponential         thrpt   15        477.980     ± 17.082  ops/s
HistogramBenchmark.prometheusClassic                thrpt   15       5448.257   ± 1576.642  ops/s
HistogramBenchmark.prometheusNative                 thrpt   15       3013.680    ± 249.220  ops/s
HistogramBenchmark.simpleclient                     thrpt   15       4507.169     ± 34.159  ops/s
TextFormatUtilBenchmark.openMetricsWriteToByteArray  thrpt   15     516838.496   ± 4693.146  ops/s
TextFormatUtilBenchmark.openMetricsWriteToNull      thrpt   15     532233.883   ± 2881.543  ops/s
TextFormatUtilBenchmark.prometheusWriteToByteArray  thrpt   15     544546.345   ± 7180.515  ops/s
TextFormatUtilBenchmark.prometheusWriteToNull       thrpt   15     552342.033   ± 3402.788  ops/s
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
