# Prometheus Java Client Benchmarks

## Run Information

- **Date:** 2026-08-08T04:36:08Z
- **Commit:** [`4b69f40`](https://github.com/psantamaria/client_java/commit/4b69f40bd4e616d69468ce99dc4323162287a577)
- **JDK:** 25.0.2 (OpenJDK 64-Bit Server VM)
- **Benchmark config:** 3 fork(s), 3 warmup, 5 measurement, 4 threads
- **Hardware:** AMD EPYC 9V74 80-Core Processor, 4 cores, 16 GB RAM
- **OS:** Linux 6.17.0-1020-azure

## Results

### CounterBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusInc | 59.39K | ± 1.55K | ops/s | **fastest** |
| prometheusNoLabelsInc | 51.54K | ± 1.13K | ops/s | 1.2x slower |
| prometheusAdd | 48.23K | ± 354.66 | ops/s | 1.2x slower |
| codahaleIncNoLabels | 43.58K | ± 826.84 | ops/s | 1.4x slower |
| simpleclientInc | 6.26K | ± 132.74 | ops/s | 9.5x slower |
| simpleclientNoLabelsInc | 6.14K | ± 203.62 | ops/s | 9.7x slower |
| simpleclientAdd | 5.79K | ± 180.46 | ops/s | 10x slower |
| openTelemetryIncNoLabels | 1.50K | ± 55.65 | ops/s | 40x slower |
| openTelemetryInc | 1.50K | ± 52.19 | ops/s | 40x slower |
| openTelemetryAdd | 1.49K | ± 97.48 | ops/s | 40x slower |

### HistogramBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusClassic | 4.82K | ± 761.63 | ops/s | **fastest** |
| simpleclient | 4.56K | ± 58.42 | ops/s | 1.1x slower |
| prometheusNative | 3.04K | ± 288.56 | ops/s | 1.6x slower |
| openTelemetryClassic | 646.61 | ± 34.65 | ops/s | 7.5x slower |
| openTelemetryExponential | 531.69 | ± 7.48 | ops/s | 9.1x slower |

### TextFormatUtilBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusWriteToNull | 535.88K | ± 5.40K | ops/s | **fastest** |
| prometheusWriteToByteArray | 527.32K | ± 5.70K | ops/s | 1.0x slower |
| openMetricsWriteToNull | 518.53K | ± 3.99K | ops/s | 1.0x slower |
| openMetricsWriteToByteArray | 510.77K | ± 1.16K | ops/s | 1.0x slower |

### Raw Results

```
Benchmark                                            Mode  Cnt          Score        Error  Units
CounterBenchmark.codahaleIncNoLabels                thrpt   15      43584.895    ± 826.839  ops/s
CounterBenchmark.openTelemetryAdd                   thrpt   15       1487.968     ± 97.476  ops/s
CounterBenchmark.openTelemetryInc                   thrpt   15       1498.198     ± 52.187  ops/s
CounterBenchmark.openTelemetryIncNoLabels           thrpt   15       1499.638     ± 55.651  ops/s
CounterBenchmark.prometheusAdd                      thrpt   15      48228.971    ± 354.664  ops/s
CounterBenchmark.prometheusInc                      thrpt   15      59389.831   ± 1548.634  ops/s
CounterBenchmark.prometheusNoLabelsInc              thrpt   15      51544.953   ± 1125.437  ops/s
CounterBenchmark.simpleclientAdd                    thrpt   15       5793.432    ± 180.458  ops/s
CounterBenchmark.simpleclientInc                    thrpt   15       6261.238    ± 132.737  ops/s
CounterBenchmark.simpleclientNoLabelsInc            thrpt   15       6140.653    ± 203.617  ops/s
HistogramBenchmark.openTelemetryClassic             thrpt   15        646.607     ± 34.652  ops/s
HistogramBenchmark.openTelemetryExponential         thrpt   15        531.695      ± 7.483  ops/s
HistogramBenchmark.prometheusClassic                thrpt   15       4823.168    ± 761.627  ops/s
HistogramBenchmark.prometheusNative                 thrpt   15       3043.209    ± 288.559  ops/s
HistogramBenchmark.simpleclient                     thrpt   15       4561.088     ± 58.422  ops/s
TextFormatUtilBenchmark.openMetricsWriteToByteArray  thrpt   15     510773.043   ± 1164.826  ops/s
TextFormatUtilBenchmark.openMetricsWriteToNull      thrpt   15     518529.165   ± 3994.787  ops/s
TextFormatUtilBenchmark.prometheusWriteToByteArray  thrpt   15     527315.393   ± 5695.850  ops/s
TextFormatUtilBenchmark.prometheusWriteToNull       thrpt   15     535875.473   ± 5404.030  ops/s
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
