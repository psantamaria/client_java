# Prometheus Java Client Benchmarks

## Run Information

- **Date:** 2026-06-02T07:54:30Z
- **Commit:** [`4b69f40`](https://github.com/psantamaria/client_java/commit/4b69f40bd4e616d69468ce99dc4323162287a577)
- **JDK:** 25.0.2 (OpenJDK 64-Bit Server VM)
- **Benchmark config:** 3 fork(s), 3 warmup, 5 measurement, 4 threads
- **Hardware:** AMD EPYC 7763 64-Core Processor, 4 cores, 16 GB RAM
- **OS:** Linux 6.17.0-1015-azure

## Results

### CounterBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusInc | 66.01K | ± 310.99 | ops/s | **fastest** |
| prometheusNoLabelsInc | 56.36K | ± 1.40K | ops/s | 1.2x slower |
| prometheusAdd | 51.25K | ± 456.55 | ops/s | 1.3x slower |
| codahaleIncNoLabels | 47.38K | ± 604.65 | ops/s | 1.4x slower |
| simpleclientInc | 6.57K | ± 204.75 | ops/s | 10x slower |
| simpleclientNoLabelsInc | 6.50K | ± 132.47 | ops/s | 10x slower |
| simpleclientAdd | 6.06K | ± 38.71 | ops/s | 11x slower |
| openTelemetryAdd | 1.37K | ± 243.24 | ops/s | 48x slower |
| openTelemetryIncNoLabels | 1.30K | ± 224.22 | ops/s | 51x slower |
| openTelemetryInc | 1.28K | ± 45.01 | ops/s | 52x slower |

### HistogramBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| simpleclient | 4.41K | ± 69.52 | ops/s | **fastest** |
| prometheusClassic | 4.03K | ± 230.02 | ops/s | 1.1x slower |
| prometheusNative | 2.99K | ± 252.92 | ops/s | 1.5x slower |
| openTelemetryClassic | 660.82 | ± 33.36 | ops/s | 6.7x slower |
| openTelemetryExponential | 575.91 | ± 29.39 | ops/s | 7.7x slower |

### TextFormatUtilBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusWriteToNull | 482.50K | ± 4.49K | ops/s | **fastest** |
| prometheusWriteToByteArray | 480.63K | ± 2.73K | ops/s | 1.0x slower |
| openMetricsWriteToNull | 475.02K | ± 4.36K | ops/s | 1.0x slower |
| openMetricsWriteToByteArray | 466.63K | ± 3.50K | ops/s | 1.0x slower |

### Raw Results

```
Benchmark                                            Mode  Cnt          Score        Error  Units
CounterBenchmark.codahaleIncNoLabels                thrpt   15      47383.040    ± 604.645  ops/s
CounterBenchmark.openTelemetryAdd                   thrpt   15       1374.728    ± 243.241  ops/s
CounterBenchmark.openTelemetryInc                   thrpt   15       1278.351     ± 45.013  ops/s
CounterBenchmark.openTelemetryIncNoLabels           thrpt   15       1299.420    ± 224.219  ops/s
CounterBenchmark.prometheusAdd                      thrpt   15      51253.137    ± 456.549  ops/s
CounterBenchmark.prometheusInc                      thrpt   15      66010.112    ± 310.986  ops/s
CounterBenchmark.prometheusNoLabelsInc              thrpt   15      56357.170   ± 1400.573  ops/s
CounterBenchmark.simpleclientAdd                    thrpt   15       6063.630     ± 38.713  ops/s
CounterBenchmark.simpleclientInc                    thrpt   15       6570.885    ± 204.749  ops/s
CounterBenchmark.simpleclientNoLabelsInc            thrpt   15       6502.368    ± 132.467  ops/s
HistogramBenchmark.openTelemetryClassic             thrpt   15        660.822     ± 33.357  ops/s
HistogramBenchmark.openTelemetryExponential         thrpt   15        575.912     ± 29.388  ops/s
HistogramBenchmark.prometheusClassic                thrpt   15       4029.312    ± 230.018  ops/s
HistogramBenchmark.prometheusNative                 thrpt   15       2987.995    ± 252.920  ops/s
HistogramBenchmark.simpleclient                     thrpt   15       4409.441     ± 69.520  ops/s
TextFormatUtilBenchmark.openMetricsWriteToByteArray  thrpt   15     466626.159   ± 3496.331  ops/s
TextFormatUtilBenchmark.openMetricsWriteToNull      thrpt   15     475019.138   ± 4357.363  ops/s
TextFormatUtilBenchmark.prometheusWriteToByteArray  thrpt   15     480631.158   ± 2728.557  ops/s
TextFormatUtilBenchmark.prometheusWriteToNull       thrpt   15     482496.981   ± 4485.239  ops/s
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
