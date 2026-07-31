# Prometheus Java Client Benchmarks

## Run Information

- **Date:** 2026-07-31T06:47:59Z
- **Commit:** [`4b69f40`](https://github.com/psantamaria/client_java/commit/4b69f40bd4e616d69468ce99dc4323162287a577)
- **JDK:** 25.0.2 (OpenJDK 64-Bit Server VM)
- **Benchmark config:** 3 fork(s), 3 warmup, 5 measurement, 4 threads
- **Hardware:** Intel(R) Xeon(R) Platinum 8370C CPU @ 2.80GHz, 4 cores, 16 GB RAM
- **OS:** Linux 6.17.0-1020-azure

## Results

### CounterBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusInc | 30.74K | ± 1.26K | ops/s | **fastest** |
| prometheusNoLabelsInc | 30.41K | ± 890.00 | ops/s | 1.0x slower |
| codahaleIncNoLabels | 29.68K | ± 939.11 | ops/s | 1.0x slower |
| prometheusAdd | 27.81K | ± 873.50 | ops/s | 1.1x slower |
| simpleclientInc | 6.98K | ± 107.89 | ops/s | 4.4x slower |
| simpleclientNoLabelsInc | 6.50K | ± 77.49 | ops/s | 4.7x slower |
| simpleclientAdd | 6.41K | ± 451.26 | ops/s | 4.8x slower |
| openTelemetryAdd | 1.43K | ± 84.16 | ops/s | 21x slower |
| openTelemetryIncNoLabels | 1.41K | ± 144.44 | ops/s | 22x slower |
| openTelemetryInc | 1.38K | ± 138.12 | ops/s | 22x slower |

### HistogramBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| simpleclient | 4.42K | ± 77.67 | ops/s | **fastest** |
| prometheusClassic | 2.82K | ± 556.26 | ops/s | 1.6x slower |
| prometheusNative | 2.24K | ± 205.48 | ops/s | 2.0x slower |
| openTelemetryClassic | 518.50 | ± 34.73 | ops/s | 8.5x slower |
| openTelemetryExponential | 419.02 | ± 17.26 | ops/s | 11x slower |

### TextFormatUtilBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusWriteToByteArray | 308.54K | ± 2.47K | ops/s | **fastest** |
| prometheusWriteToNull | 307.84K | ± 2.66K | ops/s | 1.0x slower |
| openMetricsWriteToByteArray | 288.73K | ± 5.09K | ops/s | 1.1x slower |
| openMetricsWriteToNull | 287.14K | ± 6.07K | ops/s | 1.1x slower |

### Raw Results

```
Benchmark                                            Mode  Cnt          Score        Error  Units
CounterBenchmark.codahaleIncNoLabels                thrpt   15      29684.535    ± 939.115  ops/s
CounterBenchmark.openTelemetryAdd                   thrpt   15       1430.235     ± 84.157  ops/s
CounterBenchmark.openTelemetryInc                   thrpt   15       1379.817    ± 138.118  ops/s
CounterBenchmark.openTelemetryIncNoLabels           thrpt   15       1407.788    ± 144.444  ops/s
CounterBenchmark.prometheusAdd                      thrpt   15      27813.003    ± 873.496  ops/s
CounterBenchmark.prometheusInc                      thrpt   15      30743.356   ± 1262.681  ops/s
CounterBenchmark.prometheusNoLabelsInc              thrpt   15      30407.262    ± 889.997  ops/s
CounterBenchmark.simpleclientAdd                    thrpt   15       6405.868    ± 451.258  ops/s
CounterBenchmark.simpleclientInc                    thrpt   15       6982.431    ± 107.888  ops/s
CounterBenchmark.simpleclientNoLabelsInc            thrpt   15       6501.566     ± 77.486  ops/s
HistogramBenchmark.openTelemetryClassic             thrpt   15        518.499     ± 34.727  ops/s
HistogramBenchmark.openTelemetryExponential         thrpt   15        419.015     ± 17.259  ops/s
HistogramBenchmark.prometheusClassic                thrpt   15       2823.862    ± 556.260  ops/s
HistogramBenchmark.prometheusNative                 thrpt   15       2238.377    ± 205.478  ops/s
HistogramBenchmark.simpleclient                     thrpt   15       4415.419     ± 77.673  ops/s
TextFormatUtilBenchmark.openMetricsWriteToByteArray  thrpt   15     288728.239   ± 5086.681  ops/s
TextFormatUtilBenchmark.openMetricsWriteToNull      thrpt   15     287143.557   ± 6069.616  ops/s
TextFormatUtilBenchmark.prometheusWriteToByteArray  thrpt   15     308542.960   ± 2470.276  ops/s
TextFormatUtilBenchmark.prometheusWriteToNull       thrpt   15     307842.856   ± 2657.178  ops/s
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
