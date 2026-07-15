# Prometheus Java Client Benchmarks

## Run Information

- **Date:** 2026-07-15T06:03:21Z
- **Commit:** [`4b69f40`](https://github.com/psantamaria/client_java/commit/4b69f40bd4e616d69468ce99dc4323162287a577)
- **JDK:** 25.0.2 (OpenJDK 64-Bit Server VM)
- **Benchmark config:** 3 fork(s), 3 warmup, 5 measurement, 4 threads
- **Hardware:** INTEL(R) XEON(R) PLATINUM 8573C, 4 cores, 16 GB RAM
- **OS:** Linux 6.17.0-1018-azure

## Results

### CounterBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| codahaleIncNoLabels | 27.59K | ± 170.32 | ops/s | **fastest** |
| prometheusNoLabelsInc | 26.83K | ± 38.55 | ops/s | 1.0x slower |
| prometheusInc | 26.60K | ± 33.65 | ops/s | 1.0x slower |
| prometheusAdd | 25.78K | ± 230.16 | ops/s | 1.1x slower |
| simpleclientNoLabelsInc | 6.67K | ± 51.19 | ops/s | 4.1x slower |
| simpleclientInc | 6.67K | ± 41.25 | ops/s | 4.1x slower |
| simpleclientAdd | 6.47K | ± 132.11 | ops/s | 4.3x slower |
| openTelemetryIncNoLabels | 1.06K | ± 105.91 | ops/s | 26x slower |
| openTelemetryInc | 1.03K | ± 63.61 | ops/s | 27x slower |
| openTelemetryAdd | 1.00K | ± 63.83 | ops/s | 28x slower |

### HistogramBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| simpleclient | 4.38K | ± 85.13 | ops/s | **fastest** |
| prometheusClassic | 2.88K | ± 715.67 | ops/s | 1.5x slower |
| prometheusNative | 2.07K | ± 210.20 | ops/s | 2.1x slower |
| openTelemetryClassic | 362.33 | ± 10.61 | ops/s | 12x slower |
| openTelemetryExponential | 323.13 | ± 18.30 | ops/s | 14x slower |

### TextFormatUtilBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusWriteToNull | 286.72K | ± 4.62K | ops/s | **fastest** |
| prometheusWriteToByteArray | 284.69K | ± 3.51K | ops/s | 1.0x slower |
| openMetricsWriteToNull | 270.08K | ± 1.92K | ops/s | 1.1x slower |
| openMetricsWriteToByteArray | 265.57K | ± 1.91K | ops/s | 1.1x slower |

### Raw Results

```
Benchmark                                            Mode  Cnt          Score        Error  Units
CounterBenchmark.codahaleIncNoLabels                thrpt   15      27587.820    ± 170.323  ops/s
CounterBenchmark.openTelemetryAdd                   thrpt   15       1003.073     ± 63.828  ops/s
CounterBenchmark.openTelemetryInc                   thrpt   15       1030.677     ± 63.605  ops/s
CounterBenchmark.openTelemetryIncNoLabels           thrpt   15       1063.867    ± 105.905  ops/s
CounterBenchmark.prometheusAdd                      thrpt   15      25784.477    ± 230.163  ops/s
CounterBenchmark.prometheusInc                      thrpt   15      26603.975     ± 33.649  ops/s
CounterBenchmark.prometheusNoLabelsInc              thrpt   15      26826.341     ± 38.552  ops/s
CounterBenchmark.simpleclientAdd                    thrpt   15       6466.416    ± 132.113  ops/s
CounterBenchmark.simpleclientInc                    thrpt   15       6667.753     ± 41.245  ops/s
CounterBenchmark.simpleclientNoLabelsInc            thrpt   15       6669.796     ± 51.185  ops/s
HistogramBenchmark.openTelemetryClassic             thrpt   15        362.325     ± 10.611  ops/s
HistogramBenchmark.openTelemetryExponential         thrpt   15        323.132     ± 18.298  ops/s
HistogramBenchmark.prometheusClassic                thrpt   15       2879.841    ± 715.674  ops/s
HistogramBenchmark.prometheusNative                 thrpt   15       2073.497    ± 210.203  ops/s
HistogramBenchmark.simpleclient                     thrpt   15       4380.553     ± 85.128  ops/s
TextFormatUtilBenchmark.openMetricsWriteToByteArray  thrpt   15     265566.874   ± 1908.472  ops/s
TextFormatUtilBenchmark.openMetricsWriteToNull      thrpt   15     270078.557   ± 1918.971  ops/s
TextFormatUtilBenchmark.prometheusWriteToByteArray  thrpt   15     284691.301   ± 3506.039  ops/s
TextFormatUtilBenchmark.prometheusWriteToNull       thrpt   15     286723.950   ± 4621.708  ops/s
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
