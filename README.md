# Prometheus Java Client Benchmarks

## Run Information

- **Date:** 2026-09-17T08:18:35Z
- **Commit:** [`4b69f40`](https://github.com/psantamaria/client_java/commit/4b69f40bd4e616d69468ce99dc4323162287a577)
- **JDK:** 25.0.2 (OpenJDK 64-Bit Server VM)
- **Benchmark config:** 3 fork(s), 3 warmup, 5 measurement, 4 threads
- **Hardware:** AMD EPYC 7763 64-Core Processor, 4 cores, 16 GB RAM
- **OS:** Linux 6.17.0-1022-azure

## Results

### CounterBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusInc | 66.43K | ± 548.74 | ops/s | **fastest** |
| prometheusNoLabelsInc | 56.83K | ± 347.87 | ops/s | 1.2x slower |
| prometheusAdd | 50.82K | ± 681.58 | ops/s | 1.3x slower |
| codahaleIncNoLabels | 49.42K | ± 1.99K | ops/s | 1.3x slower |
| simpleclientInc | 6.67K | ± 23.94 | ops/s | 10.0x slower |
| simpleclientNoLabelsInc | 6.61K | ± 16.75 | ops/s | 10x slower |
| simpleclientAdd | 6.34K | ± 192.33 | ops/s | 10x slower |
| openTelemetryAdd | 1.41K | ± 252.43 | ops/s | 47x slower |
| openTelemetryIncNoLabels | 1.33K | ± 205.14 | ops/s | 50x slower |
| openTelemetryInc | 1.25K | ± 34.20 | ops/s | 53x slower |

### HistogramBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusClassic | 6.56K | ± 922.83 | ops/s | **fastest** |
| simpleclient | 4.42K | ± 55.47 | ops/s | 1.5x slower |
| prometheusNative | 2.93K | ± 386.45 | ops/s | 2.2x slower |
| openTelemetryClassic | 699.40 | ± 29.20 | ops/s | 9.4x slower |
| openTelemetryExponential | 560.22 | ± 17.52 | ops/s | 12x slower |

### TextFormatUtilBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusWriteToNull | 489.68K | ± 1.28K | ops/s | **fastest** |
| openMetricsWriteToNull | 485.36K | ± 1.57K | ops/s | 1.0x slower |
| prometheusWriteToByteArray | 484.96K | ± 3.55K | ops/s | 1.0x slower |
| openMetricsWriteToByteArray | 470.54K | ± 4.34K | ops/s | 1.0x slower |

### Raw Results

```
Benchmark                                            Mode  Cnt          Score        Error  Units
CounterBenchmark.codahaleIncNoLabels                thrpt   15      49424.947   ± 1994.922  ops/s
CounterBenchmark.openTelemetryAdd                   thrpt   15       1409.135    ± 252.429  ops/s
CounterBenchmark.openTelemetryInc                   thrpt   15       1247.365     ± 34.203  ops/s
CounterBenchmark.openTelemetryIncNoLabels           thrpt   15       1328.525    ± 205.141  ops/s
CounterBenchmark.prometheusAdd                      thrpt   15      50821.700    ± 681.578  ops/s
CounterBenchmark.prometheusInc                      thrpt   15      66428.858    ± 548.736  ops/s
CounterBenchmark.prometheusNoLabelsInc              thrpt   15      56825.270    ± 347.866  ops/s
CounterBenchmark.simpleclientAdd                    thrpt   15       6337.638    ± 192.327  ops/s
CounterBenchmark.simpleclientInc                    thrpt   15       6671.185     ± 23.938  ops/s
CounterBenchmark.simpleclientNoLabelsInc            thrpt   15       6609.736     ± 16.749  ops/s
HistogramBenchmark.openTelemetryClassic             thrpt   15        699.405     ± 29.200  ops/s
HistogramBenchmark.openTelemetryExponential         thrpt   15        560.218     ± 17.516  ops/s
HistogramBenchmark.prometheusClassic                thrpt   15       6564.331    ± 922.831  ops/s
HistogramBenchmark.prometheusNative                 thrpt   15       2929.327    ± 386.454  ops/s
HistogramBenchmark.simpleclient                     thrpt   15       4417.293     ± 55.472  ops/s
TextFormatUtilBenchmark.openMetricsWriteToByteArray  thrpt   15     470535.969   ± 4336.601  ops/s
TextFormatUtilBenchmark.openMetricsWriteToNull      thrpt   15     485358.860   ± 1565.590  ops/s
TextFormatUtilBenchmark.prometheusWriteToByteArray  thrpt   15     484959.341   ± 3548.540  ops/s
TextFormatUtilBenchmark.prometheusWriteToNull       thrpt   15     489678.080   ± 1275.556  ops/s
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
