# Prometheus Java Client Benchmarks

## Run Information

- **Date:** 2026-09-21T08:47:57Z
- **Commit:** [`4b69f40`](https://github.com/psantamaria/client_java/commit/4b69f40bd4e616d69468ce99dc4323162287a577)
- **JDK:** 25.0.2 (OpenJDK 64-Bit Server VM)
- **Benchmark config:** 3 fork(s), 3 warmup, 5 measurement, 4 threads
- **Hardware:** AMD EPYC 7763 64-Core Processor, 4 cores, 16 GB RAM
- **OS:** Linux 6.17.0-1022-azure

## Results

### CounterBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusInc | 65.53K | ± 830.18 | ops/s | **fastest** |
| prometheusNoLabelsInc | 56.65K | ± 389.68 | ops/s | 1.2x slower |
| prometheusAdd | 51.45K | ± 207.18 | ops/s | 1.3x slower |
| codahaleIncNoLabels | 49.74K | ± 1.84K | ops/s | 1.3x slower |
| simpleclientInc | 6.61K | ± 95.51 | ops/s | 9.9x slower |
| simpleclientNoLabelsInc | 6.47K | ± 186.39 | ops/s | 10x slower |
| simpleclientAdd | 6.11K | ± 231.29 | ops/s | 11x slower |
| openTelemetryAdd | 1.56K | ± 338.57 | ops/s | 42x slower |
| openTelemetryIncNoLabels | 1.25K | ± 100.97 | ops/s | 52x slower |
| openTelemetryInc | 1.19K | ± 34.34 | ops/s | 55x slower |

### HistogramBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusClassic | 5.21K | ± 414.10 | ops/s | **fastest** |
| simpleclient | 4.38K | ± 51.25 | ops/s | 1.2x slower |
| prometheusNative | 2.97K | ± 321.95 | ops/s | 1.8x slower |
| openTelemetryClassic | 645.52 | ± 19.10 | ops/s | 8.1x slower |
| openTelemetryExponential | 557.35 | ± 31.44 | ops/s | 9.3x slower |

### TextFormatUtilBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusWriteToNull | 487.10K | ± 1.49K | ops/s | **fastest** |
| prometheusWriteToByteArray | 482.24K | ± 2.67K | ops/s | 1.0x slower |
| openMetricsWriteToNull | 477.39K | ± 3.62K | ops/s | 1.0x slower |
| openMetricsWriteToByteArray | 469.09K | ± 4.44K | ops/s | 1.0x slower |

### Raw Results

```
Benchmark                                            Mode  Cnt          Score        Error  Units
CounterBenchmark.codahaleIncNoLabels                thrpt   15      49744.511   ± 1836.971  ops/s
CounterBenchmark.openTelemetryAdd                   thrpt   15       1562.242    ± 338.570  ops/s
CounterBenchmark.openTelemetryInc                   thrpt   15       1190.232     ± 34.342  ops/s
CounterBenchmark.openTelemetryIncNoLabels           thrpt   15       1253.075    ± 100.966  ops/s
CounterBenchmark.prometheusAdd                      thrpt   15      51448.428    ± 207.185  ops/s
CounterBenchmark.prometheusInc                      thrpt   15      65529.868    ± 830.179  ops/s
CounterBenchmark.prometheusNoLabelsInc              thrpt   15      56651.892    ± 389.678  ops/s
CounterBenchmark.simpleclientAdd                    thrpt   15       6110.766    ± 231.286  ops/s
CounterBenchmark.simpleclientInc                    thrpt   15       6609.081     ± 95.509  ops/s
CounterBenchmark.simpleclientNoLabelsInc            thrpt   15       6468.684    ± 186.387  ops/s
HistogramBenchmark.openTelemetryClassic             thrpt   15        645.519     ± 19.101  ops/s
HistogramBenchmark.openTelemetryExponential         thrpt   15        557.348     ± 31.440  ops/s
HistogramBenchmark.prometheusClassic                thrpt   15       5208.735    ± 414.099  ops/s
HistogramBenchmark.prometheusNative                 thrpt   15       2968.280    ± 321.952  ops/s
HistogramBenchmark.simpleclient                     thrpt   15       4375.984     ± 51.251  ops/s
TextFormatUtilBenchmark.openMetricsWriteToByteArray  thrpt   15     469086.567   ± 4440.687  ops/s
TextFormatUtilBenchmark.openMetricsWriteToNull      thrpt   15     477388.568   ± 3624.540  ops/s
TextFormatUtilBenchmark.prometheusWriteToByteArray  thrpt   15     482239.150   ± 2674.523  ops/s
TextFormatUtilBenchmark.prometheusWriteToNull       thrpt   15     487097.668   ± 1493.611  ops/s
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
