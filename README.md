# Prometheus Java Client Benchmarks

## Run Information

- **Date:** 2026-09-27T08:44:28Z
- **Commit:** [`4b69f40`](https://github.com/psantamaria/client_java/commit/4b69f40bd4e616d69468ce99dc4323162287a577)
- **JDK:** 25.0.2 (OpenJDK 64-Bit Server VM)
- **Benchmark config:** 3 fork(s), 3 warmup, 5 measurement, 4 threads
- **Hardware:** AMD EPYC 9V74 80-Core Processor, 4 cores, 16 GB RAM
- **OS:** Linux 6.17.0-1022-azure

## Results

### CounterBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusInc | 78.38K | ± 1.11K | ops/s | **fastest** |
| prometheusNoLabelsInc | 66.90K | ± 966.83 | ops/s | 1.2x slower |
| prometheusAdd | 62.08K | ± 669.10 | ops/s | 1.3x slower |
| codahaleIncNoLabels | 57.33K | ± 959.58 | ops/s | 1.4x slower |
| simpleclientInc | 8.14K | ± 95.81 | ops/s | 9.6x slower |
| simpleclientNoLabelsInc | 8.06K | ± 63.00 | ops/s | 9.7x slower |
| simpleclientAdd | 7.52K | ± 419.77 | ops/s | 10x slower |
| openTelemetryAdd | 1.73K | ± 110.10 | ops/s | 45x slower |
| openTelemetryInc | 1.70K | ± 46.77 | ops/s | 46x slower |
| openTelemetryIncNoLabels | 1.67K | ± 92.37 | ops/s | 47x slower |

### HistogramBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusClassic | 9.22K | ± 1.95K | ops/s | **fastest** |
| simpleclient | 5.48K | ± 131.61 | ops/s | 1.7x slower |
| prometheusNative | 3.57K | ± 189.28 | ops/s | 2.6x slower |
| openTelemetryClassic | 765.48 | ± 3.77 | ops/s | 12x slower |
| openTelemetryExponential | 695.83 | ± 17.91 | ops/s | 13x slower |

### TextFormatUtilBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusWriteToNull | 671.60K | ± 6.91K | ops/s | **fastest** |
| prometheusWriteToByteArray | 660.29K | ± 3.50K | ops/s | 1.0x slower |
| openMetricsWriteToNull | 648.83K | ± 5.05K | ops/s | 1.0x slower |
| openMetricsWriteToByteArray | 633.94K | ± 4.70K | ops/s | 1.1x slower |

### Raw Results

```
Benchmark                                            Mode  Cnt          Score        Error  Units
CounterBenchmark.codahaleIncNoLabels                thrpt   15      57329.719    ± 959.581  ops/s
CounterBenchmark.openTelemetryAdd                   thrpt   15       1733.870    ± 110.104  ops/s
CounterBenchmark.openTelemetryInc                   thrpt   15       1702.720     ± 46.768  ops/s
CounterBenchmark.openTelemetryIncNoLabels           thrpt   15       1665.942     ± 92.367  ops/s
CounterBenchmark.prometheusAdd                      thrpt   15      62081.348    ± 669.099  ops/s
CounterBenchmark.prometheusInc                      thrpt   15      78384.736   ± 1111.417  ops/s
CounterBenchmark.prometheusNoLabelsInc              thrpt   15      66904.161    ± 966.829  ops/s
CounterBenchmark.simpleclientAdd                    thrpt   15       7515.224    ± 419.771  ops/s
CounterBenchmark.simpleclientInc                    thrpt   15       8138.082     ± 95.808  ops/s
CounterBenchmark.simpleclientNoLabelsInc            thrpt   15       8063.933     ± 62.997  ops/s
HistogramBenchmark.openTelemetryClassic             thrpt   15        765.477      ± 3.768  ops/s
HistogramBenchmark.openTelemetryExponential         thrpt   15        695.828     ± 17.910  ops/s
HistogramBenchmark.prometheusClassic                thrpt   15       9218.489   ± 1951.483  ops/s
HistogramBenchmark.prometheusNative                 thrpt   15       3569.094    ± 189.276  ops/s
HistogramBenchmark.simpleclient                     thrpt   15       5483.332    ± 131.610  ops/s
TextFormatUtilBenchmark.openMetricsWriteToByteArray  thrpt   15     633942.632   ± 4697.087  ops/s
TextFormatUtilBenchmark.openMetricsWriteToNull      thrpt   15     648826.432   ± 5047.647  ops/s
TextFormatUtilBenchmark.prometheusWriteToByteArray  thrpt   15     660294.119   ± 3502.863  ops/s
TextFormatUtilBenchmark.prometheusWriteToNull       thrpt   15     671604.118   ± 6911.784  ops/s
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
