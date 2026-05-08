# Prometheus Java Client Benchmarks

## Run Information

- **Date:** 2026-05-08T06:07:27Z
- **Commit:** [`4b69f40`](https://github.com/psantamaria/client_java/commit/4b69f40bd4e616d69468ce99dc4323162287a577)
- **JDK:** 25.0.2 (OpenJDK 64-Bit Server VM)
- **Benchmark config:** 3 fork(s), 3 warmup, 5 measurement, 4 threads
- **Hardware:** AMD EPYC 7763 64-Core Processor, 4 cores, 16 GB RAM
- **OS:** Linux 6.17.0-1010-azure

## Results

### CounterBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusInc | 64.14K | ± 3.79K | ops/s | **fastest** |
| prometheusNoLabelsInc | 56.01K | ± 728.83 | ops/s | 1.1x slower |
| prometheusAdd | 50.80K | ± 593.35 | ops/s | 1.3x slower |
| codahaleIncNoLabels | 48.41K | ± 2.03K | ops/s | 1.3x slower |
| simpleclientInc | 6.51K | ± 177.45 | ops/s | 9.9x slower |
| simpleclientNoLabelsInc | 6.48K | ± 186.96 | ops/s | 9.9x slower |
| simpleclientAdd | 6.31K | ± 240.86 | ops/s | 10x slower |
| openTelemetryAdd | 1.36K | ± 65.04 | ops/s | 47x slower |
| openTelemetryInc | 1.32K | ± 219.18 | ops/s | 49x slower |
| openTelemetryIncNoLabels | 1.13K | ± 76.39 | ops/s | 57x slower |

### HistogramBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusClassic | 4.48K | ± 363.32 | ops/s | **fastest** |
| simpleclient | 4.43K | ± 62.29 | ops/s | 1.0x slower |
| prometheusNative | 2.92K | ± 262.28 | ops/s | 1.5x slower |
| openTelemetryClassic | 707.37 | ± 50.58 | ops/s | 6.3x slower |
| openTelemetryExponential | 558.66 | ± 32.64 | ops/s | 8.0x slower |

### TextFormatUtilBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusWriteToNull | 488.55K | ± 1.55K | ops/s | **fastest** |
| prometheusWriteToByteArray | 479.98K | ± 5.65K | ops/s | 1.0x slower |
| openMetricsWriteToNull | 477.29K | ± 3.09K | ops/s | 1.0x slower |
| openMetricsWriteToByteArray | 471.59K | ± 5.28K | ops/s | 1.0x slower |

### Raw Results

```
Benchmark                                            Mode  Cnt          Score        Error  Units
CounterBenchmark.codahaleIncNoLabels                thrpt   15      48412.757   ± 2028.083  ops/s
CounterBenchmark.openTelemetryAdd                   thrpt   15       1363.799     ± 65.040  ops/s
CounterBenchmark.openTelemetryInc                   thrpt   15       1318.262    ± 219.176  ops/s
CounterBenchmark.openTelemetryIncNoLabels           thrpt   15       1132.664     ± 76.387  ops/s
CounterBenchmark.prometheusAdd                      thrpt   15      50798.169    ± 593.350  ops/s
CounterBenchmark.prometheusInc                      thrpt   15      64136.024   ± 3791.440  ops/s
CounterBenchmark.prometheusNoLabelsInc              thrpt   15      56010.058    ± 728.831  ops/s
CounterBenchmark.simpleclientAdd                    thrpt   15       6311.824    ± 240.858  ops/s
CounterBenchmark.simpleclientInc                    thrpt   15       6505.503    ± 177.445  ops/s
CounterBenchmark.simpleclientNoLabelsInc            thrpt   15       6476.575    ± 186.963  ops/s
HistogramBenchmark.openTelemetryClassic             thrpt   15        707.368     ± 50.583  ops/s
HistogramBenchmark.openTelemetryExponential         thrpt   15        558.656     ± 32.640  ops/s
HistogramBenchmark.prometheusClassic                thrpt   15       4480.452    ± 363.317  ops/s
HistogramBenchmark.prometheusNative                 thrpt   15       2917.417    ± 262.281  ops/s
HistogramBenchmark.simpleclient                     thrpt   15       4429.433     ± 62.293  ops/s
TextFormatUtilBenchmark.openMetricsWriteToByteArray  thrpt   15     471588.051   ± 5284.453  ops/s
TextFormatUtilBenchmark.openMetricsWriteToNull      thrpt   15     477292.070   ± 3094.099  ops/s
TextFormatUtilBenchmark.prometheusWriteToByteArray  thrpt   15     479980.799   ± 5648.708  ops/s
TextFormatUtilBenchmark.prometheusWriteToNull       thrpt   15     488545.231   ± 1551.814  ops/s
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
