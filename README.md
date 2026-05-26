# Prometheus Java Client Benchmarks

## Run Information

- **Date:** 2026-05-26T07:19:00Z
- **Commit:** [`4b69f40`](https://github.com/psantamaria/client_java/commit/4b69f40bd4e616d69468ce99dc4323162287a577)
- **JDK:** 25.0.2 (OpenJDK 64-Bit Server VM)
- **Benchmark config:** 3 fork(s), 3 warmup, 5 measurement, 4 threads
- **Hardware:** AMD EPYC 7763 64-Core Processor, 4 cores, 16 GB RAM
- **OS:** Linux 6.17.0-1013-azure

## Results

### CounterBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusInc | 64.90K | ± 1.15K | ops/s | **fastest** |
| prometheusNoLabelsInc | 56.74K | ± 378.01 | ops/s | 1.1x slower |
| prometheusAdd | 48.14K | ± 4.68K | ops/s | 1.3x slower |
| codahaleIncNoLabels | 47.37K | ± 414.34 | ops/s | 1.4x slower |
| simpleclientNoLabelsInc | 6.36K | ± 38.70 | ops/s | 10x slower |
| simpleclientInc | 6.33K | ± 40.25 | ops/s | 10x slower |
| simpleclientAdd | 6.10K | ± 274.99 | ops/s | 11x slower |
| openTelemetryAdd | 1.44K | ± 221.50 | ops/s | 45x slower |
| openTelemetryInc | 1.41K | ± 237.55 | ops/s | 46x slower |
| openTelemetryIncNoLabels | 1.27K | ± 58.95 | ops/s | 51x slower |

### HistogramBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusClassic | 5.55K | ± 1.10K | ops/s | **fastest** |
| simpleclient | 4.40K | ± 48.71 | ops/s | 1.3x slower |
| prometheusNative | 2.57K | ± 39.25 | ops/s | 2.2x slower |
| openTelemetryClassic | 710.63 | ± 5.40 | ops/s | 7.8x slower |
| openTelemetryExponential | 589.36 | ± 8.60 | ops/s | 9.4x slower |

### TextFormatUtilBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusWriteToNull | 485.69K | ± 3.44K | ops/s | **fastest** |
| prometheusWriteToByteArray | 485.04K | ± 2.93K | ops/s | 1.0x slower |
| openMetricsWriteToNull | 478.29K | ± 4.23K | ops/s | 1.0x slower |
| openMetricsWriteToByteArray | 478.09K | ± 5.70K | ops/s | 1.0x slower |

### Raw Results

```
Benchmark                                            Mode  Cnt          Score        Error  Units
CounterBenchmark.codahaleIncNoLabels                thrpt   15      47368.293    ± 414.345  ops/s
CounterBenchmark.openTelemetryAdd                   thrpt   15       1443.234    ± 221.501  ops/s
CounterBenchmark.openTelemetryInc                   thrpt   15       1408.066    ± 237.547  ops/s
CounterBenchmark.openTelemetryIncNoLabels           thrpt   15       1265.301     ± 58.954  ops/s
CounterBenchmark.prometheusAdd                      thrpt   15      48141.380   ± 4676.765  ops/s
CounterBenchmark.prometheusInc                      thrpt   15      64901.200   ± 1154.222  ops/s
CounterBenchmark.prometheusNoLabelsInc              thrpt   15      56741.485    ± 378.010  ops/s
CounterBenchmark.simpleclientAdd                    thrpt   15       6102.400    ± 274.989  ops/s
CounterBenchmark.simpleclientInc                    thrpt   15       6334.991     ± 40.247  ops/s
CounterBenchmark.simpleclientNoLabelsInc            thrpt   15       6355.571     ± 38.697  ops/s
HistogramBenchmark.openTelemetryClassic             thrpt   15        710.632      ± 5.400  ops/s
HistogramBenchmark.openTelemetryExponential         thrpt   15        589.355      ± 8.605  ops/s
HistogramBenchmark.prometheusClassic                thrpt   15       5551.292   ± 1100.119  ops/s
HistogramBenchmark.prometheusNative                 thrpt   15       2573.269     ± 39.254  ops/s
HistogramBenchmark.simpleclient                     thrpt   15       4396.778     ± 48.713  ops/s
TextFormatUtilBenchmark.openMetricsWriteToByteArray  thrpt   15     478093.293   ± 5695.595  ops/s
TextFormatUtilBenchmark.openMetricsWriteToNull      thrpt   15     478294.946   ± 4225.744  ops/s
TextFormatUtilBenchmark.prometheusWriteToByteArray  thrpt   15     485037.800   ± 2926.503  ops/s
TextFormatUtilBenchmark.prometheusWriteToNull       thrpt   15     485687.223   ± 3437.035  ops/s
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
