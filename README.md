# Prometheus Java Client Benchmarks

## Run Information

- **Date:** 2026-04-24T06:08:20Z
- **Commit:** [`4b69f40`](https://github.com/psantamaria/client_java/commit/4b69f40bd4e616d69468ce99dc4323162287a577)
- **JDK:** 25.0.2 (OpenJDK 64-Bit Server VM)
- **Benchmark config:** 3 fork(s), 3 warmup, 5 measurement, 4 threads
- **Hardware:** AMD EPYC 7763 64-Core Processor, 4 cores, 16 GB RAM
- **OS:** Linux 6.17.0-1010-azure

## Results

### CounterBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusInc | 65.87K | ± 254.31 | ops/s | **fastest** |
| prometheusNoLabelsInc | 56.80K | ± 283.76 | ops/s | 1.2x slower |
| prometheusAdd | 51.15K | ± 437.15 | ops/s | 1.3x slower |
| codahaleIncNoLabels | 48.70K | ± 973.64 | ops/s | 1.4x slower |
| simpleclientNoLabelsInc | 6.56K | ± 120.89 | ops/s | 10x slower |
| simpleclientInc | 6.47K | ± 157.32 | ops/s | 10x slower |
| simpleclientAdd | 6.14K | ± 229.31 | ops/s | 11x slower |
| openTelemetryAdd | 1.42K | ± 96.88 | ops/s | 46x slower |
| openTelemetryInc | 1.40K | ± 168.49 | ops/s | 47x slower |
| openTelemetryIncNoLabels | 1.26K | ± 77.76 | ops/s | 52x slower |

### HistogramBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusClassic | 4.52K | ± 665.10 | ops/s | **fastest** |
| simpleclient | 4.42K | ± 86.30 | ops/s | 1.0x slower |
| prometheusNative | 3.05K | ± 189.94 | ops/s | 1.5x slower |
| openTelemetryClassic | 708.40 | ± 50.32 | ops/s | 6.4x slower |
| openTelemetryExponential | 536.75 | ± 17.92 | ops/s | 8.4x slower |

### TextFormatUtilBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusWriteToNull | 458.14K | ± 18.15K | ops/s | **fastest** |
| openMetricsWriteToNull | 453.09K | ± 9.51K | ops/s | 1.0x slower |
| openMetricsWriteToByteArray | 453.08K | ± 6.48K | ops/s | 1.0x slower |
| prometheusWriteToByteArray | 446.63K | ± 6.43K | ops/s | 1.0x slower |

### Raw Results

```
Benchmark                                            Mode  Cnt          Score        Error  Units
CounterBenchmark.codahaleIncNoLabels                thrpt   15      48704.827    ± 973.642  ops/s
CounterBenchmark.openTelemetryAdd                   thrpt   15       1419.263     ± 96.881  ops/s
CounterBenchmark.openTelemetryInc                   thrpt   15       1400.189    ± 168.485  ops/s
CounterBenchmark.openTelemetryIncNoLabels           thrpt   15       1261.418     ± 77.758  ops/s
CounterBenchmark.prometheusAdd                      thrpt   15      51148.500    ± 437.153  ops/s
CounterBenchmark.prometheusInc                      thrpt   15      65874.587    ± 254.313  ops/s
CounterBenchmark.prometheusNoLabelsInc              thrpt   15      56804.027    ± 283.760  ops/s
CounterBenchmark.simpleclientAdd                    thrpt   15       6142.166    ± 229.307  ops/s
CounterBenchmark.simpleclientInc                    thrpt   15       6472.159    ± 157.321  ops/s
CounterBenchmark.simpleclientNoLabelsInc            thrpt   15       6558.295    ± 120.890  ops/s
HistogramBenchmark.openTelemetryClassic             thrpt   15        708.395     ± 50.325  ops/s
HistogramBenchmark.openTelemetryExponential         thrpt   15        536.751     ± 17.922  ops/s
HistogramBenchmark.prometheusClassic                thrpt   15       4516.738    ± 665.104  ops/s
HistogramBenchmark.prometheusNative                 thrpt   15       3053.173    ± 189.939  ops/s
HistogramBenchmark.simpleclient                     thrpt   15       4419.087     ± 86.302  ops/s
TextFormatUtilBenchmark.openMetricsWriteToByteArray  thrpt   15     453075.725   ± 6476.769  ops/s
TextFormatUtilBenchmark.openMetricsWriteToNull      thrpt   15     453088.073   ± 9506.391  ops/s
TextFormatUtilBenchmark.prometheusWriteToByteArray  thrpt   15     446627.976   ± 6430.960  ops/s
TextFormatUtilBenchmark.prometheusWriteToNull       thrpt   15     458144.690  ± 18151.613  ops/s
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
