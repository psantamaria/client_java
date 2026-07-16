# Prometheus Java Client Benchmarks

## Run Information

- **Date:** 2026-07-16T06:12:34Z
- **Commit:** [`4b69f40`](https://github.com/psantamaria/client_java/commit/4b69f40bd4e616d69468ce99dc4323162287a577)
- **JDK:** 25.0.2 (OpenJDK 64-Bit Server VM)
- **Benchmark config:** 3 fork(s), 3 warmup, 5 measurement, 4 threads
- **Hardware:** AMD EPYC 7763 64-Core Processor, 4 cores, 16 GB RAM
- **OS:** Linux 6.17.0-1018-azure

## Results

### CounterBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusInc | 61.32K | ± 793.55 | ops/s | **fastest** |
| prometheusNoLabelsInc | 52.88K | ± 555.65 | ops/s | 1.2x slower |
| prometheusAdd | 47.12K | ± 626.84 | ops/s | 1.3x slower |
| codahaleIncNoLabels | 45.48K | ± 1.20K | ops/s | 1.3x slower |
| simpleclientNoLabelsInc | 6.11K | ± 148.34 | ops/s | 10x slower |
| simpleclientInc | 6.01K | ± 176.69 | ops/s | 10x slower |
| simpleclientAdd | 5.93K | ± 272.20 | ops/s | 10x slower |
| openTelemetryInc | 1.21K | ± 38.93 | ops/s | 51x slower |
| openTelemetryAdd | 1.15K | ± 18.78 | ops/s | 53x slower |
| openTelemetryIncNoLabels | 1.13K | ± 24.75 | ops/s | 54x slower |

### HistogramBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusClassic | 5.22K | ± 1.32K | ops/s | **fastest** |
| simpleclient | 4.13K | ± 52.75 | ops/s | 1.3x slower |
| prometheusNative | 2.82K | ± 264.74 | ops/s | 1.9x slower |
| openTelemetryClassic | 636.86 | ± 34.80 | ops/s | 8.2x slower |
| openTelemetryExponential | 520.31 | ± 4.39 | ops/s | 10x slower |

### TextFormatUtilBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusWriteToByteArray | 396.11K | ± 10.13K | ops/s | **fastest** |
| openMetricsWriteToNull | 367.32K | ± 12.13K | ops/s | 1.1x slower |
| openMetricsWriteToByteArray | 361.21K | ± 7.37K | ops/s | 1.1x slower |
| prometheusWriteToNull | 358.64K | ± 15.74K | ops/s | 1.1x slower |

### Raw Results

```
Benchmark                                            Mode  Cnt          Score        Error  Units
CounterBenchmark.codahaleIncNoLabels                thrpt   15      45479.149   ± 1198.083  ops/s
CounterBenchmark.openTelemetryAdd                   thrpt   15       1146.508     ± 18.783  ops/s
CounterBenchmark.openTelemetryInc                   thrpt   15       1212.701     ± 38.927  ops/s
CounterBenchmark.openTelemetryIncNoLabels           thrpt   15       1133.483     ± 24.748  ops/s
CounterBenchmark.prometheusAdd                      thrpt   15      47122.246    ± 626.843  ops/s
CounterBenchmark.prometheusInc                      thrpt   15      61323.913    ± 793.555  ops/s
CounterBenchmark.prometheusNoLabelsInc              thrpt   15      52877.733    ± 555.652  ops/s
CounterBenchmark.simpleclientAdd                    thrpt   15       5933.488    ± 272.197  ops/s
CounterBenchmark.simpleclientInc                    thrpt   15       6011.181    ± 176.694  ops/s
CounterBenchmark.simpleclientNoLabelsInc            thrpt   15       6112.705    ± 148.345  ops/s
HistogramBenchmark.openTelemetryClassic             thrpt   15        636.865     ± 34.802  ops/s
HistogramBenchmark.openTelemetryExponential         thrpt   15        520.311      ± 4.387  ops/s
HistogramBenchmark.prometheusClassic                thrpt   15       5224.389   ± 1319.324  ops/s
HistogramBenchmark.prometheusNative                 thrpt   15       2816.041    ± 264.741  ops/s
HistogramBenchmark.simpleclient                     thrpt   15       4125.598     ± 52.754  ops/s
TextFormatUtilBenchmark.openMetricsWriteToByteArray  thrpt   15     361208.145   ± 7368.770  ops/s
TextFormatUtilBenchmark.openMetricsWriteToNull      thrpt   15     367323.234  ± 12131.119  ops/s
TextFormatUtilBenchmark.prometheusWriteToByteArray  thrpt   15     396112.672  ± 10129.430  ops/s
TextFormatUtilBenchmark.prometheusWriteToNull       thrpt   15     358638.879  ± 15741.532  ops/s
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
