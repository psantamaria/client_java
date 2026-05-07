# Prometheus Java Client Benchmarks

## Run Information

- **Date:** 2026-05-07T06:44:34Z
- **Commit:** [`4b69f40`](https://github.com/psantamaria/client_java/commit/4b69f40bd4e616d69468ce99dc4323162287a577)
- **JDK:** 25.0.2 (OpenJDK 64-Bit Server VM)
- **Benchmark config:** 3 fork(s), 3 warmup, 5 measurement, 4 threads
- **Hardware:** AMD EPYC 9V74 80-Core Processor, 4 cores, 16 GB RAM
- **OS:** Linux 6.17.0-1010-azure

## Results

### CounterBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusInc | 59.47K | ± 667.18 | ops/s | **fastest** |
| prometheusNoLabelsInc | 51.39K | ± 915.89 | ops/s | 1.2x slower |
| prometheusAdd | 47.97K | ± 316.73 | ops/s | 1.2x slower |
| codahaleIncNoLabels | 44.15K | ± 908.41 | ops/s | 1.3x slower |
| simpleclientNoLabelsInc | 6.27K | ± 76.76 | ops/s | 9.5x slower |
| simpleclientInc | 6.22K | ± 172.33 | ops/s | 9.6x slower |
| simpleclientAdd | 5.75K | ± 222.81 | ops/s | 10x slower |
| openTelemetryInc | 1.40K | ± 132.95 | ops/s | 42x slower |
| openTelemetryAdd | 1.32K | ± 12.23 | ops/s | 45x slower |
| openTelemetryIncNoLabels | 1.29K | ± 78.62 | ops/s | 46x slower |

### HistogramBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusClassic | 5.11K | ± 395.53 | ops/s | **fastest** |
| simpleclient | 4.47K | ± 80.03 | ops/s | 1.1x slower |
| prometheusNative | 3.14K | ± 80.08 | ops/s | 1.6x slower |
| openTelemetryClassic | 612.97 | ± 11.95 | ops/s | 8.3x slower |
| openTelemetryExponential | 524.02 | ± 26.25 | ops/s | 9.7x slower |

### TextFormatUtilBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusWriteToNull | 561.13K | ± 4.12K | ops/s | **fastest** |
| prometheusWriteToByteArray | 544.49K | ± 2.34K | ops/s | 1.0x slower |
| openMetricsWriteToNull | 539.62K | ± 4.50K | ops/s | 1.0x slower |
| openMetricsWriteToByteArray | 525.67K | ± 5.81K | ops/s | 1.1x slower |

### Raw Results

```
Benchmark                                            Mode  Cnt          Score        Error  Units
CounterBenchmark.codahaleIncNoLabels                thrpt   15      44147.533    ± 908.406  ops/s
CounterBenchmark.openTelemetryAdd                   thrpt   15       1324.681     ± 12.228  ops/s
CounterBenchmark.openTelemetryInc                   thrpt   15       1403.000    ± 132.950  ops/s
CounterBenchmark.openTelemetryIncNoLabels           thrpt   15       1291.656     ± 78.624  ops/s
CounterBenchmark.prometheusAdd                      thrpt   15      47972.384    ± 316.733  ops/s
CounterBenchmark.prometheusInc                      thrpt   15      59471.197    ± 667.179  ops/s
CounterBenchmark.prometheusNoLabelsInc              thrpt   15      51386.623    ± 915.890  ops/s
CounterBenchmark.simpleclientAdd                    thrpt   15       5747.251    ± 222.812  ops/s
CounterBenchmark.simpleclientInc                    thrpt   15       6222.659    ± 172.328  ops/s
CounterBenchmark.simpleclientNoLabelsInc            thrpt   15       6271.222     ± 76.757  ops/s
HistogramBenchmark.openTelemetryClassic             thrpt   15        612.967     ± 11.951  ops/s
HistogramBenchmark.openTelemetryExponential         thrpt   15        524.023     ± 26.247  ops/s
HistogramBenchmark.prometheusClassic                thrpt   15       5107.849    ± 395.531  ops/s
HistogramBenchmark.prometheusNative                 thrpt   15       3138.053     ± 80.077  ops/s
HistogramBenchmark.simpleclient                     thrpt   15       4472.137     ± 80.028  ops/s
TextFormatUtilBenchmark.openMetricsWriteToByteArray  thrpt   15     525666.332   ± 5811.682  ops/s
TextFormatUtilBenchmark.openMetricsWriteToNull      thrpt   15     539624.330   ± 4501.159  ops/s
TextFormatUtilBenchmark.prometheusWriteToByteArray  thrpt   15     544486.534   ± 2335.890  ops/s
TextFormatUtilBenchmark.prometheusWriteToNull       thrpt   15     561133.363   ± 4116.982  ops/s
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
