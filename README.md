# Prometheus Java Client Benchmarks

## Run Information

- **Date:** 2026-09-10T08:11:35Z
- **Commit:** [`4b69f40`](https://github.com/psantamaria/client_java/commit/4b69f40bd4e616d69468ce99dc4323162287a577)
- **JDK:** 25.0.2 (OpenJDK 64-Bit Server VM)
- **Benchmark config:** 3 fork(s), 3 warmup, 5 measurement, 4 threads
- **Hardware:** Intel(R) Xeon(R) Platinum 8370C CPU @ 2.80GHz, 4 cores, 16 GB RAM
- **OS:** Linux 6.17.0-1022-azure

## Results

### CounterBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusInc | 31.51K | ± 13.86 | ops/s | **fastest** |
| prometheusNoLabelsInc | 30.58K | ± 1.13K | ops/s | 1.0x slower |
| codahaleIncNoLabels | 28.99K | ± 1.11K | ops/s | 1.1x slower |
| prometheusAdd | 28.40K | ± 84.47 | ops/s | 1.1x slower |
| simpleclientInc | 6.84K | ± 90.82 | ops/s | 4.6x slower |
| simpleclientNoLabelsInc | 6.66K | ± 148.56 | ops/s | 4.7x slower |
| simpleclientAdd | 6.36K | ± 200.83 | ops/s | 5.0x slower |
| openTelemetryIncNoLabels | 1.41K | ± 73.54 | ops/s | 22x slower |
| openTelemetryInc | 1.36K | ± 56.39 | ops/s | 23x slower |
| openTelemetryAdd | 1.30K | ± 81.50 | ops/s | 24x slower |

### HistogramBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| simpleclient | 4.48K | ± 36.58 | ops/s | **fastest** |
| prometheusClassic | 2.77K | ± 443.51 | ops/s | 1.6x slower |
| prometheusNative | 2.22K | ± 238.21 | ops/s | 2.0x slower |
| openTelemetryClassic | 497.92 | ± 6.94 | ops/s | 9.0x slower |
| openTelemetryExponential | 411.37 | ± 7.71 | ops/s | 11x slower |

### TextFormatUtilBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusWriteToNull | 314.80K | ± 1.63K | ops/s | **fastest** |
| prometheusWriteToByteArray | 312.85K | ± 1.44K | ops/s | 1.0x slower |
| openMetricsWriteToNull | 295.13K | ± 1.87K | ops/s | 1.1x slower |
| openMetricsWriteToByteArray | 294.16K | ± 1.08K | ops/s | 1.1x slower |

### Raw Results

```
Benchmark                                            Mode  Cnt          Score        Error  Units
CounterBenchmark.codahaleIncNoLabels                thrpt   15      28991.218   ± 1112.403  ops/s
CounterBenchmark.openTelemetryAdd                   thrpt   15       1297.861     ± 81.495  ops/s
CounterBenchmark.openTelemetryInc                   thrpt   15       1363.922     ± 56.393  ops/s
CounterBenchmark.openTelemetryIncNoLabels           thrpt   15       1406.347     ± 73.537  ops/s
CounterBenchmark.prometheusAdd                      thrpt   15      28396.414     ± 84.470  ops/s
CounterBenchmark.prometheusInc                      thrpt   15      31509.480     ± 13.864  ops/s
CounterBenchmark.prometheusNoLabelsInc              thrpt   15      30579.877   ± 1130.395  ops/s
CounterBenchmark.simpleclientAdd                    thrpt   15       6357.634    ± 200.827  ops/s
CounterBenchmark.simpleclientInc                    thrpt   15       6843.940     ± 90.822  ops/s
CounterBenchmark.simpleclientNoLabelsInc            thrpt   15       6655.510    ± 148.560  ops/s
HistogramBenchmark.openTelemetryClassic             thrpt   15        497.915      ± 6.945  ops/s
HistogramBenchmark.openTelemetryExponential         thrpt   15        411.375      ± 7.715  ops/s
HistogramBenchmark.prometheusClassic                thrpt   15       2766.533    ± 443.508  ops/s
HistogramBenchmark.prometheusNative                 thrpt   15       2221.656    ± 238.212  ops/s
HistogramBenchmark.simpleclient                     thrpt   15       4475.355     ± 36.580  ops/s
TextFormatUtilBenchmark.openMetricsWriteToByteArray  thrpt   15     294155.027   ± 1083.730  ops/s
TextFormatUtilBenchmark.openMetricsWriteToNull      thrpt   15     295126.860   ± 1872.010  ops/s
TextFormatUtilBenchmark.prometheusWriteToByteArray  thrpt   15     312846.823   ± 1442.733  ops/s
TextFormatUtilBenchmark.prometheusWriteToNull       thrpt   15     314800.214   ± 1626.445  ops/s
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
