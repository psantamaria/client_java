# Prometheus Java Client Benchmarks

## Run Information

- **Date:** 2026-08-13T05:21:42Z
- **Commit:** [`4b69f40`](https://github.com/psantamaria/client_java/commit/4b69f40bd4e616d69468ce99dc4323162287a577)
- **JDK:** 25.0.2 (OpenJDK 64-Bit Server VM)
- **Benchmark config:** 3 fork(s), 3 warmup, 5 measurement, 4 threads
- **Hardware:** INTEL(R) XEON(R) PLATINUM 8573C, 4 cores, 16 GB RAM
- **OS:** Linux 6.17.0-1020-azure

## Results

### CounterBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| codahaleIncNoLabels | 27.24K | ± 868.75 | ops/s | **fastest** |
| prometheusInc | 27.04K | ± 685.42 | ops/s | 1.0x slower |
| prometheusNoLabelsInc | 26.77K | ± 97.29 | ops/s | 1.0x slower |
| prometheusAdd | 25.90K | ± 125.44 | ops/s | 1.1x slower |
| simpleclientNoLabelsInc | 6.67K | ± 51.78 | ops/s | 4.1x slower |
| simpleclientInc | 6.65K | ± 35.71 | ops/s | 4.1x slower |
| simpleclientAdd | 6.59K | ± 53.49 | ops/s | 4.1x slower |
| openTelemetryAdd | 1.10K | ± 120.61 | ops/s | 25x slower |
| openTelemetryIncNoLabels | 1.02K | ± 49.31 | ops/s | 27x slower |
| openTelemetryInc | 1.00K | ± 45.60 | ops/s | 27x slower |

### HistogramBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| simpleclient | 4.40K | ± 43.96 | ops/s | **fastest** |
| prometheusClassic | 2.43K | ± 418.17 | ops/s | 1.8x slower |
| prometheusNative | 2.22K | ± 115.23 | ops/s | 2.0x slower |
| openTelemetryClassic | 387.87 | ± 6.26 | ops/s | 11x slower |
| openTelemetryExponential | 339.09 | ± 8.14 | ops/s | 13x slower |

### TextFormatUtilBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusWriteToByteArray | 295.84K | ± 2.04K | ops/s | **fastest** |
| prometheusWriteToNull | 295.72K | ± 2.70K | ops/s | 1.0x slower |
| openMetricsWriteToNull | 281.64K | ± 7.73K | ops/s | 1.1x slower |
| openMetricsWriteToByteArray | 280.58K | ± 1.41K | ops/s | 1.1x slower |

### Raw Results

```
Benchmark                                            Mode  Cnt          Score        Error  Units
CounterBenchmark.codahaleIncNoLabels                thrpt   15      27236.615    ± 868.745  ops/s
CounterBenchmark.openTelemetryAdd                   thrpt   15       1097.166    ± 120.610  ops/s
CounterBenchmark.openTelemetryInc                   thrpt   15       1003.977     ± 45.601  ops/s
CounterBenchmark.openTelemetryIncNoLabels           thrpt   15       1022.572     ± 49.308  ops/s
CounterBenchmark.prometheusAdd                      thrpt   15      25895.156    ± 125.442  ops/s
CounterBenchmark.prometheusInc                      thrpt   15      27044.095    ± 685.422  ops/s
CounterBenchmark.prometheusNoLabelsInc              thrpt   15      26766.699     ± 97.285  ops/s
CounterBenchmark.simpleclientAdd                    thrpt   15       6591.718     ± 53.489  ops/s
CounterBenchmark.simpleclientInc                    thrpt   15       6653.096     ± 35.711  ops/s
CounterBenchmark.simpleclientNoLabelsInc            thrpt   15       6672.714     ± 51.777  ops/s
HistogramBenchmark.openTelemetryClassic             thrpt   15        387.870      ± 6.256  ops/s
HistogramBenchmark.openTelemetryExponential         thrpt   15        339.094      ± 8.139  ops/s
HistogramBenchmark.prometheusClassic                thrpt   15       2433.802    ± 418.169  ops/s
HistogramBenchmark.prometheusNative                 thrpt   15       2215.598    ± 115.233  ops/s
HistogramBenchmark.simpleclient                     thrpt   15       4396.818     ± 43.958  ops/s
TextFormatUtilBenchmark.openMetricsWriteToByteArray  thrpt   15     280584.557   ± 1406.769  ops/s
TextFormatUtilBenchmark.openMetricsWriteToNull      thrpt   15     281635.799   ± 7730.031  ops/s
TextFormatUtilBenchmark.prometheusWriteToByteArray  thrpt   15     295841.836   ± 2044.546  ops/s
TextFormatUtilBenchmark.prometheusWriteToNull       thrpt   15     295720.571   ± 2704.196  ops/s
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
