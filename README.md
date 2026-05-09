# Prometheus Java Client Benchmarks

## Run Information

- **Date:** 2026-05-09T06:34:36Z
- **Commit:** [`4b69f40`](https://github.com/psantamaria/client_java/commit/4b69f40bd4e616d69468ce99dc4323162287a577)
- **JDK:** 25.0.2 (OpenJDK 64-Bit Server VM)
- **Benchmark config:** 3 fork(s), 3 warmup, 5 measurement, 4 threads
- **Hardware:** Intel(R) Xeon(R) Platinum 8370C CPU @ 2.80GHz, 4 cores, 16 GB RAM
- **OS:** Linux 6.17.0-1010-azure

## Results

### CounterBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusInc | 30.74K | ± 1.31K | ops/s | **fastest** |
| prometheusNoLabelsInc | 30.18K | ± 1.12K | ops/s | 1.0x slower |
| codahaleIncNoLabels | 29.33K | ± 1.77K | ops/s | 1.0x slower |
| prometheusAdd | 28.48K | ± 27.22 | ops/s | 1.1x slower |
| simpleclientNoLabelsInc | 6.99K | ± 48.36 | ops/s | 4.4x slower |
| simpleclientInc | 6.85K | ± 100.10 | ops/s | 4.5x slower |
| simpleclientAdd | 6.74K | ± 35.01 | ops/s | 4.6x slower |
| openTelemetryAdd | 1.41K | ± 74.65 | ops/s | 22x slower |
| openTelemetryInc | 1.39K | ± 90.00 | ops/s | 22x slower |
| openTelemetryIncNoLabels | 1.36K | ± 91.25 | ops/s | 23x slower |

### HistogramBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| simpleclient | 4.50K | ± 106.46 | ops/s | **fastest** |
| prometheusClassic | 4.04K | ± 1.95K | ops/s | 1.1x slower |
| prometheusNative | 2.30K | ± 251.01 | ops/s | 2.0x slower |
| openTelemetryClassic | 548.11 | ± 34.56 | ops/s | 8.2x slower |
| openTelemetryExponential | 448.02 | ± 7.40 | ops/s | 10x slower |

### TextFormatUtilBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusWriteToNull | 321.84K | ± 1.86K | ops/s | **fastest** |
| prometheusWriteToByteArray | 319.27K | ± 2.32K | ops/s | 1.0x slower |
| openMetricsWriteToNull | 301.80K | ± 1.81K | ops/s | 1.1x slower |
| openMetricsWriteToByteArray | 299.13K | ± 1.16K | ops/s | 1.1x slower |

### Raw Results

```
Benchmark                                            Mode  Cnt          Score        Error  Units
CounterBenchmark.codahaleIncNoLabels                thrpt   15      29331.077   ± 1771.306  ops/s
CounterBenchmark.openTelemetryAdd                   thrpt   15       1405.236     ± 74.651  ops/s
CounterBenchmark.openTelemetryInc                   thrpt   15       1386.714     ± 90.004  ops/s
CounterBenchmark.openTelemetryIncNoLabels           thrpt   15       1358.666     ± 91.249  ops/s
CounterBenchmark.prometheusAdd                      thrpt   15      28476.478     ± 27.219  ops/s
CounterBenchmark.prometheusInc                      thrpt   15      30742.972   ± 1310.523  ops/s
CounterBenchmark.prometheusNoLabelsInc              thrpt   15      30183.148   ± 1118.348  ops/s
CounterBenchmark.simpleclientAdd                    thrpt   15       6744.244     ± 35.007  ops/s
CounterBenchmark.simpleclientInc                    thrpt   15       6849.900    ± 100.102  ops/s
CounterBenchmark.simpleclientNoLabelsInc            thrpt   15       6992.769     ± 48.362  ops/s
HistogramBenchmark.openTelemetryClassic             thrpt   15        548.110     ± 34.558  ops/s
HistogramBenchmark.openTelemetryExponential         thrpt   15        448.021      ± 7.403  ops/s
HistogramBenchmark.prometheusClassic                thrpt   15       4038.978   ± 1949.506  ops/s
HistogramBenchmark.prometheusNative                 thrpt   15       2297.214    ± 251.015  ops/s
HistogramBenchmark.simpleclient                     thrpt   15       4497.461    ± 106.463  ops/s
TextFormatUtilBenchmark.openMetricsWriteToByteArray  thrpt   15     299132.210   ± 1159.268  ops/s
TextFormatUtilBenchmark.openMetricsWriteToNull      thrpt   15     301797.282   ± 1806.310  ops/s
TextFormatUtilBenchmark.prometheusWriteToByteArray  thrpt   15     319267.798   ± 2316.255  ops/s
TextFormatUtilBenchmark.prometheusWriteToNull       thrpt   15     321844.599   ± 1858.352  ops/s
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
