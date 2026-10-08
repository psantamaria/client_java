# Prometheus Java Client Benchmarks

## Run Information

- **Date:** 2026-10-08T09:34:14Z
- **Commit:** [`4b69f40`](https://github.com/psantamaria/client_java/commit/4b69f40bd4e616d69468ce99dc4323162287a577)
- **JDK:** 25.0.2 (OpenJDK 64-Bit Server VM)
- **Benchmark config:** 3 fork(s), 3 warmup, 5 measurement, 4 threads
- **Hardware:** INTEL(R) XEON(R) PLATINUM 8573C, 4 cores, 16 GB RAM
- **OS:** Linux 6.17.0-1022-azure

## Results

### CounterBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| codahaleIncNoLabels | 27.25K | ± 203.80 | ops/s | **fastest** |
| prometheusNoLabelsInc | 26.55K | ± 262.32 | ops/s | 1.0x slower |
| prometheusInc | 26.47K | ± 41.36 | ops/s | 1.0x slower |
| prometheusAdd | 25.82K | ± 118.56 | ops/s | 1.1x slower |
| simpleclientInc | 6.68K | ± 67.86 | ops/s | 4.1x slower |
| simpleclientAdd | 6.63K | ± 48.16 | ops/s | 4.1x slower |
| simpleclientNoLabelsInc | 6.56K | ± 53.40 | ops/s | 4.2x slower |
| openTelemetryIncNoLabels | 1.05K | ± 55.79 | ops/s | 26x slower |
| openTelemetryAdd | 1.05K | ± 96.14 | ops/s | 26x slower |
| openTelemetryInc | 989.01 | ± 40.34 | ops/s | 28x slower |

### HistogramBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| simpleclient | 4.25K | ± 38.65 | ops/s | **fastest** |
| prometheusClassic | 3.01K | ± 483.75 | ops/s | 1.4x slower |
| prometheusNative | 2.30K | ± 188.44 | ops/s | 1.8x slower |
| openTelemetryClassic | 363.24 | ± 1.30 | ops/s | 12x slower |
| openTelemetryExponential | 306.33 | ± 4.62 | ops/s | 14x slower |

### TextFormatUtilBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusWriteToNull | 292.94K | ± 1.39K | ops/s | **fastest** |
| prometheusWriteToByteArray | 292.13K | ± 884.21 | ops/s | 1.0x slower |
| openMetricsWriteToNull | 276.09K | ± 2.20K | ops/s | 1.1x slower |
| openMetricsWriteToByteArray | 275.24K | ± 921.23 | ops/s | 1.1x slower |

### Raw Results

```
Benchmark                                            Mode  Cnt          Score        Error  Units
CounterBenchmark.codahaleIncNoLabels                thrpt   15      27248.081    ± 203.796  ops/s
CounterBenchmark.openTelemetryAdd                   thrpt   15       1053.109     ± 96.139  ops/s
CounterBenchmark.openTelemetryInc                   thrpt   15        989.015     ± 40.341  ops/s
CounterBenchmark.openTelemetryIncNoLabels           thrpt   15       1053.730     ± 55.788  ops/s
CounterBenchmark.prometheusAdd                      thrpt   15      25816.958    ± 118.561  ops/s
CounterBenchmark.prometheusInc                      thrpt   15      26470.482     ± 41.358  ops/s
CounterBenchmark.prometheusNoLabelsInc              thrpt   15      26548.791    ± 262.323  ops/s
CounterBenchmark.simpleclientAdd                    thrpt   15       6628.392     ± 48.155  ops/s
CounterBenchmark.simpleclientInc                    thrpt   15       6680.998     ± 67.856  ops/s
CounterBenchmark.simpleclientNoLabelsInc            thrpt   15       6557.516     ± 53.398  ops/s
HistogramBenchmark.openTelemetryClassic             thrpt   15        363.242      ± 1.304  ops/s
HistogramBenchmark.openTelemetryExponential         thrpt   15        306.333      ± 4.615  ops/s
HistogramBenchmark.prometheusClassic                thrpt   15       3005.359    ± 483.753  ops/s
HistogramBenchmark.prometheusNative                 thrpt   15       2304.503    ± 188.442  ops/s
HistogramBenchmark.simpleclient                     thrpt   15       4253.261     ± 38.648  ops/s
TextFormatUtilBenchmark.openMetricsWriteToByteArray  thrpt   15     275235.821    ± 921.229  ops/s
TextFormatUtilBenchmark.openMetricsWriteToNull      thrpt   15     276091.772   ± 2196.720  ops/s
TextFormatUtilBenchmark.prometheusWriteToByteArray  thrpt   15     292125.443    ± 884.208  ops/s
TextFormatUtilBenchmark.prometheusWriteToNull       thrpt   15     292943.685   ± 1391.936  ops/s
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
