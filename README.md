# Prometheus Java Client Benchmarks

## Run Information

- **Date:** 2026-07-28T06:16:20Z
- **Commit:** [`4b69f40`](https://github.com/psantamaria/client_java/commit/4b69f40bd4e616d69468ce99dc4323162287a577)
- **JDK:** 25.0.2 (OpenJDK 64-Bit Server VM)
- **Benchmark config:** 3 fork(s), 3 warmup, 5 measurement, 4 threads
- **Hardware:** AMD EPYC 7763 64-Core Processor, 4 cores, 16 GB RAM
- **OS:** Linux 6.17.0-1020-azure

## Results

### CounterBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusInc | 66.06K | ± 279.49 | ops/s | **fastest** |
| prometheusNoLabelsInc | 56.61K | ± 396.64 | ops/s | 1.2x slower |
| prometheusAdd | 50.88K | ± 629.53 | ops/s | 1.3x slower |
| codahaleIncNoLabels | 49.43K | ± 544.09 | ops/s | 1.3x slower |
| simpleclientNoLabelsInc | 6.57K | ± 35.22 | ops/s | 10x slower |
| simpleclientInc | 6.47K | ± 165.13 | ops/s | 10x slower |
| simpleclientAdd | 6.36K | ± 148.53 | ops/s | 10x slower |
| openTelemetryAdd | 1.69K | ± 271.17 | ops/s | 39x slower |
| openTelemetryInc | 1.31K | ± 36.11 | ops/s | 50x slower |
| openTelemetryIncNoLabels | 1.24K | ± 43.41 | ops/s | 53x slower |

### HistogramBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusClassic | 5.90K | ± 1.47K | ops/s | **fastest** |
| simpleclient | 4.46K | ± 37.74 | ops/s | 1.3x slower |
| prometheusNative | 2.82K | ± 344.81 | ops/s | 2.1x slower |
| openTelemetryClassic | 721.76 | ± 10.87 | ops/s | 8.2x slower |
| openTelemetryExponential | 571.03 | ± 47.48 | ops/s | 10x slower |

### TextFormatUtilBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusWriteToNull | 479.42K | ± 3.71K | ops/s | **fastest** |
| prometheusWriteToByteArray | 475.11K | ± 6.33K | ops/s | 1.0x slower |
| openMetricsWriteToNull | 470.71K | ± 3.39K | ops/s | 1.0x slower |
| openMetricsWriteToByteArray | 467.94K | ± 6.51K | ops/s | 1.0x slower |

### Raw Results

```
Benchmark                                            Mode  Cnt          Score        Error  Units
CounterBenchmark.codahaleIncNoLabels                thrpt   15      49433.071    ± 544.094  ops/s
CounterBenchmark.openTelemetryAdd                   thrpt   15       1688.845    ± 271.172  ops/s
CounterBenchmark.openTelemetryInc                   thrpt   15       1312.020     ± 36.114  ops/s
CounterBenchmark.openTelemetryIncNoLabels           thrpt   15       1244.505     ± 43.407  ops/s
CounterBenchmark.prometheusAdd                      thrpt   15      50880.661    ± 629.534  ops/s
CounterBenchmark.prometheusInc                      thrpt   15      66057.431    ± 279.493  ops/s
CounterBenchmark.prometheusNoLabelsInc              thrpt   15      56610.450    ± 396.639  ops/s
CounterBenchmark.simpleclientAdd                    thrpt   15       6363.456    ± 148.526  ops/s
CounterBenchmark.simpleclientInc                    thrpt   15       6469.446    ± 165.127  ops/s
CounterBenchmark.simpleclientNoLabelsInc            thrpt   15       6566.372     ± 35.220  ops/s
HistogramBenchmark.openTelemetryClassic             thrpt   15        721.757     ± 10.870  ops/s
HistogramBenchmark.openTelemetryExponential         thrpt   15        571.029     ± 47.480  ops/s
HistogramBenchmark.prometheusClassic                thrpt   15       5902.862   ± 1466.909  ops/s
HistogramBenchmark.prometheusNative                 thrpt   15       2815.426    ± 344.812  ops/s
HistogramBenchmark.simpleclient                     thrpt   15       4455.662     ± 37.741  ops/s
TextFormatUtilBenchmark.openMetricsWriteToByteArray  thrpt   15     467942.054   ± 6510.541  ops/s
TextFormatUtilBenchmark.openMetricsWriteToNull      thrpt   15     470713.017   ± 3386.538  ops/s
TextFormatUtilBenchmark.prometheusWriteToByteArray  thrpt   15     475109.551   ± 6332.687  ops/s
TextFormatUtilBenchmark.prometheusWriteToNull       thrpt   15     479424.192   ± 3711.749  ops/s
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
