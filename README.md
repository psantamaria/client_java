# Prometheus Java Client Benchmarks

## Run Information

- **Date:** 2026-06-07T07:35:20Z
- **Commit:** [`4b69f40`](https://github.com/psantamaria/client_java/commit/4b69f40bd4e616d69468ce99dc4323162287a577)
- **JDK:** 25.0.2 (OpenJDK 64-Bit Server VM)
- **Benchmark config:** 3 fork(s), 3 warmup, 5 measurement, 4 threads
- **Hardware:** AMD EPYC 9V74 80-Core Processor, 4 cores, 16 GB RAM
- **OS:** Linux 6.17.0-1015-azure

## Results

### CounterBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusInc | 59.53K | ± 329.07 | ops/s | **fastest** |
| prometheusNoLabelsInc | 52.09K | ± 868.45 | ops/s | 1.1x slower |
| prometheusAdd | 48.53K | ± 83.47 | ops/s | 1.2x slower |
| codahaleIncNoLabels | 44.33K | ± 378.19 | ops/s | 1.3x slower |
| simpleclientNoLabelsInc | 6.27K | ± 32.63 | ops/s | 9.5x slower |
| simpleclientInc | 6.04K | ± 235.14 | ops/s | 9.9x slower |
| simpleclientAdd | 5.97K | ± 204.18 | ops/s | 10.0x slower |
| openTelemetryAdd | 1.37K | ± 100.07 | ops/s | 43x slower |
| openTelemetryInc | 1.31K | ± 121.31 | ops/s | 45x slower |
| openTelemetryIncNoLabels | 1.27K | ± 53.68 | ops/s | 47x slower |

### HistogramBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusClassic | 4.46K | ± 327.28 | ops/s | **fastest** |
| simpleclient | 4.22K | ± 22.43 | ops/s | 1.1x slower |
| prometheusNative | 2.96K | ± 124.08 | ops/s | 1.5x slower |
| openTelemetryClassic | 619.81 | ± 15.89 | ops/s | 7.2x slower |
| openTelemetryExponential | 518.51 | ± 8.38 | ops/s | 8.6x slower |

### TextFormatUtilBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusWriteToNull | 553.57K | ± 3.70K | ops/s | **fastest** |
| prometheusWriteToByteArray | 547.15K | ± 2.21K | ops/s | 1.0x slower |
| openMetricsWriteToNull | 538.15K | ± 3.13K | ops/s | 1.0x slower |
| openMetricsWriteToByteArray | 527.81K | ± 6.90K | ops/s | 1.0x slower |

### Raw Results

```
Benchmark                                            Mode  Cnt          Score        Error  Units
CounterBenchmark.codahaleIncNoLabels                thrpt   15      44334.502    ± 378.192  ops/s
CounterBenchmark.openTelemetryAdd                   thrpt   15       1371.809    ± 100.071  ops/s
CounterBenchmark.openTelemetryInc                   thrpt   15       1312.043    ± 121.310  ops/s
CounterBenchmark.openTelemetryIncNoLabels           thrpt   15       1268.967     ± 53.680  ops/s
CounterBenchmark.prometheusAdd                      thrpt   15      48528.602     ± 83.469  ops/s
CounterBenchmark.prometheusInc                      thrpt   15      59528.243    ± 329.065  ops/s
CounterBenchmark.prometheusNoLabelsInc              thrpt   15      52092.023    ± 868.448  ops/s
CounterBenchmark.simpleclientAdd                    thrpt   15       5967.972    ± 204.184  ops/s
CounterBenchmark.simpleclientInc                    thrpt   15       6042.408    ± 235.139  ops/s
CounterBenchmark.simpleclientNoLabelsInc            thrpt   15       6270.348     ± 32.634  ops/s
HistogramBenchmark.openTelemetryClassic             thrpt   15        619.809     ± 15.886  ops/s
HistogramBenchmark.openTelemetryExponential         thrpt   15        518.511      ± 8.381  ops/s
HistogramBenchmark.prometheusClassic                thrpt   15       4461.915    ± 327.277  ops/s
HistogramBenchmark.prometheusNative                 thrpt   15       2961.269    ± 124.080  ops/s
HistogramBenchmark.simpleclient                     thrpt   15       4222.277     ± 22.433  ops/s
TextFormatUtilBenchmark.openMetricsWriteToByteArray  thrpt   15     527806.599   ± 6897.682  ops/s
TextFormatUtilBenchmark.openMetricsWriteToNull      thrpt   15     538148.716   ± 3128.986  ops/s
TextFormatUtilBenchmark.prometheusWriteToByteArray  thrpt   15     547153.409   ± 2212.357  ops/s
TextFormatUtilBenchmark.prometheusWriteToNull       thrpt   15     553568.363   ± 3697.307  ops/s
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
