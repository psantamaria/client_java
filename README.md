# Prometheus Java Client Benchmarks

## Run Information

- **Date:** 2026-09-19T08:12:26Z
- **Commit:** [`4b69f40`](https://github.com/psantamaria/client_java/commit/4b69f40bd4e616d69468ce99dc4323162287a577)
- **JDK:** 25.0.2 (OpenJDK 64-Bit Server VM)
- **Benchmark config:** 3 fork(s), 3 warmup, 5 measurement, 4 threads
- **Hardware:** AMD EPYC 7763 64-Core Processor, 4 cores, 16 GB RAM
- **OS:** Linux 6.17.0-1022-azure

## Results

### CounterBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusInc | 66.39K | ± 155.49 | ops/s | **fastest** |
| prometheusNoLabelsInc | 57.07K | ± 127.23 | ops/s | 1.2x slower |
| prometheusAdd | 50.74K | ± 686.38 | ops/s | 1.3x slower |
| codahaleIncNoLabels | 49.06K | ± 1.93K | ops/s | 1.4x slower |
| simpleclientInc | 6.58K | ± 170.34 | ops/s | 10x slower |
| simpleclientNoLabelsInc | 6.36K | ± 194.33 | ops/s | 10x slower |
| simpleclientAdd | 6.02K | ± 66.46 | ops/s | 11x slower |
| openTelemetryInc | 1.35K | ± 169.62 | ops/s | 49x slower |
| openTelemetryAdd | 1.26K | ± 68.37 | ops/s | 53x slower |
| openTelemetryIncNoLabels | 1.18K | ± 31.14 | ops/s | 56x slower |

### HistogramBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusClassic | 5.33K | ± 1.00K | ops/s | **fastest** |
| simpleclient | 4.40K | ± 99.44 | ops/s | 1.2x slower |
| prometheusNative | 2.80K | ± 373.64 | ops/s | 1.9x slower |
| openTelemetryClassic | 679.94 | ± 40.10 | ops/s | 7.8x slower |
| openTelemetryExponential | 573.57 | ± 28.57 | ops/s | 9.3x slower |

### TextFormatUtilBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusWriteToNull | 494.44K | ± 3.59K | ops/s | **fastest** |
| openMetricsWriteToNull | 488.43K | ± 5.81K | ops/s | 1.0x slower |
| prometheusWriteToByteArray | 485.93K | ± 5.22K | ops/s | 1.0x slower |
| openMetricsWriteToByteArray | 477.68K | ± 3.58K | ops/s | 1.0x slower |

### Raw Results

```
Benchmark                                            Mode  Cnt          Score        Error  Units
CounterBenchmark.codahaleIncNoLabels                thrpt   15      49058.414   ± 1931.190  ops/s
CounterBenchmark.openTelemetryAdd                   thrpt   15       1262.513     ± 68.370  ops/s
CounterBenchmark.openTelemetryInc                   thrpt   15       1347.177    ± 169.618  ops/s
CounterBenchmark.openTelemetryIncNoLabels           thrpt   15       1179.595     ± 31.143  ops/s
CounterBenchmark.prometheusAdd                      thrpt   15      50739.504    ± 686.377  ops/s
CounterBenchmark.prometheusInc                      thrpt   15      66389.757    ± 155.486  ops/s
CounterBenchmark.prometheusNoLabelsInc              thrpt   15      57066.283    ± 127.232  ops/s
CounterBenchmark.simpleclientAdd                    thrpt   15       6024.139     ± 66.460  ops/s
CounterBenchmark.simpleclientInc                    thrpt   15       6580.441    ± 170.345  ops/s
CounterBenchmark.simpleclientNoLabelsInc            thrpt   15       6356.915    ± 194.329  ops/s
HistogramBenchmark.openTelemetryClassic             thrpt   15        679.936     ± 40.103  ops/s
HistogramBenchmark.openTelemetryExponential         thrpt   15        573.571     ± 28.574  ops/s
HistogramBenchmark.prometheusClassic                thrpt   15       5326.030   ± 1003.471  ops/s
HistogramBenchmark.prometheusNative                 thrpt   15       2797.935    ± 373.637  ops/s
HistogramBenchmark.simpleclient                     thrpt   15       4398.751     ± 99.443  ops/s
TextFormatUtilBenchmark.openMetricsWriteToByteArray  thrpt   15     477680.630   ± 3579.475  ops/s
TextFormatUtilBenchmark.openMetricsWriteToNull      thrpt   15     488426.558   ± 5812.237  ops/s
TextFormatUtilBenchmark.prometheusWriteToByteArray  thrpt   15     485933.770   ± 5224.330  ops/s
TextFormatUtilBenchmark.prometheusWriteToNull       thrpt   15     494436.372   ± 3586.780  ops/s
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
