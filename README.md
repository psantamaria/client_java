# Prometheus Java Client Benchmarks

## Run Information

- **Date:** 2026-06-21T08:03:32Z
- **Commit:** [`4b69f40`](https://github.com/psantamaria/client_java/commit/4b69f40bd4e616d69468ce99dc4323162287a577)
- **JDK:** 25.0.2 (OpenJDK 64-Bit Server VM)
- **Benchmark config:** 3 fork(s), 3 warmup, 5 measurement, 4 threads
- **Hardware:** AMD EPYC 7763 64-Core Processor, 4 cores, 16 GB RAM
- **OS:** Linux 6.17.0-1018-azure

## Results

### CounterBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusInc | 65.74K | ± 130.66 | ops/s | **fastest** |
| prometheusNoLabelsInc | 57.21K | ± 148.41 | ops/s | 1.1x slower |
| prometheusAdd | 51.08K | ± 802.86 | ops/s | 1.3x slower |
| codahaleIncNoLabels | 44.34K | ± 8.02K | ops/s | 1.5x slower |
| simpleclientNoLabelsInc | 6.61K | ± 10.85 | ops/s | 9.9x slower |
| simpleclientInc | 6.58K | ± 186.98 | ops/s | 10.0x slower |
| simpleclientAdd | 6.27K | ± 210.66 | ops/s | 10x slower |
| openTelemetryAdd | 1.37K | ± 225.19 | ops/s | 48x slower |
| openTelemetryInc | 1.25K | ± 13.40 | ops/s | 53x slower |
| openTelemetryIncNoLabels | 1.19K | ± 49.03 | ops/s | 55x slower |

### HistogramBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusClassic | 4.68K | ± 906.13 | ops/s | **fastest** |
| simpleclient | 4.51K | ± 11.24 | ops/s | 1.0x slower |
| prometheusNative | 3.00K | ± 308.86 | ops/s | 1.6x slower |
| openTelemetryClassic | 683.79 | ± 50.37 | ops/s | 6.8x slower |
| openTelemetryExponential | 561.65 | ± 45.47 | ops/s | 8.3x slower |

### TextFormatUtilBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusWriteToNull | 477.81K | ± 4.54K | ops/s | **fastest** |
| prometheusWriteToByteArray | 469.39K | ± 10.17K | ops/s | 1.0x slower |
| openMetricsWriteToNull | 467.13K | ± 4.56K | ops/s | 1.0x slower |
| openMetricsWriteToByteArray | 460.28K | ± 7.12K | ops/s | 1.0x slower |

### Raw Results

```
Benchmark                                            Mode  Cnt          Score        Error  Units
CounterBenchmark.codahaleIncNoLabels                thrpt   15      44337.364   ± 8023.814  ops/s
CounterBenchmark.openTelemetryAdd                   thrpt   15       1369.625    ± 225.186  ops/s
CounterBenchmark.openTelemetryInc                   thrpt   15       1248.346     ± 13.396  ops/s
CounterBenchmark.openTelemetryIncNoLabels           thrpt   15       1193.409     ± 49.035  ops/s
CounterBenchmark.prometheusAdd                      thrpt   15      51075.543    ± 802.856  ops/s
CounterBenchmark.prometheusInc                      thrpt   15      65738.157    ± 130.662  ops/s
CounterBenchmark.prometheusNoLabelsInc              thrpt   15      57210.040    ± 148.408  ops/s
CounterBenchmark.simpleclientAdd                    thrpt   15       6266.323    ± 210.663  ops/s
CounterBenchmark.simpleclientInc                    thrpt   15       6582.932    ± 186.980  ops/s
CounterBenchmark.simpleclientNoLabelsInc            thrpt   15       6607.928     ± 10.851  ops/s
HistogramBenchmark.openTelemetryClassic             thrpt   15        683.788     ± 50.372  ops/s
HistogramBenchmark.openTelemetryExponential         thrpt   15        561.648     ± 45.466  ops/s
HistogramBenchmark.prometheusClassic                thrpt   15       4677.029    ± 906.126  ops/s
HistogramBenchmark.prometheusNative                 thrpt   15       3002.267    ± 308.857  ops/s
HistogramBenchmark.simpleclient                     thrpt   15       4508.147     ± 11.244  ops/s
TextFormatUtilBenchmark.openMetricsWriteToByteArray  thrpt   15     460281.989   ± 7124.081  ops/s
TextFormatUtilBenchmark.openMetricsWriteToNull      thrpt   15     467130.267   ± 4560.928  ops/s
TextFormatUtilBenchmark.prometheusWriteToByteArray  thrpt   15     469386.620  ± 10173.673  ops/s
TextFormatUtilBenchmark.prometheusWriteToNull       thrpt   15     477814.810   ± 4543.992  ops/s
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
