# Prometheus Java Client Benchmarks

## Run Information

- **Date:** 2026-08-17T04:10:43Z
- **Commit:** [`4b69f40`](https://github.com/psantamaria/client_java/commit/4b69f40bd4e616d69468ce99dc4323162287a577)
- **JDK:** 25.0.2 (OpenJDK 64-Bit Server VM)
- **Benchmark config:** 3 fork(s), 3 warmup, 5 measurement, 4 threads
- **Hardware:** AMD EPYC 7763 64-Core Processor, 4 cores, 16 GB RAM
- **OS:** Linux 6.17.0-1022-azure

## Results

### CounterBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusInc | 61.79K | ± 2.81K | ops/s | **fastest** |
| prometheusNoLabelsInc | 56.59K | ± 673.06 | ops/s | 1.1x slower |
| prometheusAdd | 50.25K | ± 67.81 | ops/s | 1.2x slower |
| codahaleIncNoLabels | 49.53K | ± 524.33 | ops/s | 1.2x slower |
| simpleclientInc | 6.69K | ± 12.39 | ops/s | 9.2x slower |
| simpleclientNoLabelsInc | 6.48K | ± 198.98 | ops/s | 9.5x slower |
| simpleclientAdd | 6.46K | ± 15.31 | ops/s | 9.6x slower |
| openTelemetryIncNoLabels | 1.40K | ± 208.54 | ops/s | 44x slower |
| openTelemetryAdd | 1.39K | ± 216.05 | ops/s | 45x slower |
| openTelemetryInc | 1.37K | ± 202.52 | ops/s | 45x slower |

### HistogramBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusClassic | 6.00K | ± 1.34K | ops/s | **fastest** |
| simpleclient | 4.48K | ± 65.81 | ops/s | 1.3x slower |
| prometheusNative | 3.01K | ± 267.12 | ops/s | 2.0x slower |
| openTelemetryClassic | 657.31 | ± 15.84 | ops/s | 9.1x slower |
| openTelemetryExponential | 529.60 | ± 14.12 | ops/s | 11x slower |

### TextFormatUtilBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| openMetricsWriteToNull | 490.89K | ± 1.36K | ops/s | **fastest** |
| prometheusWriteToByteArray | 490.78K | ± 1.79K | ops/s | 1.0x slower |
| prometheusWriteToNull | 490.59K | ± 1.10K | ops/s | 1.0x slower |
| openMetricsWriteToByteArray | 479.07K | ± 4.65K | ops/s | 1.0x slower |

### Raw Results

```
Benchmark                                            Mode  Cnt          Score        Error  Units
CounterBenchmark.codahaleIncNoLabels                thrpt   15      49525.465    ± 524.329  ops/s
CounterBenchmark.openTelemetryAdd                   thrpt   15       1385.136    ± 216.046  ops/s
CounterBenchmark.openTelemetryInc                   thrpt   15       1373.371    ± 202.518  ops/s
CounterBenchmark.openTelemetryIncNoLabels           thrpt   15       1401.199    ± 208.544  ops/s
CounterBenchmark.prometheusAdd                      thrpt   15      50254.389     ± 67.813  ops/s
CounterBenchmark.prometheusInc                      thrpt   15      61786.667   ± 2808.396  ops/s
CounterBenchmark.prometheusNoLabelsInc              thrpt   15      56594.160    ± 673.060  ops/s
CounterBenchmark.simpleclientAdd                    thrpt   15       6456.609     ± 15.311  ops/s
CounterBenchmark.simpleclientInc                    thrpt   15       6686.623     ± 12.388  ops/s
CounterBenchmark.simpleclientNoLabelsInc            thrpt   15       6475.519    ± 198.978  ops/s
HistogramBenchmark.openTelemetryClassic             thrpt   15        657.309     ± 15.843  ops/s
HistogramBenchmark.openTelemetryExponential         thrpt   15        529.600     ± 14.122  ops/s
HistogramBenchmark.prometheusClassic                thrpt   15       6004.963   ± 1340.551  ops/s
HistogramBenchmark.prometheusNative                 thrpt   15       3012.917    ± 267.116  ops/s
HistogramBenchmark.simpleclient                     thrpt   15       4476.089     ± 65.808  ops/s
TextFormatUtilBenchmark.openMetricsWriteToByteArray  thrpt   15     479074.762   ± 4653.394  ops/s
TextFormatUtilBenchmark.openMetricsWriteToNull      thrpt   15     490892.001   ± 1356.912  ops/s
TextFormatUtilBenchmark.prometheusWriteToByteArray  thrpt   15     490782.375   ± 1794.405  ops/s
TextFormatUtilBenchmark.prometheusWriteToNull       thrpt   15     490594.759   ± 1095.586  ops/s
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
