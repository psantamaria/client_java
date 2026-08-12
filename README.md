# Prometheus Java Client Benchmarks

## Run Information

- **Date:** 2026-08-12T05:17:17Z
- **Commit:** [`4b69f40`](https://github.com/psantamaria/client_java/commit/4b69f40bd4e616d69468ce99dc4323162287a577)
- **JDK:** 25.0.2 (OpenJDK 64-Bit Server VM)
- **Benchmark config:** 3 fork(s), 3 warmup, 5 measurement, 4 threads
- **Hardware:** Intel(R) Xeon(R) Platinum 8370C CPU @ 2.80GHz, 4 cores, 16 GB RAM
- **OS:** Linux 6.17.0-1022-azure

## Results

### CounterBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusInc | 31.12K | ± 646.30 | ops/s | **fastest** |
| codahaleIncNoLabels | 30.91K | ± 1.92K | ops/s | 1.0x slower |
| prometheusNoLabelsInc | 30.72K | ± 1.08K | ops/s | 1.0x slower |
| prometheusAdd | 27.02K | ± 2.38K | ops/s | 1.2x slower |
| simpleclientInc | 6.91K | ± 68.34 | ops/s | 4.5x slower |
| simpleclientNoLabelsInc | 6.87K | ± 211.36 | ops/s | 4.5x slower |
| simpleclientAdd | 6.36K | ± 135.42 | ops/s | 4.9x slower |
| openTelemetryIncNoLabels | 1.51K | ± 54.08 | ops/s | 21x slower |
| openTelemetryInc | 1.48K | ± 76.19 | ops/s | 21x slower |
| openTelemetryAdd | 1.35K | ± 110.13 | ops/s | 23x slower |

### HistogramBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| simpleclient | 4.47K | ± 54.36 | ops/s | **fastest** |
| prometheusClassic | 3.09K | ± 379.44 | ops/s | 1.4x slower |
| prometheusNative | 2.31K | ± 230.35 | ops/s | 1.9x slower |
| openTelemetryClassic | 521.71 | ± 5.56 | ops/s | 8.6x slower |
| openTelemetryExponential | 430.44 | ± 14.54 | ops/s | 10x slower |

### TextFormatUtilBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusWriteToNull | 318.82K | ± 1.72K | ops/s | **fastest** |
| prometheusWriteToByteArray | 314.23K | ± 1.32K | ops/s | 1.0x slower |
| openMetricsWriteToNull | 296.93K | ± 1.26K | ops/s | 1.1x slower |
| openMetricsWriteToByteArray | 294.74K | ± 2.44K | ops/s | 1.1x slower |

### Raw Results

```
Benchmark                                            Mode  Cnt          Score        Error  Units
CounterBenchmark.codahaleIncNoLabels                thrpt   15      30906.524   ± 1920.728  ops/s
CounterBenchmark.openTelemetryAdd                   thrpt   15       1351.551    ± 110.127  ops/s
CounterBenchmark.openTelemetryInc                   thrpt   15       1482.983     ± 76.192  ops/s
CounterBenchmark.openTelemetryIncNoLabels           thrpt   15       1513.912     ± 54.077  ops/s
CounterBenchmark.prometheusAdd                      thrpt   15      27017.297   ± 2376.737  ops/s
CounterBenchmark.prometheusInc                      thrpt   15      31119.219    ± 646.302  ops/s
CounterBenchmark.prometheusNoLabelsInc              thrpt   15      30719.882   ± 1079.554  ops/s
CounterBenchmark.simpleclientAdd                    thrpt   15       6363.656    ± 135.419  ops/s
CounterBenchmark.simpleclientInc                    thrpt   15       6912.412     ± 68.341  ops/s
CounterBenchmark.simpleclientNoLabelsInc            thrpt   15       6869.935    ± 211.356  ops/s
HistogramBenchmark.openTelemetryClassic             thrpt   15        521.709      ± 5.560  ops/s
HistogramBenchmark.openTelemetryExponential         thrpt   15        430.438     ± 14.543  ops/s
HistogramBenchmark.prometheusClassic                thrpt   15       3093.630    ± 379.442  ops/s
HistogramBenchmark.prometheusNative                 thrpt   15       2310.616    ± 230.346  ops/s
HistogramBenchmark.simpleclient                     thrpt   15       4473.133     ± 54.361  ops/s
TextFormatUtilBenchmark.openMetricsWriteToByteArray  thrpt   15     294739.934   ± 2441.341  ops/s
TextFormatUtilBenchmark.openMetricsWriteToNull      thrpt   15     296925.802   ± 1263.040  ops/s
TextFormatUtilBenchmark.prometheusWriteToByteArray  thrpt   15     314229.175   ± 1319.712  ops/s
TextFormatUtilBenchmark.prometheusWriteToNull       thrpt   15     318821.108   ± 1716.714  ops/s
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
