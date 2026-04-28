# Prometheus Java Client Benchmarks

## Run Information

- **Date:** 2026-04-28T06:43:52Z
- **Commit:** [`4b69f40`](https://github.com/psantamaria/client_java/commit/4b69f40bd4e616d69468ce99dc4323162287a577)
- **JDK:** 25.0.2 (OpenJDK 64-Bit Server VM)
- **Benchmark config:** 3 fork(s), 3 warmup, 5 measurement, 4 threads
- **Hardware:** Intel(R) Xeon(R) Platinum 8370C CPU @ 2.80GHz, 4 cores, 16 GB RAM
- **OS:** Linux 6.17.0-1010-azure

## Results

### CounterBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusNoLabelsInc | 31.11K | ± 28.66 | ops/s | **fastest** |
| prometheusInc | 30.71K | ± 1.30K | ops/s | 1.0x slower |
| codahaleIncNoLabels | 29.56K | ± 666.66 | ops/s | 1.1x slower |
| prometheusAdd | 28.04K | ± 739.92 | ops/s | 1.1x slower |
| simpleclientInc | 6.83K | ± 109.35 | ops/s | 4.6x slower |
| simpleclientNoLabelsInc | 6.75K | ± 215.47 | ops/s | 4.6x slower |
| simpleclientAdd | 6.58K | ± 175.30 | ops/s | 4.7x slower |
| openTelemetryInc | 1.44K | ± 150.27 | ops/s | 22x slower |
| openTelemetryIncNoLabels | 1.44K | ± 153.51 | ops/s | 22x slower |
| openTelemetryAdd | 1.37K | ± 30.14 | ops/s | 23x slower |

### HistogramBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| simpleclient | 4.43K | ± 44.06 | ops/s | **fastest** |
| prometheusClassic | 3.53K | ± 173.59 | ops/s | 1.3x slower |
| prometheusNative | 2.38K | ± 217.86 | ops/s | 1.9x slower |
| openTelemetryClassic | 522.81 | ± 21.86 | ops/s | 8.5x slower |
| openTelemetryExponential | 417.49 | ± 8.90 | ops/s | 11x slower |

### TextFormatUtilBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusWriteToByteArray | 315.16K | ± 2.03K | ops/s | **fastest** |
| prometheusWriteToNull | 314.50K | ± 1.88K | ops/s | 1.0x slower |
| openMetricsWriteToNull | 296.75K | ± 2.98K | ops/s | 1.1x slower |
| openMetricsWriteToByteArray | 293.87K | ± 2.53K | ops/s | 1.1x slower |

### Raw Results

```
Benchmark                                            Mode  Cnt          Score        Error  Units
CounterBenchmark.codahaleIncNoLabels                thrpt   15      29555.658    ± 666.662  ops/s
CounterBenchmark.openTelemetryAdd                   thrpt   15       1374.846     ± 30.140  ops/s
CounterBenchmark.openTelemetryInc                   thrpt   15       1437.980    ± 150.267  ops/s
CounterBenchmark.openTelemetryIncNoLabels           thrpt   15       1435.296    ± 153.507  ops/s
CounterBenchmark.prometheusAdd                      thrpt   15      28039.588    ± 739.922  ops/s
CounterBenchmark.prometheusInc                      thrpt   15      30711.725   ± 1302.932  ops/s
CounterBenchmark.prometheusNoLabelsInc              thrpt   15      31114.193     ± 28.660  ops/s
CounterBenchmark.simpleclientAdd                    thrpt   15       6579.192    ± 175.301  ops/s
CounterBenchmark.simpleclientInc                    thrpt   15       6830.517    ± 109.352  ops/s
CounterBenchmark.simpleclientNoLabelsInc            thrpt   15       6746.239    ± 215.467  ops/s
HistogramBenchmark.openTelemetryClassic             thrpt   15        522.806     ± 21.857  ops/s
HistogramBenchmark.openTelemetryExponential         thrpt   15        417.489      ± 8.896  ops/s
HistogramBenchmark.prometheusClassic                thrpt   15       3533.976    ± 173.586  ops/s
HistogramBenchmark.prometheusNative                 thrpt   15       2382.156    ± 217.858  ops/s
HistogramBenchmark.simpleclient                     thrpt   15       4430.769     ± 44.059  ops/s
TextFormatUtilBenchmark.openMetricsWriteToByteArray  thrpt   15     293872.628   ± 2531.492  ops/s
TextFormatUtilBenchmark.openMetricsWriteToNull      thrpt   15     296752.460   ± 2981.787  ops/s
TextFormatUtilBenchmark.prometheusWriteToByteArray  thrpt   15     315162.209   ± 2033.471  ops/s
TextFormatUtilBenchmark.prometheusWriteToNull       thrpt   15     314496.853   ± 1879.214  ops/s
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
