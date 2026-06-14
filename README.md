# Prometheus Java Client Benchmarks

## Run Information

- **Date:** 2026-06-14T07:46:33Z
- **Commit:** [`4b69f40`](https://github.com/psantamaria/client_java/commit/4b69f40bd4e616d69468ce99dc4323162287a577)
- **JDK:** 25.0.2 (OpenJDK 64-Bit Server VM)
- **Benchmark config:** 3 fork(s), 3 warmup, 5 measurement, 4 threads
- **Hardware:** AMD EPYC 9V74 80-Core Processor, 4 cores, 16 GB RAM
- **OS:** Linux 6.17.0-1018-azure

## Results

### CounterBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusInc | 75.80K | ± 3.59K | ops/s | **fastest** |
| prometheusNoLabelsInc | 67.11K | ± 977.62 | ops/s | 1.1x slower |
| prometheusAdd | 62.93K | ± 1.25K | ops/s | 1.2x slower |
| codahaleIncNoLabels | 56.66K | ± 293.79 | ops/s | 1.3x slower |
| simpleclientInc | 7.95K | ± 44.20 | ops/s | 9.5x slower |
| simpleclientNoLabelsInc | 7.80K | ± 264.17 | ops/s | 9.7x slower |
| simpleclientAdd | 7.51K | ± 26.67 | ops/s | 10x slower |
| openTelemetryIncNoLabels | 1.74K | ± 138.58 | ops/s | 44x slower |
| openTelemetryInc | 1.67K | ± 156.24 | ops/s | 45x slower |
| openTelemetryAdd | 1.64K | ± 16.19 | ops/s | 46x slower |

### HistogramBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusClassic | 6.41K | ± 1.21K | ops/s | **fastest** |
| simpleclient | 5.82K | ± 106.54 | ops/s | 1.1x slower |
| prometheusNative | 4.05K | ± 111.02 | ops/s | 1.6x slower |
| openTelemetryClassic | 757.13 | ± 5.41 | ops/s | 8.5x slower |
| openTelemetryExponential | 671.30 | ± 23.94 | ops/s | 9.5x slower |

### TextFormatUtilBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusWriteToNull | 674.28K | ± 3.58K | ops/s | **fastest** |
| prometheusWriteToByteArray | 664.14K | ± 8.49K | ops/s | 1.0x slower |
| openMetricsWriteToNull | 648.23K | ± 2.77K | ops/s | 1.0x slower |
| openMetricsWriteToByteArray | 638.13K | ± 2.63K | ops/s | 1.1x slower |

### Raw Results

```
Benchmark                                            Mode  Cnt          Score        Error  Units
CounterBenchmark.codahaleIncNoLabels                thrpt   15      56655.252    ± 293.793  ops/s
CounterBenchmark.openTelemetryAdd                   thrpt   15       1640.109     ± 16.193  ops/s
CounterBenchmark.openTelemetryInc                   thrpt   15       1674.214    ± 156.236  ops/s
CounterBenchmark.openTelemetryIncNoLabels           thrpt   15       1736.198    ± 138.581  ops/s
CounterBenchmark.prometheusAdd                      thrpt   15      62925.218   ± 1249.046  ops/s
CounterBenchmark.prometheusInc                      thrpt   15      75800.460   ± 3594.974  ops/s
CounterBenchmark.prometheusNoLabelsInc              thrpt   15      67108.630    ± 977.622  ops/s
CounterBenchmark.simpleclientAdd                    thrpt   15       7514.557     ± 26.668  ops/s
CounterBenchmark.simpleclientInc                    thrpt   15       7954.354     ± 44.201  ops/s
CounterBenchmark.simpleclientNoLabelsInc            thrpt   15       7802.837    ± 264.172  ops/s
HistogramBenchmark.openTelemetryClassic             thrpt   15        757.129      ± 5.410  ops/s
HistogramBenchmark.openTelemetryExponential         thrpt   15        671.302     ± 23.943  ops/s
HistogramBenchmark.prometheusClassic                thrpt   15       6410.692   ± 1211.894  ops/s
HistogramBenchmark.prometheusNative                 thrpt   15       4047.055    ± 111.016  ops/s
HistogramBenchmark.simpleclient                     thrpt   15       5820.728    ± 106.537  ops/s
TextFormatUtilBenchmark.openMetricsWriteToByteArray  thrpt   15     638125.524   ± 2632.517  ops/s
TextFormatUtilBenchmark.openMetricsWriteToNull      thrpt   15     648225.391   ± 2766.999  ops/s
TextFormatUtilBenchmark.prometheusWriteToByteArray  thrpt   15     664136.016   ± 8494.852  ops/s
TextFormatUtilBenchmark.prometheusWriteToNull       thrpt   15     674283.596   ± 3578.437  ops/s
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
