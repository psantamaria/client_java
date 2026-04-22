# Prometheus Java Client Benchmarks

## Run Information

- **Date:** 2026-04-22T05:59:55Z
- **Commit:** [`4b69f40`](https://github.com/psantamaria/client_java/commit/4b69f40bd4e616d69468ce99dc4323162287a577)
- **JDK:** 25.0.2 (OpenJDK 64-Bit Server VM)
- **Benchmark config:** 3 fork(s), 3 warmup, 5 measurement, 4 threads
- **Hardware:** AMD EPYC 9V74 80-Core Processor, 4 cores, 16 GB RAM
- **OS:** Linux 6.17.0-1010-azure

## Results

### CounterBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusInc | 59.61K | ± 508.56 | ops/s | **fastest** |
| prometheusNoLabelsInc | 49.93K | ± 2.38K | ops/s | 1.2x slower |
| prometheusAdd | 48.35K | ± 274.29 | ops/s | 1.2x slower |
| codahaleIncNoLabels | 42.30K | ± 1.45K | ops/s | 1.4x slower |
| simpleclientInc | 6.16K | ± 150.52 | ops/s | 9.7x slower |
| simpleclientAdd | 6.03K | ± 158.69 | ops/s | 9.9x slower |
| simpleclientNoLabelsInc | 6.01K | ± 138.77 | ops/s | 9.9x slower |
| openTelemetryAdd | 1.38K | ± 109.57 | ops/s | 43x slower |
| openTelemetryIncNoLabels | 1.27K | ± 76.28 | ops/s | 47x slower |
| openTelemetryInc | 1.25K | ± 27.71 | ops/s | 48x slower |

### HistogramBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusClassic | 5.14K | ± 1.75K | ops/s | **fastest** |
| simpleclient | 4.52K | ± 51.48 | ops/s | 1.1x slower |
| prometheusNative | 2.80K | ± 250.56 | ops/s | 1.8x slower |
| openTelemetryClassic | 595.19 | ± 21.22 | ops/s | 8.6x slower |
| openTelemetryExponential | 524.32 | ± 11.02 | ops/s | 9.8x slower |

### TextFormatUtilBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusWriteToNull | 556.11K | ± 4.50K | ops/s | **fastest** |
| prometheusWriteToByteArray | 545.61K | ± 3.06K | ops/s | 1.0x slower |
| openMetricsWriteToNull | 536.79K | ± 4.50K | ops/s | 1.0x slower |
| openMetricsWriteToByteArray | 528.64K | ± 3.06K | ops/s | 1.1x slower |

### Raw Results

```
Benchmark                                            Mode  Cnt          Score        Error  Units
CounterBenchmark.codahaleIncNoLabels                thrpt   15      42301.530   ± 1453.488  ops/s
CounterBenchmark.openTelemetryAdd                   thrpt   15       1381.835    ± 109.574  ops/s
CounterBenchmark.openTelemetryInc                   thrpt   15       1248.304     ± 27.705  ops/s
CounterBenchmark.openTelemetryIncNoLabels           thrpt   15       1269.002     ± 76.281  ops/s
CounterBenchmark.prometheusAdd                      thrpt   15      48354.945    ± 274.290  ops/s
CounterBenchmark.prometheusInc                      thrpt   15      59613.434    ± 508.562  ops/s
CounterBenchmark.prometheusNoLabelsInc              thrpt   15      49927.918   ± 2375.638  ops/s
CounterBenchmark.simpleclientAdd                    thrpt   15       6033.366    ± 158.690  ops/s
CounterBenchmark.simpleclientInc                    thrpt   15       6155.586    ± 150.518  ops/s
CounterBenchmark.simpleclientNoLabelsInc            thrpt   15       6011.843    ± 138.775  ops/s
HistogramBenchmark.openTelemetryClassic             thrpt   15        595.192     ± 21.219  ops/s
HistogramBenchmark.openTelemetryExponential         thrpt   15        524.321     ± 11.021  ops/s
HistogramBenchmark.prometheusClassic                thrpt   15       5142.759   ± 1748.992  ops/s
HistogramBenchmark.prometheusNative                 thrpt   15       2801.803    ± 250.564  ops/s
HistogramBenchmark.simpleclient                     thrpt   15       4517.743     ± 51.483  ops/s
TextFormatUtilBenchmark.openMetricsWriteToByteArray  thrpt   15     528635.643   ± 3056.164  ops/s
TextFormatUtilBenchmark.openMetricsWriteToNull      thrpt   15     536792.027   ± 4495.705  ops/s
TextFormatUtilBenchmark.prometheusWriteToByteArray  thrpt   15     545613.432   ± 3055.657  ops/s
TextFormatUtilBenchmark.prometheusWriteToNull       thrpt   15     556105.642   ± 4495.124  ops/s
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
