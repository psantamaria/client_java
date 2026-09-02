# Prometheus Java Client Benchmarks

## Run Information

- **Date:** 2026-09-02T07:59:34Z
- **Commit:** [`4b69f40`](https://github.com/psantamaria/client_java/commit/4b69f40bd4e616d69468ce99dc4323162287a577)
- **JDK:** 25.0.2 (OpenJDK 64-Bit Server VM)
- **Benchmark config:** 3 fork(s), 3 warmup, 5 measurement, 4 threads
- **Hardware:** AMD EPYC 7763 64-Core Processor, 4 cores, 16 GB RAM
- **OS:** Linux 6.17.0-1022-azure

## Results

### CounterBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusInc | 64.94K | ± 1.82K | ops/s | **fastest** |
| prometheusNoLabelsInc | 56.89K | ± 387.46 | ops/s | 1.1x slower |
| prometheusAdd | 51.00K | ± 282.38 | ops/s | 1.3x slower |
| codahaleIncNoLabels | 49.61K | ± 919.50 | ops/s | 1.3x slower |
| simpleclientNoLabelsInc | 6.56K | ± 60.42 | ops/s | 9.9x slower |
| simpleclientInc | 6.56K | ± 198.12 | ops/s | 9.9x slower |
| simpleclientAdd | 5.94K | ± 104.40 | ops/s | 11x slower |
| openTelemetryInc | 1.43K | ± 251.08 | ops/s | 45x slower |
| openTelemetryAdd | 1.42K | ± 262.27 | ops/s | 46x slower |
| openTelemetryIncNoLabels | 1.19K | ± 35.44 | ops/s | 55x slower |

### HistogramBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusClassic | 6.38K | ± 2.33K | ops/s | **fastest** |
| simpleclient | 4.41K | ± 93.66 | ops/s | 1.4x slower |
| prometheusNative | 2.79K | ± 368.83 | ops/s | 2.3x slower |
| openTelemetryClassic | 677.92 | ± 10.17 | ops/s | 9.4x slower |
| openTelemetryExponential | 579.56 | ± 22.59 | ops/s | 11x slower |

### TextFormatUtilBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusWriteToNull | 487.01K | ± 2.35K | ops/s | **fastest** |
| prometheusWriteToByteArray | 479.71K | ± 4.62K | ops/s | 1.0x slower |
| openMetricsWriteToNull | 473.43K | ± 3.88K | ops/s | 1.0x slower |
| openMetricsWriteToByteArray | 470.03K | ± 5.34K | ops/s | 1.0x slower |

### Raw Results

```
Benchmark                                            Mode  Cnt          Score        Error  Units
CounterBenchmark.codahaleIncNoLabels                thrpt   15      49613.444    ± 919.501  ops/s
CounterBenchmark.openTelemetryAdd                   thrpt   15       1420.149    ± 262.274  ops/s
CounterBenchmark.openTelemetryInc                   thrpt   15       1428.803    ± 251.083  ops/s
CounterBenchmark.openTelemetryIncNoLabels           thrpt   15       1191.494     ± 35.440  ops/s
CounterBenchmark.prometheusAdd                      thrpt   15      51004.243    ± 282.378  ops/s
CounterBenchmark.prometheusInc                      thrpt   15      64941.387   ± 1818.494  ops/s
CounterBenchmark.prometheusNoLabelsInc              thrpt   15      56891.435    ± 387.456  ops/s
CounterBenchmark.simpleclientAdd                    thrpt   15       5936.045    ± 104.397  ops/s
CounterBenchmark.simpleclientInc                    thrpt   15       6555.979    ± 198.120  ops/s
CounterBenchmark.simpleclientNoLabelsInc            thrpt   15       6561.515     ± 60.418  ops/s
HistogramBenchmark.openTelemetryClassic             thrpt   15        677.921     ± 10.173  ops/s
HistogramBenchmark.openTelemetryExponential         thrpt   15        579.560     ± 22.594  ops/s
HistogramBenchmark.prometheusClassic                thrpt   15       6383.945   ± 2331.734  ops/s
HistogramBenchmark.prometheusNative                 thrpt   15       2788.997    ± 368.835  ops/s
HistogramBenchmark.simpleclient                     thrpt   15       4413.263     ± 93.664  ops/s
TextFormatUtilBenchmark.openMetricsWriteToByteArray  thrpt   15     470033.483   ± 5339.467  ops/s
TextFormatUtilBenchmark.openMetricsWriteToNull      thrpt   15     473425.665   ± 3878.027  ops/s
TextFormatUtilBenchmark.prometheusWriteToByteArray  thrpt   15     479707.398   ± 4617.543  ops/s
TextFormatUtilBenchmark.prometheusWriteToNull       thrpt   15     487008.078   ± 2348.929  ops/s
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
