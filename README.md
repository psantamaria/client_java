# Prometheus Java Client Benchmarks

## Run Information

- **Date:** 2026-10-07T09:19:40Z
- **Commit:** [`4b69f40`](https://github.com/psantamaria/client_java/commit/4b69f40bd4e616d69468ce99dc4323162287a577)
- **JDK:** 25.0.2 (OpenJDK 64-Bit Server VM)
- **Benchmark config:** 3 fork(s), 3 warmup, 5 measurement, 4 threads
- **Hardware:** AMD EPYC 7763 64-Core Processor, 4 cores, 16 GB RAM
- **OS:** Linux 6.17.0-1022-azure

## Results

### CounterBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusInc | 66.71K | ± 736.92 | ops/s | **fastest** |
| prometheusNoLabelsInc | 56.64K | ± 409.30 | ops/s | 1.2x slower |
| prometheusAdd | 50.87K | ± 738.60 | ops/s | 1.3x slower |
| codahaleIncNoLabels | 49.21K | ± 1.58K | ops/s | 1.4x slower |
| simpleclientInc | 6.66K | ± 64.18 | ops/s | 10x slower |
| simpleclientNoLabelsInc | 6.60K | ± 19.03 | ops/s | 10x slower |
| simpleclientAdd | 6.18K | ± 239.51 | ops/s | 11x slower |
| openTelemetryIncNoLabels | 1.38K | ± 262.24 | ops/s | 48x slower |
| openTelemetryAdd | 1.27K | ± 11.74 | ops/s | 53x slower |
| openTelemetryInc | 1.22K | ± 32.37 | ops/s | 55x slower |

### HistogramBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusClassic | 5.68K | ± 1.17K | ops/s | **fastest** |
| simpleclient | 4.36K | ± 31.54 | ops/s | 1.3x slower |
| prometheusNative | 2.82K | ± 327.55 | ops/s | 2.0x slower |
| openTelemetryClassic | 700.23 | ± 53.19 | ops/s | 8.1x slower |
| openTelemetryExponential | 565.23 | ± 19.81 | ops/s | 10x slower |

### TextFormatUtilBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusWriteToNull | 485.22K | ± 4.24K | ops/s | **fastest** |
| openMetricsWriteToNull | 480.42K | ± 2.51K | ops/s | 1.0x slower |
| prometheusWriteToByteArray | 476.09K | ± 6.39K | ops/s | 1.0x slower |
| openMetricsWriteToByteArray | 466.42K | ± 4.10K | ops/s | 1.0x slower |

### Raw Results

```
Benchmark                                            Mode  Cnt          Score        Error  Units
CounterBenchmark.codahaleIncNoLabels                thrpt   15      49211.419   ± 1583.677  ops/s
CounterBenchmark.openTelemetryAdd                   thrpt   15       1268.425     ± 11.743  ops/s
CounterBenchmark.openTelemetryInc                   thrpt   15       1216.750     ± 32.375  ops/s
CounterBenchmark.openTelemetryIncNoLabels           thrpt   15       1382.856    ± 262.239  ops/s
CounterBenchmark.prometheusAdd                      thrpt   15      50865.268    ± 738.596  ops/s
CounterBenchmark.prometheusInc                      thrpt   15      66709.708    ± 736.925  ops/s
CounterBenchmark.prometheusNoLabelsInc              thrpt   15      56643.068    ± 409.300  ops/s
CounterBenchmark.simpleclientAdd                    thrpt   15       6176.074    ± 239.512  ops/s
CounterBenchmark.simpleclientInc                    thrpt   15       6657.750     ± 64.180  ops/s
CounterBenchmark.simpleclientNoLabelsInc            thrpt   15       6597.619     ± 19.028  ops/s
HistogramBenchmark.openTelemetryClassic             thrpt   15        700.234     ± 53.187  ops/s
HistogramBenchmark.openTelemetryExponential         thrpt   15        565.227     ± 19.812  ops/s
HistogramBenchmark.prometheusClassic                thrpt   15       5681.260   ± 1171.462  ops/s
HistogramBenchmark.prometheusNative                 thrpt   15       2823.873    ± 327.553  ops/s
HistogramBenchmark.simpleclient                     thrpt   15       4363.890     ± 31.537  ops/s
TextFormatUtilBenchmark.openMetricsWriteToByteArray  thrpt   15     466422.761   ± 4100.860  ops/s
TextFormatUtilBenchmark.openMetricsWriteToNull      thrpt   15     480420.597   ± 2505.866  ops/s
TextFormatUtilBenchmark.prometheusWriteToByteArray  thrpt   15     476088.949   ± 6386.735  ops/s
TextFormatUtilBenchmark.prometheusWriteToNull       thrpt   15     485216.560   ± 4244.474  ops/s
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
