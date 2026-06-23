# Prometheus Java Client Benchmarks

## Run Information

- **Date:** 2026-06-23T07:19:01Z
- **Commit:** [`4b69f40`](https://github.com/psantamaria/client_java/commit/4b69f40bd4e616d69468ce99dc4323162287a577)
- **JDK:** 25.0.2 (OpenJDK 64-Bit Server VM)
- **Benchmark config:** 3 fork(s), 3 warmup, 5 measurement, 4 threads
- **Hardware:** AMD EPYC 9V74 80-Core Processor, 4 cores, 16 GB RAM
- **OS:** Linux 6.17.0-1018-azure

## Results

### CounterBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusInc | 60.90K | ± 709.78 | ops/s | **fastest** |
| prometheusNoLabelsInc | 51.92K | ± 840.32 | ops/s | 1.2x slower |
| prometheusAdd | 46.93K | ± 2.38K | ops/s | 1.3x slower |
| codahaleIncNoLabels | 43.48K | ± 1.56K | ops/s | 1.4x slower |
| simpleclientInc | 6.24K | ± 73.49 | ops/s | 9.8x slower |
| simpleclientAdd | 6.07K | ± 169.67 | ops/s | 10x slower |
| simpleclientNoLabelsInc | 5.98K | ± 212.79 | ops/s | 10x slower |
| openTelemetryInc | 1.42K | ± 111.73 | ops/s | 43x slower |
| openTelemetryAdd | 1.40K | ± 41.22 | ops/s | 44x slower |
| openTelemetryIncNoLabels | 1.29K | ± 73.75 | ops/s | 47x slower |

### HistogramBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusClassic | 5.49K | ± 2.49K | ops/s | **fastest** |
| simpleclient | 4.52K | ± 90.57 | ops/s | 1.2x slower |
| prometheusNative | 2.84K | ± 113.29 | ops/s | 1.9x slower |
| openTelemetryClassic | 617.99 | ± 13.98 | ops/s | 8.9x slower |
| openTelemetryExponential | 522.66 | ± 22.93 | ops/s | 10x slower |

### TextFormatUtilBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusWriteToNull | 554.81K | ± 5.64K | ops/s | **fastest** |
| prometheusWriteToByteArray | 543.71K | ± 4.38K | ops/s | 1.0x slower |
| openMetricsWriteToNull | 535.59K | ± 6.89K | ops/s | 1.0x slower |
| openMetricsWriteToByteArray | 524.85K | ± 4.63K | ops/s | 1.1x slower |

### Raw Results

```
Benchmark                                            Mode  Cnt          Score        Error  Units
CounterBenchmark.codahaleIncNoLabels                thrpt   15      43476.049   ± 1555.554  ops/s
CounterBenchmark.openTelemetryAdd                   thrpt   15       1397.675     ± 41.221  ops/s
CounterBenchmark.openTelemetryInc                   thrpt   15       1415.129    ± 111.731  ops/s
CounterBenchmark.openTelemetryIncNoLabels           thrpt   15       1294.957     ± 73.745  ops/s
CounterBenchmark.prometheusAdd                      thrpt   15      46934.978   ± 2383.013  ops/s
CounterBenchmark.prometheusInc                      thrpt   15      60898.146    ± 709.781  ops/s
CounterBenchmark.prometheusNoLabelsInc              thrpt   15      51915.912    ± 840.318  ops/s
CounterBenchmark.simpleclientAdd                    thrpt   15       6069.282    ± 169.674  ops/s
CounterBenchmark.simpleclientInc                    thrpt   15       6235.263     ± 73.495  ops/s
CounterBenchmark.simpleclientNoLabelsInc            thrpt   15       5980.727    ± 212.788  ops/s
HistogramBenchmark.openTelemetryClassic             thrpt   15        617.993     ± 13.984  ops/s
HistogramBenchmark.openTelemetryExponential         thrpt   15        522.657     ± 22.928  ops/s
HistogramBenchmark.prometheusClassic                thrpt   15       5485.050   ± 2492.031  ops/s
HistogramBenchmark.prometheusNative                 thrpt   15       2839.739    ± 113.293  ops/s
HistogramBenchmark.simpleclient                     thrpt   15       4518.574     ± 90.575  ops/s
TextFormatUtilBenchmark.openMetricsWriteToByteArray  thrpt   15     524845.911   ± 4633.139  ops/s
TextFormatUtilBenchmark.openMetricsWriteToNull      thrpt   15     535588.523   ± 6885.537  ops/s
TextFormatUtilBenchmark.prometheusWriteToByteArray  thrpt   15     543708.913   ± 4382.322  ops/s
TextFormatUtilBenchmark.prometheusWriteToNull       thrpt   15     554814.882   ± 5636.031  ops/s
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
