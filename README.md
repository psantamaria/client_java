# Prometheus Java Client Benchmarks

## Run Information

- **Date:** 2026-06-10T07:35:24Z
- **Commit:** [`4b69f40`](https://github.com/psantamaria/client_java/commit/4b69f40bd4e616d69468ce99dc4323162287a577)
- **JDK:** 25.0.2 (OpenJDK 64-Bit Server VM)
- **Benchmark config:** 3 fork(s), 3 warmup, 5 measurement, 4 threads
- **Hardware:** AMD EPYC 7763 64-Core Processor, 4 cores, 16 GB RAM
- **OS:** Linux 6.17.0-1015-azure

## Results

### CounterBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusInc | 65.20K | ± 1.41K | ops/s | **fastest** |
| prometheusNoLabelsInc | 56.79K | ± 380.72 | ops/s | 1.1x slower |
| prometheusAdd | 51.00K | ± 309.96 | ops/s | 1.3x slower |
| codahaleIncNoLabels | 41.38K | ± 13.84K | ops/s | 1.6x slower |
| simpleclientInc | 6.64K | ± 46.92 | ops/s | 9.8x slower |
| simpleclientNoLabelsInc | 6.51K | ± 131.58 | ops/s | 10x slower |
| simpleclientAdd | 6.27K | ± 178.75 | ops/s | 10x slower |
| openTelemetryInc | 1.26K | ± 22.11 | ops/s | 52x slower |
| openTelemetryAdd | 1.23K | ± 7.14 | ops/s | 53x slower |
| openTelemetryIncNoLabels | 1.21K | ± 30.18 | ops/s | 54x slower |

### HistogramBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusClassic | 5.16K | ± 338.50 | ops/s | **fastest** |
| simpleclient | 4.46K | ± 38.52 | ops/s | 1.2x slower |
| prometheusNative | 3.12K | ± 110.33 | ops/s | 1.7x slower |
| openTelemetryClassic | 683.17 | ± 60.49 | ops/s | 7.6x slower |
| openTelemetryExponential | 570.51 | ± 12.35 | ops/s | 9.0x slower |

### TextFormatUtilBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusWriteToNull | 487.61K | ± 6.69K | ops/s | **fastest** |
| openMetricsWriteToNull | 483.43K | ± 2.91K | ops/s | 1.0x slower |
| prometheusWriteToByteArray | 480.64K | ± 7.38K | ops/s | 1.0x slower |
| openMetricsWriteToByteArray | 473.69K | ± 3.78K | ops/s | 1.0x slower |

### Raw Results

```
Benchmark                                            Mode  Cnt          Score        Error  Units
CounterBenchmark.codahaleIncNoLabels                thrpt   15      41381.561  ± 13836.733  ops/s
CounterBenchmark.openTelemetryAdd                   thrpt   15       1225.571      ± 7.143  ops/s
CounterBenchmark.openTelemetryInc                   thrpt   15       1255.840     ± 22.106  ops/s
CounterBenchmark.openTelemetryIncNoLabels           thrpt   15       1208.095     ± 30.177  ops/s
CounterBenchmark.prometheusAdd                      thrpt   15      50996.759    ± 309.959  ops/s
CounterBenchmark.prometheusInc                      thrpt   15      65200.819   ± 1408.503  ops/s
CounterBenchmark.prometheusNoLabelsInc              thrpt   15      56787.251    ± 380.716  ops/s
CounterBenchmark.simpleclientAdd                    thrpt   15       6267.068    ± 178.753  ops/s
CounterBenchmark.simpleclientInc                    thrpt   15       6641.469     ± 46.920  ops/s
CounterBenchmark.simpleclientNoLabelsInc            thrpt   15       6510.542    ± 131.580  ops/s
HistogramBenchmark.openTelemetryClassic             thrpt   15        683.169     ± 60.494  ops/s
HistogramBenchmark.openTelemetryExponential         thrpt   15        570.509     ± 12.346  ops/s
HistogramBenchmark.prometheusClassic                thrpt   15       5160.618    ± 338.501  ops/s
HistogramBenchmark.prometheusNative                 thrpt   15       3117.544    ± 110.328  ops/s
HistogramBenchmark.simpleclient                     thrpt   15       4461.456     ± 38.522  ops/s
TextFormatUtilBenchmark.openMetricsWriteToByteArray  thrpt   15     473689.893   ± 3780.276  ops/s
TextFormatUtilBenchmark.openMetricsWriteToNull      thrpt   15     483431.788   ± 2910.792  ops/s
TextFormatUtilBenchmark.prometheusWriteToByteArray  thrpt   15     480643.007   ± 7383.568  ops/s
TextFormatUtilBenchmark.prometheusWriteToNull       thrpt   15     487612.722   ± 6688.721  ops/s
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
