# Prometheus Java Client Benchmarks

## Run Information

- **Date:** 2026-06-12T07:46:15Z
- **Commit:** [`4b69f40`](https://github.com/psantamaria/client_java/commit/4b69f40bd4e616d69468ce99dc4323162287a577)
- **JDK:** 25.0.2 (OpenJDK 64-Bit Server VM)
- **Benchmark config:** 3 fork(s), 3 warmup, 5 measurement, 4 threads
- **Hardware:** Intel(R) Xeon(R) Platinum 8370C CPU @ 2.80GHz, 4 cores, 16 GB RAM
- **OS:** Linux 6.17.0-1018-azure

## Results

### CounterBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusInc | 31.51K | ± 30.04 | ops/s | **fastest** |
| prometheusNoLabelsInc | 30.56K | ± 578.64 | ops/s | 1.0x slower |
| codahaleIncNoLabels | 28.90K | ± 539.98 | ops/s | 1.1x slower |
| prometheusAdd | 28.48K | ± 208.81 | ops/s | 1.1x slower |
| simpleclientInc | 6.74K | ± 79.48 | ops/s | 4.7x slower |
| simpleclientNoLabelsInc | 6.66K | ± 215.25 | ops/s | 4.7x slower |
| simpleclientAdd | 6.50K | ± 105.97 | ops/s | 4.8x slower |
| openTelemetryIncNoLabels | 1.31K | ± 111.29 | ops/s | 24x slower |
| openTelemetryAdd | 1.30K | ± 57.33 | ops/s | 24x slower |
| openTelemetryInc | 1.30K | ± 50.54 | ops/s | 24x slower |

### HistogramBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| simpleclient | 4.51K | ± 61.45 | ops/s | **fastest** |
| prometheusClassic | 2.95K | ± 296.58 | ops/s | 1.5x slower |
| prometheusNative | 2.18K | ± 131.84 | ops/s | 2.1x slower |
| openTelemetryClassic | 519.57 | ± 26.73 | ops/s | 8.7x slower |
| openTelemetryExponential | 390.34 | ± 10.40 | ops/s | 12x slower |

### TextFormatUtilBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusWriteToNull | 309.56K | ± 4.11K | ops/s | **fastest** |
| prometheusWriteToByteArray | 304.36K | ± 2.98K | ops/s | 1.0x slower |
| openMetricsWriteToByteArray | 290.61K | ± 1.88K | ops/s | 1.1x slower |
| openMetricsWriteToNull | 289.14K | ± 2.83K | ops/s | 1.1x slower |

### Raw Results

```
Benchmark                                            Mode  Cnt          Score        Error  Units
CounterBenchmark.codahaleIncNoLabels                thrpt   15      28895.268    ± 539.982  ops/s
CounterBenchmark.openTelemetryAdd                   thrpt   15       1296.793     ± 57.330  ops/s
CounterBenchmark.openTelemetryInc                   thrpt   15       1295.299     ± 50.542  ops/s
CounterBenchmark.openTelemetryIncNoLabels           thrpt   15       1312.224    ± 111.293  ops/s
CounterBenchmark.prometheusAdd                      thrpt   15      28481.872    ± 208.809  ops/s
CounterBenchmark.prometheusInc                      thrpt   15      31512.527     ± 30.045  ops/s
CounterBenchmark.prometheusNoLabelsInc              thrpt   15      30556.028    ± 578.637  ops/s
CounterBenchmark.simpleclientAdd                    thrpt   15       6504.906    ± 105.972  ops/s
CounterBenchmark.simpleclientInc                    thrpt   15       6743.433     ± 79.483  ops/s
CounterBenchmark.simpleclientNoLabelsInc            thrpt   15       6663.812    ± 215.251  ops/s
HistogramBenchmark.openTelemetryClassic             thrpt   15        519.566     ± 26.734  ops/s
HistogramBenchmark.openTelemetryExponential         thrpt   15        390.338     ± 10.399  ops/s
HistogramBenchmark.prometheusClassic                thrpt   15       2948.941    ± 296.580  ops/s
HistogramBenchmark.prometheusNative                 thrpt   15       2181.985    ± 131.842  ops/s
HistogramBenchmark.simpleclient                     thrpt   15       4505.469     ± 61.451  ops/s
TextFormatUtilBenchmark.openMetricsWriteToByteArray  thrpt   15     290607.810   ± 1875.925  ops/s
TextFormatUtilBenchmark.openMetricsWriteToNull      thrpt   15     289141.156   ± 2830.426  ops/s
TextFormatUtilBenchmark.prometheusWriteToByteArray  thrpt   15     304357.019   ± 2977.677  ops/s
TextFormatUtilBenchmark.prometheusWriteToNull       thrpt   15     309558.488   ± 4114.474  ops/s
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
