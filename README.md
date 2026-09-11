# Prometheus Java Client Benchmarks

## Run Information

- **Date:** 2026-09-11T08:11:18Z
- **Commit:** [`4b69f40`](https://github.com/psantamaria/client_java/commit/4b69f40bd4e616d69468ce99dc4323162287a577)
- **JDK:** 25.0.2 (OpenJDK 64-Bit Server VM)
- **Benchmark config:** 3 fork(s), 3 warmup, 5 measurement, 4 threads
- **Hardware:** AMD EPYC 7763 64-Core Processor, 4 cores, 16 GB RAM
- **OS:** Linux 6.17.0-1022-azure

## Results

### CounterBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusInc | 65.49K | ± 1.42K | ops/s | **fastest** |
| prometheusNoLabelsInc | 56.51K | ± 587.45 | ops/s | 1.2x slower |
| prometheusAdd | 49.49K | ± 1.89K | ops/s | 1.3x slower |
| codahaleIncNoLabels | 48.20K | ± 1.58K | ops/s | 1.4x slower |
| simpleclientNoLabelsInc | 6.35K | ± 199.23 | ops/s | 10x slower |
| simpleclientInc | 6.30K | ± 65.81 | ops/s | 10x slower |
| simpleclientAdd | 6.13K | ± 304.02 | ops/s | 11x slower |
| openTelemetryIncNoLabels | 1.51K | ± 160.40 | ops/s | 43x slower |
| openTelemetryAdd | 1.49K | ± 211.85 | ops/s | 44x slower |
| openTelemetryInc | 1.21K | ± 14.31 | ops/s | 54x slower |

### HistogramBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusClassic | 6.02K | ± 893.47 | ops/s | **fastest** |
| simpleclient | 4.45K | ± 37.74 | ops/s | 1.4x slower |
| prometheusNative | 2.79K | ± 302.57 | ops/s | 2.2x slower |
| openTelemetryClassic | 676.15 | ± 14.71 | ops/s | 8.9x slower |
| openTelemetryExponential | 572.98 | ± 40.26 | ops/s | 11x slower |

### TextFormatUtilBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusWriteToNull | 483.07K | ± 3.20K | ops/s | **fastest** |
| prometheusWriteToByteArray | 476.09K | ± 7.28K | ops/s | 1.0x slower |
| openMetricsWriteToNull | 468.83K | ± 2.02K | ops/s | 1.0x slower |
| openMetricsWriteToByteArray | 464.19K | ± 7.68K | ops/s | 1.0x slower |

### Raw Results

```
Benchmark                                            Mode  Cnt          Score        Error  Units
CounterBenchmark.codahaleIncNoLabels                thrpt   15      48202.421   ± 1576.212  ops/s
CounterBenchmark.openTelemetryAdd                   thrpt   15       1490.109    ± 211.852  ops/s
CounterBenchmark.openTelemetryInc                   thrpt   15       1208.146     ± 14.310  ops/s
CounterBenchmark.openTelemetryIncNoLabels           thrpt   15       1513.927    ± 160.397  ops/s
CounterBenchmark.prometheusAdd                      thrpt   15      49485.898   ± 1885.956  ops/s
CounterBenchmark.prometheusInc                      thrpt   15      65489.586   ± 1420.425  ops/s
CounterBenchmark.prometheusNoLabelsInc              thrpt   15      56509.848    ± 587.454  ops/s
CounterBenchmark.simpleclientAdd                    thrpt   15       6132.764    ± 304.020  ops/s
CounterBenchmark.simpleclientInc                    thrpt   15       6304.026     ± 65.812  ops/s
CounterBenchmark.simpleclientNoLabelsInc            thrpt   15       6354.487    ± 199.230  ops/s
HistogramBenchmark.openTelemetryClassic             thrpt   15        676.150     ± 14.709  ops/s
HistogramBenchmark.openTelemetryExponential         thrpt   15        572.978     ± 40.264  ops/s
HistogramBenchmark.prometheusClassic                thrpt   15       6024.255    ± 893.475  ops/s
HistogramBenchmark.prometheusNative                 thrpt   15       2793.962    ± 302.568  ops/s
HistogramBenchmark.simpleclient                     thrpt   15       4447.066     ± 37.735  ops/s
TextFormatUtilBenchmark.openMetricsWriteToByteArray  thrpt   15     464192.690   ± 7678.737  ops/s
TextFormatUtilBenchmark.openMetricsWriteToNull      thrpt   15     468828.143   ± 2022.421  ops/s
TextFormatUtilBenchmark.prometheusWriteToByteArray  thrpt   15     476087.245   ± 7283.707  ops/s
TextFormatUtilBenchmark.prometheusWriteToNull       thrpt   15     483066.731   ± 3203.431  ops/s
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
