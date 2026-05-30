# Prometheus Java Client Benchmarks

## Run Information

- **Date:** 2026-05-30T07:00:44Z
- **Commit:** [`4b69f40`](https://github.com/psantamaria/client_java/commit/4b69f40bd4e616d69468ce99dc4323162287a577)
- **JDK:** 25.0.2 (OpenJDK 64-Bit Server VM)
- **Benchmark config:** 3 fork(s), 3 warmup, 5 measurement, 4 threads
- **Hardware:** AMD EPYC 7763 64-Core Processor, 4 cores, 16 GB RAM
- **OS:** Linux 6.17.0-1015-azure

## Results

### CounterBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusInc | 64.16K | ± 3.44K | ops/s | **fastest** |
| prometheusNoLabelsInc | 57.11K | ± 108.76 | ops/s | 1.1x slower |
| prometheusAdd | 50.78K | ± 590.66 | ops/s | 1.3x slower |
| codahaleIncNoLabels | 48.74K | ± 1.46K | ops/s | 1.3x slower |
| simpleclientInc | 6.71K | ± 10.64 | ops/s | 9.6x slower |
| simpleclientNoLabelsInc | 6.47K | ± 195.41 | ops/s | 9.9x slower |
| simpleclientAdd | 6.32K | ± 184.15 | ops/s | 10x slower |
| openTelemetryAdd | 1.27K | ± 61.54 | ops/s | 51x slower |
| openTelemetryInc | 1.26K | ± 27.23 | ops/s | 51x slower |
| openTelemetryIncNoLabels | 1.23K | ± 55.33 | ops/s | 52x slower |

### HistogramBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusClassic | 5.96K | ± 2.99K | ops/s | **fastest** |
| simpleclient | 4.40K | ± 17.84 | ops/s | 1.4x slower |
| prometheusNative | 2.90K | ± 233.11 | ops/s | 2.1x slower |
| openTelemetryClassic | 728.21 | ± 15.02 | ops/s | 8.2x slower |
| openTelemetryExponential | 568.69 | ± 23.71 | ops/s | 10x slower |

### TextFormatUtilBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusWriteToNull | 491.09K | ± 3.19K | ops/s | **fastest** |
| prometheusWriteToByteArray | 489.71K | ± 953.72 | ops/s | 1.0x slower |
| openMetricsWriteToNull | 486.66K | ± 2.36K | ops/s | 1.0x slower |
| openMetricsWriteToByteArray | 472.17K | ± 6.19K | ops/s | 1.0x slower |

### Raw Results

```
Benchmark                                            Mode  Cnt          Score        Error  Units
CounterBenchmark.codahaleIncNoLabels                thrpt   15      48740.339   ± 1458.282  ops/s
CounterBenchmark.openTelemetryAdd                   thrpt   15       1267.702     ± 61.545  ops/s
CounterBenchmark.openTelemetryInc                   thrpt   15       1257.528     ± 27.226  ops/s
CounterBenchmark.openTelemetryIncNoLabels           thrpt   15       1226.433     ± 55.325  ops/s
CounterBenchmark.prometheusAdd                      thrpt   15      50782.976    ± 590.657  ops/s
CounterBenchmark.prometheusInc                      thrpt   15      64160.930   ± 3435.498  ops/s
CounterBenchmark.prometheusNoLabelsInc              thrpt   15      57106.725    ± 108.757  ops/s
CounterBenchmark.simpleclientAdd                    thrpt   15       6324.093    ± 184.147  ops/s
CounterBenchmark.simpleclientInc                    thrpt   15       6709.452     ± 10.638  ops/s
CounterBenchmark.simpleclientNoLabelsInc            thrpt   15       6473.627    ± 195.411  ops/s
HistogramBenchmark.openTelemetryClassic             thrpt   15        728.206     ± 15.021  ops/s
HistogramBenchmark.openTelemetryExponential         thrpt   15        568.692     ± 23.711  ops/s
HistogramBenchmark.prometheusClassic                thrpt   15       5958.985   ± 2994.955  ops/s
HistogramBenchmark.prometheusNative                 thrpt   15       2895.992    ± 233.112  ops/s
HistogramBenchmark.simpleclient                     thrpt   15       4396.516     ± 17.836  ops/s
TextFormatUtilBenchmark.openMetricsWriteToByteArray  thrpt   15     472173.927   ± 6187.989  ops/s
TextFormatUtilBenchmark.openMetricsWriteToNull      thrpt   15     486660.035   ± 2361.715  ops/s
TextFormatUtilBenchmark.prometheusWriteToByteArray  thrpt   15     489714.878    ± 953.721  ops/s
TextFormatUtilBenchmark.prometheusWriteToNull       thrpt   15     491094.084   ± 3191.502  ops/s
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
