# Prometheus Java Client Benchmarks

## Run Information

- **Date:** 2026-07-23T06:36:33Z
- **Commit:** [`4b69f40`](https://github.com/psantamaria/client_java/commit/4b69f40bd4e616d69468ce99dc4323162287a577)
- **JDK:** 25.0.2 (OpenJDK 64-Bit Server VM)
- **Benchmark config:** 3 fork(s), 3 warmup, 5 measurement, 4 threads
- **Hardware:** AMD EPYC 7763 64-Core Processor, 4 cores, 16 GB RAM
- **OS:** Linux 6.17.0-1020-azure

## Results

### CounterBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusInc | 65.59K | ± 1.39K | ops/s | **fastest** |
| prometheusNoLabelsInc | 57.12K | ± 89.04 | ops/s | 1.1x slower |
| prometheusAdd | 51.38K | ± 255.89 | ops/s | 1.3x slower |
| codahaleIncNoLabels | 45.65K | ± 8.74K | ops/s | 1.4x slower |
| simpleclientAdd | 6.46K | ± 23.36 | ops/s | 10x slower |
| simpleclientInc | 6.43K | ± 144.03 | ops/s | 10x slower |
| simpleclientNoLabelsInc | 6.40K | ± 164.88 | ops/s | 10x slower |
| openTelemetryInc | 1.35K | ± 148.28 | ops/s | 49x slower |
| openTelemetryAdd | 1.30K | ± 102.32 | ops/s | 51x slower |
| openTelemetryIncNoLabels | 1.26K | ± 92.50 | ops/s | 52x slower |

### HistogramBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusClassic | 8.33K | ± 1.55K | ops/s | **fastest** |
| simpleclient | 4.41K | ± 27.15 | ops/s | 1.9x slower |
| prometheusNative | 3.00K | ± 258.52 | ops/s | 2.8x slower |
| openTelemetryClassic | 682.93 | ± 24.21 | ops/s | 12x slower |
| openTelemetryExponential | 556.32 | ± 34.49 | ops/s | 15x slower |

### TextFormatUtilBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusWriteToNull | 485.30K | ± 6.78K | ops/s | **fastest** |
| openMetricsWriteToNull | 480.68K | ± 4.79K | ops/s | 1.0x slower |
| prometheusWriteToByteArray | 477.51K | ± 4.32K | ops/s | 1.0x slower |
| openMetricsWriteToByteArray | 468.12K | ± 3.48K | ops/s | 1.0x slower |

### Raw Results

```
Benchmark                                            Mode  Cnt          Score        Error  Units
CounterBenchmark.codahaleIncNoLabels                thrpt   15      45652.004   ± 8741.554  ops/s
CounterBenchmark.openTelemetryAdd                   thrpt   15       1297.167    ± 102.319  ops/s
CounterBenchmark.openTelemetryInc                   thrpt   15       1346.695    ± 148.278  ops/s
CounterBenchmark.openTelemetryIncNoLabels           thrpt   15       1263.155     ± 92.495  ops/s
CounterBenchmark.prometheusAdd                      thrpt   15      51383.252    ± 255.885  ops/s
CounterBenchmark.prometheusInc                      thrpt   15      65589.600   ± 1393.247  ops/s
CounterBenchmark.prometheusNoLabelsInc              thrpt   15      57124.070     ± 89.036  ops/s
CounterBenchmark.simpleclientAdd                    thrpt   15       6459.076     ± 23.363  ops/s
CounterBenchmark.simpleclientInc                    thrpt   15       6426.976    ± 144.029  ops/s
CounterBenchmark.simpleclientNoLabelsInc            thrpt   15       6395.473    ± 164.885  ops/s
HistogramBenchmark.openTelemetryClassic             thrpt   15        682.931     ± 24.215  ops/s
HistogramBenchmark.openTelemetryExponential         thrpt   15        556.324     ± 34.493  ops/s
HistogramBenchmark.prometheusClassic                thrpt   15       8330.679   ± 1554.278  ops/s
HistogramBenchmark.prometheusNative                 thrpt   15       3000.749    ± 258.517  ops/s
HistogramBenchmark.simpleclient                     thrpt   15       4407.148     ± 27.149  ops/s
TextFormatUtilBenchmark.openMetricsWriteToByteArray  thrpt   15     468115.685   ± 3482.916  ops/s
TextFormatUtilBenchmark.openMetricsWriteToNull      thrpt   15     480682.183   ± 4793.249  ops/s
TextFormatUtilBenchmark.prometheusWriteToByteArray  thrpt   15     477513.623   ± 4317.702  ops/s
TextFormatUtilBenchmark.prometheusWriteToNull       thrpt   15     485301.259   ± 6780.092  ops/s
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
