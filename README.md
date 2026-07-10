# Prometheus Java Client Benchmarks

## Run Information

- **Date:** 2026-07-10T07:15:27Z
- **Commit:** [`4b69f40`](https://github.com/psantamaria/client_java/commit/4b69f40bd4e616d69468ce99dc4323162287a577)
- **JDK:** 25.0.2 (OpenJDK 64-Bit Server VM)
- **Benchmark config:** 3 fork(s), 3 warmup, 5 measurement, 4 threads
- **Hardware:** AMD EPYC 7763 64-Core Processor, 4 cores, 16 GB RAM
- **OS:** Linux 6.17.0-1018-azure

## Results

### CounterBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusInc | 65.56K | ± 1.68K | ops/s | **fastest** |
| prometheusNoLabelsInc | 56.79K | ± 365.27 | ops/s | 1.2x slower |
| prometheusAdd | 51.32K | ± 374.83 | ops/s | 1.3x slower |
| codahaleIncNoLabels | 48.84K | ± 1.69K | ops/s | 1.3x slower |
| simpleclientNoLabelsInc | 6.48K | ± 234.27 | ops/s | 10x slower |
| simpleclientInc | 6.45K | ± 199.76 | ops/s | 10x slower |
| simpleclientAdd | 6.32K | ± 173.61 | ops/s | 10x slower |
| openTelemetryAdd | 1.31K | ± 90.49 | ops/s | 50x slower |
| openTelemetryInc | 1.28K | ± 48.36 | ops/s | 51x slower |
| openTelemetryIncNoLabels | 1.26K | ± 31.49 | ops/s | 52x slower |

### HistogramBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusClassic | 7.03K | ± 2.54K | ops/s | **fastest** |
| simpleclient | 4.45K | ± 68.74 | ops/s | 1.6x slower |
| prometheusNative | 3.06K | ± 306.09 | ops/s | 2.3x slower |
| openTelemetryClassic | 701.68 | ± 25.45 | ops/s | 10x slower |
| openTelemetryExponential | 549.49 | ± 18.46 | ops/s | 13x slower |

### TextFormatUtilBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusWriteToNull | 485.34K | ± 3.99K | ops/s | **fastest** |
| prometheusWriteToByteArray | 478.79K | ± 4.85K | ops/s | 1.0x slower |
| openMetricsWriteToByteArray | 474.66K | ± 4.68K | ops/s | 1.0x slower |
| openMetricsWriteToNull | 473.36K | ± 2.23K | ops/s | 1.0x slower |

### Raw Results

```
Benchmark                                            Mode  Cnt          Score        Error  Units
CounterBenchmark.codahaleIncNoLabels                thrpt   15      48839.863   ± 1691.737  ops/s
CounterBenchmark.openTelemetryAdd                   thrpt   15       1313.851     ± 90.485  ops/s
CounterBenchmark.openTelemetryInc                   thrpt   15       1281.969     ± 48.362  ops/s
CounterBenchmark.openTelemetryIncNoLabels           thrpt   15       1262.462     ± 31.493  ops/s
CounterBenchmark.prometheusAdd                      thrpt   15      51324.870    ± 374.829  ops/s
CounterBenchmark.prometheusInc                      thrpt   15      65557.887   ± 1680.663  ops/s
CounterBenchmark.prometheusNoLabelsInc              thrpt   15      56792.116    ± 365.267  ops/s
CounterBenchmark.simpleclientAdd                    thrpt   15       6317.132    ± 173.614  ops/s
CounterBenchmark.simpleclientInc                    thrpt   15       6448.965    ± 199.764  ops/s
CounterBenchmark.simpleclientNoLabelsInc            thrpt   15       6481.395    ± 234.270  ops/s
HistogramBenchmark.openTelemetryClassic             thrpt   15        701.675     ± 25.455  ops/s
HistogramBenchmark.openTelemetryExponential         thrpt   15        549.494     ± 18.459  ops/s
HistogramBenchmark.prometheusClassic                thrpt   15       7027.971   ± 2543.340  ops/s
HistogramBenchmark.prometheusNative                 thrpt   15       3055.867    ± 306.090  ops/s
HistogramBenchmark.simpleclient                     thrpt   15       4454.754     ± 68.740  ops/s
TextFormatUtilBenchmark.openMetricsWriteToByteArray  thrpt   15     474659.545   ± 4679.251  ops/s
TextFormatUtilBenchmark.openMetricsWriteToNull      thrpt   15     473360.347   ± 2226.543  ops/s
TextFormatUtilBenchmark.prometheusWriteToByteArray  thrpt   15     478785.244   ± 4845.390  ops/s
TextFormatUtilBenchmark.prometheusWriteToNull       thrpt   15     485338.472   ± 3987.994  ops/s
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
