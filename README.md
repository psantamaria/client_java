# Prometheus Java Client Benchmarks

## Run Information

- **Date:** 2026-09-01T08:22:24Z
- **Commit:** [`4b69f40`](https://github.com/psantamaria/client_java/commit/4b69f40bd4e616d69468ce99dc4323162287a577)
- **JDK:** 25.0.2 (OpenJDK 64-Bit Server VM)
- **Benchmark config:** 3 fork(s), 3 warmup, 5 measurement, 4 threads
- **Hardware:** AMD EPYC 9V74 80-Core Processor, 4 cores, 16 GB RAM
- **OS:** Linux 6.17.0-1022-azure

## Results

### CounterBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusInc | 60.56K | ± 1.28K | ops/s | **fastest** |
| prometheusNoLabelsInc | 51.40K | ± 421.52 | ops/s | 1.2x slower |
| prometheusAdd | 49.16K | ± 578.21 | ops/s | 1.2x slower |
| codahaleIncNoLabels | 43.25K | ± 2.10K | ops/s | 1.4x slower |
| simpleclientNoLabelsInc | 6.12K | ± 186.84 | ops/s | 9.9x slower |
| simpleclientInc | 6.04K | ± 26.92 | ops/s | 10x slower |
| simpleclientAdd | 5.89K | ± 233.09 | ops/s | 10x slower |
| openTelemetryInc | 1.38K | ± 54.91 | ops/s | 44x slower |
| openTelemetryAdd | 1.37K | ± 94.00 | ops/s | 44x slower |
| openTelemetryIncNoLabels | 1.30K | ± 109.76 | ops/s | 47x slower |

### HistogramBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusClassic | 5.93K | ± 1.27K | ops/s | **fastest** |
| simpleclient | 4.47K | ± 84.82 | ops/s | 1.3x slower |
| prometheusNative | 2.99K | ± 265.11 | ops/s | 2.0x slower |
| openTelemetryClassic | 580.83 | ± 7.36 | ops/s | 10x slower |
| openTelemetryExponential | 504.91 | ± 11.49 | ops/s | 12x slower |

### TextFormatUtilBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusWriteToNull | 555.93K | ± 8.24K | ops/s | **fastest** |
| prometheusWriteToByteArray | 543.33K | ± 6.89K | ops/s | 1.0x slower |
| openMetricsWriteToNull | 532.74K | ± 5.88K | ops/s | 1.0x slower |
| openMetricsWriteToByteArray | 528.49K | ± 3.49K | ops/s | 1.1x slower |

### Raw Results

```
Benchmark                                            Mode  Cnt          Score        Error  Units
CounterBenchmark.codahaleIncNoLabels                thrpt   15      43250.018   ± 2097.939  ops/s
CounterBenchmark.openTelemetryAdd                   thrpt   15       1371.249     ± 93.998  ops/s
CounterBenchmark.openTelemetryInc                   thrpt   15       1383.603     ± 54.911  ops/s
CounterBenchmark.openTelemetryIncNoLabels           thrpt   15       1296.993    ± 109.764  ops/s
CounterBenchmark.prometheusAdd                      thrpt   15      49161.767    ± 578.206  ops/s
CounterBenchmark.prometheusInc                      thrpt   15      60557.986   ± 1275.526  ops/s
CounterBenchmark.prometheusNoLabelsInc              thrpt   15      51404.218    ± 421.516  ops/s
CounterBenchmark.simpleclientAdd                    thrpt   15       5892.580    ± 233.091  ops/s
CounterBenchmark.simpleclientInc                    thrpt   15       6036.580     ± 26.922  ops/s
CounterBenchmark.simpleclientNoLabelsInc            thrpt   15       6118.078    ± 186.843  ops/s
HistogramBenchmark.openTelemetryClassic             thrpt   15        580.834      ± 7.360  ops/s
HistogramBenchmark.openTelemetryExponential         thrpt   15        504.914     ± 11.490  ops/s
HistogramBenchmark.prometheusClassic                thrpt   15       5930.998   ± 1273.521  ops/s
HistogramBenchmark.prometheusNative                 thrpt   15       2986.390    ± 265.106  ops/s
HistogramBenchmark.simpleclient                     thrpt   15       4468.257     ± 84.818  ops/s
TextFormatUtilBenchmark.openMetricsWriteToByteArray  thrpt   15     528492.233   ± 3489.222  ops/s
TextFormatUtilBenchmark.openMetricsWriteToNull      thrpt   15     532738.491   ± 5877.725  ops/s
TextFormatUtilBenchmark.prometheusWriteToByteArray  thrpt   15     543327.975   ± 6887.847  ops/s
TextFormatUtilBenchmark.prometheusWriteToNull       thrpt   15     555932.089   ± 8244.683  ops/s
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
