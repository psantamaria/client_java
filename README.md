# Prometheus Java Client Benchmarks

## Run Information

- **Date:** 2026-05-23T06:52:21Z
- **Commit:** [`4b69f40`](https://github.com/psantamaria/client_java/commit/4b69f40bd4e616d69468ce99dc4323162287a577)
- **JDK:** 25.0.2 (OpenJDK 64-Bit Server VM)
- **Benchmark config:** 3 fork(s), 3 warmup, 5 measurement, 4 threads
- **Hardware:** AMD EPYC 9V74 80-Core Processor, 4 cores, 16 GB RAM
- **OS:** Linux 6.17.0-1013-azure

## Results

### CounterBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusInc | 60.07K | ± 1.10K | ops/s | **fastest** |
| prometheusNoLabelsInc | 51.82K | ± 751.80 | ops/s | 1.2x slower |
| prometheusAdd | 47.68K | ± 764.00 | ops/s | 1.3x slower |
| codahaleIncNoLabels | 43.21K | ± 1.19K | ops/s | 1.4x slower |
| simpleclientInc | 6.30K | ± 83.60 | ops/s | 9.5x slower |
| simpleclientNoLabelsInc | 6.10K | ± 274.37 | ops/s | 9.9x slower |
| simpleclientAdd | 5.99K | ± 171.28 | ops/s | 10x slower |
| openTelemetryAdd | 1.39K | ± 114.70 | ops/s | 43x slower |
| openTelemetryInc | 1.30K | ± 25.77 | ops/s | 46x slower |
| openTelemetryIncNoLabels | 1.28K | ± 21.87 | ops/s | 47x slower |

### HistogramBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusClassic | 5.38K | ± 1.53K | ops/s | **fastest** |
| simpleclient | 4.32K | ± 79.78 | ops/s | 1.2x slower |
| prometheusNative | 2.97K | ± 274.84 | ops/s | 1.8x slower |
| openTelemetryClassic | 591.73 | ± 27.76 | ops/s | 9.1x slower |
| openTelemetryExponential | 512.35 | ± 38.90 | ops/s | 10x slower |

### TextFormatUtilBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusWriteToNull | 564.16K | ± 2.43K | ops/s | **fastest** |
| prometheusWriteToByteArray | 544.03K | ± 4.24K | ops/s | 1.0x slower |
| openMetricsWriteToNull | 532.75K | ± 5.57K | ops/s | 1.1x slower |
| openMetricsWriteToByteArray | 527.62K | ± 3.55K | ops/s | 1.1x slower |

### Raw Results

```
Benchmark                                            Mode  Cnt          Score        Error  Units
CounterBenchmark.codahaleIncNoLabels                thrpt   15      43209.647   ± 1191.091  ops/s
CounterBenchmark.openTelemetryAdd                   thrpt   15       1389.161    ± 114.695  ops/s
CounterBenchmark.openTelemetryInc                   thrpt   15       1298.224     ± 25.771  ops/s
CounterBenchmark.openTelemetryIncNoLabels           thrpt   15       1276.582     ± 21.866  ops/s
CounterBenchmark.prometheusAdd                      thrpt   15      47683.470    ± 764.000  ops/s
CounterBenchmark.prometheusInc                      thrpt   15      60072.315   ± 1104.411  ops/s
CounterBenchmark.prometheusNoLabelsInc              thrpt   15      51819.505    ± 751.805  ops/s
CounterBenchmark.simpleclientAdd                    thrpt   15       5990.649    ± 171.284  ops/s
CounterBenchmark.simpleclientInc                    thrpt   15       6303.813     ± 83.595  ops/s
CounterBenchmark.simpleclientNoLabelsInc            thrpt   15       6097.267    ± 274.375  ops/s
HistogramBenchmark.openTelemetryClassic             thrpt   15        591.729     ± 27.757  ops/s
HistogramBenchmark.openTelemetryExponential         thrpt   15        512.352     ± 38.900  ops/s
HistogramBenchmark.prometheusClassic                thrpt   15       5378.278   ± 1526.639  ops/s
HistogramBenchmark.prometheusNative                 thrpt   15       2965.938    ± 274.841  ops/s
HistogramBenchmark.simpleclient                     thrpt   15       4323.295     ± 79.782  ops/s
TextFormatUtilBenchmark.openMetricsWriteToByteArray  thrpt   15     527616.340   ± 3551.221  ops/s
TextFormatUtilBenchmark.openMetricsWriteToNull      thrpt   15     532746.926   ± 5567.410  ops/s
TextFormatUtilBenchmark.prometheusWriteToByteArray  thrpt   15     544031.021   ± 4244.281  ops/s
TextFormatUtilBenchmark.prometheusWriteToNull       thrpt   15     564155.555   ± 2433.819  ops/s
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
