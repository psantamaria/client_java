# Prometheus Java Client Benchmarks

## Run Information

- **Date:** 2026-05-22T07:18:14Z
- **Commit:** [`4b69f40`](https://github.com/psantamaria/client_java/commit/4b69f40bd4e616d69468ce99dc4323162287a577)
- **JDK:** 25.0.2 (OpenJDK 64-Bit Server VM)
- **Benchmark config:** 3 fork(s), 3 warmup, 5 measurement, 4 threads
- **Hardware:** Intel(R) Xeon(R) Platinum 8370C CPU @ 2.80GHz, 4 cores, 16 GB RAM
- **OS:** Linux 6.17.0-1013-azure

## Results

### CounterBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusInc | 31.51K | ± 12.73 | ops/s | **fastest** |
| prometheusNoLabelsInc | 29.92K | ± 935.24 | ops/s | 1.1x slower |
| codahaleIncNoLabels | 29.39K | ± 164.74 | ops/s | 1.1x slower |
| prometheusAdd | 27.44K | ± 1.86K | ops/s | 1.1x slower |
| simpleclientInc | 6.83K | ± 162.69 | ops/s | 4.6x slower |
| simpleclientNoLabelsInc | 6.82K | ± 161.48 | ops/s | 4.6x slower |
| simpleclientAdd | 6.42K | ± 188.37 | ops/s | 4.9x slower |
| openTelemetryIncNoLabels | 1.48K | ± 120.28 | ops/s | 21x slower |
| openTelemetryAdd | 1.34K | ± 80.98 | ops/s | 24x slower |
| openTelemetryInc | 1.30K | ± 8.91 | ops/s | 24x slower |

### HistogramBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| simpleclient | 4.50K | ± 22.46 | ops/s | **fastest** |
| prometheusClassic | 2.94K | ± 492.90 | ops/s | 1.5x slower |
| prometheusNative | 2.07K | ± 109.44 | ops/s | 2.2x slower |
| openTelemetryClassic | 500.86 | ± 32.34 | ops/s | 9.0x slower |
| openTelemetryExponential | 393.76 | ± 17.26 | ops/s | 11x slower |

### TextFormatUtilBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusWriteToNull | 316.43K | ± 1.60K | ops/s | **fastest** |
| prometheusWriteToByteArray | 313.47K | ± 1.94K | ops/s | 1.0x slower |
| openMetricsWriteToNull | 299.43K | ± 2.79K | ops/s | 1.1x slower |
| openMetricsWriteToByteArray | 298.35K | ± 2.91K | ops/s | 1.1x slower |

### Raw Results

```
Benchmark                                            Mode  Cnt          Score        Error  Units
CounterBenchmark.codahaleIncNoLabels                thrpt   15      29387.533    ± 164.736  ops/s
CounterBenchmark.openTelemetryAdd                   thrpt   15       1336.078     ± 80.981  ops/s
CounterBenchmark.openTelemetryInc                   thrpt   15       1303.169      ± 8.907  ops/s
CounterBenchmark.openTelemetryIncNoLabels           thrpt   15       1477.368    ± 120.284  ops/s
CounterBenchmark.prometheusAdd                      thrpt   15      27439.077   ± 1855.304  ops/s
CounterBenchmark.prometheusInc                      thrpt   15      31510.600     ± 12.729  ops/s
CounterBenchmark.prometheusNoLabelsInc              thrpt   15      29924.956    ± 935.241  ops/s
CounterBenchmark.simpleclientAdd                    thrpt   15       6420.212    ± 188.367  ops/s
CounterBenchmark.simpleclientInc                    thrpt   15       6834.586    ± 162.693  ops/s
CounterBenchmark.simpleclientNoLabelsInc            thrpt   15       6818.353    ± 161.476  ops/s
HistogramBenchmark.openTelemetryClassic             thrpt   15        500.862     ± 32.338  ops/s
HistogramBenchmark.openTelemetryExponential         thrpt   15        393.765     ± 17.261  ops/s
HistogramBenchmark.prometheusClassic                thrpt   15       2944.521    ± 492.900  ops/s
HistogramBenchmark.prometheusNative                 thrpt   15       2072.534    ± 109.439  ops/s
HistogramBenchmark.simpleclient                     thrpt   15       4497.015     ± 22.463  ops/s
TextFormatUtilBenchmark.openMetricsWriteToByteArray  thrpt   15     298354.272   ± 2913.338  ops/s
TextFormatUtilBenchmark.openMetricsWriteToNull      thrpt   15     299428.475   ± 2792.526  ops/s
TextFormatUtilBenchmark.prometheusWriteToByteArray  thrpt   15     313473.256   ± 1936.675  ops/s
TextFormatUtilBenchmark.prometheusWriteToNull       thrpt   15     316430.458   ± 1597.666  ops/s
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
