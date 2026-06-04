# Prometheus Java Client Benchmarks

## Run Information

- **Date:** 2026-06-04T07:55:07Z
- **Commit:** [`4b69f40`](https://github.com/psantamaria/client_java/commit/4b69f40bd4e616d69468ce99dc4323162287a577)
- **JDK:** 25.0.2 (OpenJDK 64-Bit Server VM)
- **Benchmark config:** 3 fork(s), 3 warmup, 5 measurement, 4 threads
- **Hardware:** AMD EPYC 9V74 80-Core Processor, 4 cores, 16 GB RAM
- **OS:** Linux 6.17.0-1015-azure

## Results

### CounterBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusInc | 58.79K | ± 2.99K | ops/s | **fastest** |
| prometheusNoLabelsInc | 51.53K | ± 627.34 | ops/s | 1.1x slower |
| prometheusAdd | 48.39K | ± 414.43 | ops/s | 1.2x slower |
| codahaleIncNoLabels | 44.53K | ± 744.45 | ops/s | 1.3x slower |
| simpleclientInc | 6.30K | ± 89.93 | ops/s | 9.3x slower |
| simpleclientNoLabelsInc | 6.26K | ± 21.58 | ops/s | 9.4x slower |
| simpleclientAdd | 6.03K | ± 168.42 | ops/s | 9.7x slower |
| openTelemetryAdd | 1.39K | ± 123.80 | ops/s | 42x slower |
| openTelemetryInc | 1.32K | ± 140.58 | ops/s | 45x slower |
| openTelemetryIncNoLabels | 1.31K | ± 59.02 | ops/s | 45x slower |

### HistogramBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusClassic | 5.22K | ± 743.61 | ops/s | **fastest** |
| simpleclient | 4.46K | ± 98.99 | ops/s | 1.2x slower |
| prometheusNative | 2.93K | ± 221.81 | ops/s | 1.8x slower |
| openTelemetryClassic | 627.44 | ± 12.96 | ops/s | 8.3x slower |
| openTelemetryExponential | 533.71 | ± 10.92 | ops/s | 9.8x slower |

### TextFormatUtilBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusWriteToNull | 538.25K | ± 2.44K | ops/s | **fastest** |
| prometheusWriteToByteArray | 524.61K | ± 3.95K | ops/s | 1.0x slower |
| openMetricsWriteToNull | 524.24K | ± 4.85K | ops/s | 1.0x slower |
| openMetricsWriteToByteArray | 506.81K | ± 3.47K | ops/s | 1.1x slower |

### Raw Results

```
Benchmark                                            Mode  Cnt          Score        Error  Units
CounterBenchmark.codahaleIncNoLabels                thrpt   15      44528.140    ± 744.450  ops/s
CounterBenchmark.openTelemetryAdd                   thrpt   15       1389.869    ± 123.799  ops/s
CounterBenchmark.openTelemetryInc                   thrpt   15       1319.775    ± 140.581  ops/s
CounterBenchmark.openTelemetryIncNoLabels           thrpt   15       1314.220     ± 59.025  ops/s
CounterBenchmark.prometheusAdd                      thrpt   15      48390.283    ± 414.434  ops/s
CounterBenchmark.prometheusInc                      thrpt   15      58792.851   ± 2994.173  ops/s
CounterBenchmark.prometheusNoLabelsInc              thrpt   15      51530.276    ± 627.340  ops/s
CounterBenchmark.simpleclientAdd                    thrpt   15       6034.816    ± 168.424  ops/s
CounterBenchmark.simpleclientInc                    thrpt   15       6304.239     ± 89.926  ops/s
CounterBenchmark.simpleclientNoLabelsInc            thrpt   15       6259.002     ± 21.576  ops/s
HistogramBenchmark.openTelemetryClassic             thrpt   15        627.443     ± 12.959  ops/s
HistogramBenchmark.openTelemetryExponential         thrpt   15        533.709     ± 10.923  ops/s
HistogramBenchmark.prometheusClassic                thrpt   15       5220.239    ± 743.606  ops/s
HistogramBenchmark.prometheusNative                 thrpt   15       2928.378    ± 221.815  ops/s
HistogramBenchmark.simpleclient                     thrpt   15       4457.243     ± 98.991  ops/s
TextFormatUtilBenchmark.openMetricsWriteToByteArray  thrpt   15     506806.062   ± 3471.318  ops/s
TextFormatUtilBenchmark.openMetricsWriteToNull      thrpt   15     524240.629   ± 4848.717  ops/s
TextFormatUtilBenchmark.prometheusWriteToByteArray  thrpt   15     524610.153   ± 3950.233  ops/s
TextFormatUtilBenchmark.prometheusWriteToNull       thrpt   15     538247.871   ± 2443.822  ops/s
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
