# Prometheus Java Client Benchmarks

## Run Information

- **Date:** 2026-07-01T07:37:25Z
- **Commit:** [`4b69f40`](https://github.com/psantamaria/client_java/commit/4b69f40bd4e616d69468ce99dc4323162287a577)
- **JDK:** 25.0.2 (OpenJDK 64-Bit Server VM)
- **Benchmark config:** 3 fork(s), 3 warmup, 5 measurement, 4 threads
- **Hardware:** AMD EPYC 7763 64-Core Processor, 4 cores, 16 GB RAM
- **OS:** Linux 6.17.0-1018-azure

## Results

### CounterBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusInc | 66.93K | ± 410.93 | ops/s | **fastest** |
| prometheusNoLabelsInc | 56.98K | ± 345.72 | ops/s | 1.2x slower |
| prometheusAdd | 51.18K | ± 212.07 | ops/s | 1.3x slower |
| codahaleIncNoLabels | 49.09K | ± 1.50K | ops/s | 1.4x slower |
| simpleclientNoLabelsInc | 6.48K | ± 184.67 | ops/s | 10x slower |
| simpleclientInc | 6.48K | ± 185.47 | ops/s | 10x slower |
| simpleclientAdd | 6.21K | ± 177.91 | ops/s | 11x slower |
| openTelemetryAdd | 1.43K | ± 215.37 | ops/s | 47x slower |
| openTelemetryIncNoLabels | 1.36K | ± 174.55 | ops/s | 49x slower |
| openTelemetryInc | 1.34K | ± 199.07 | ops/s | 50x slower |

### HistogramBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusClassic | 5.87K | ± 1.07K | ops/s | **fastest** |
| simpleclient | 4.47K | ± 48.71 | ops/s | 1.3x slower |
| prometheusNative | 2.74K | ± 331.65 | ops/s | 2.1x slower |
| openTelemetryClassic | 680.25 | ± 17.95 | ops/s | 8.6x slower |
| openTelemetryExponential | 546.79 | ± 12.88 | ops/s | 11x slower |

### TextFormatUtilBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusWriteToNull | 481.55K | ± 2.47K | ops/s | **fastest** |
| openMetricsWriteToNull | 465.18K | ± 8.81K | ops/s | 1.0x slower |
| openMetricsWriteToByteArray | 462.59K | ± 4.58K | ops/s | 1.0x slower |
| prometheusWriteToByteArray | 462.51K | ± 10.50K | ops/s | 1.0x slower |

### Raw Results

```
Benchmark                                            Mode  Cnt          Score        Error  Units
CounterBenchmark.codahaleIncNoLabels                thrpt   15      49086.401   ± 1502.754  ops/s
CounterBenchmark.openTelemetryAdd                   thrpt   15       1427.350    ± 215.371  ops/s
CounterBenchmark.openTelemetryInc                   thrpt   15       1338.916    ± 199.075  ops/s
CounterBenchmark.openTelemetryIncNoLabels           thrpt   15       1361.315    ± 174.547  ops/s
CounterBenchmark.prometheusAdd                      thrpt   15      51181.130    ± 212.074  ops/s
CounterBenchmark.prometheusInc                      thrpt   15      66934.765    ± 410.926  ops/s
CounterBenchmark.prometheusNoLabelsInc              thrpt   15      56980.020    ± 345.717  ops/s
CounterBenchmark.simpleclientAdd                    thrpt   15       6212.397    ± 177.909  ops/s
CounterBenchmark.simpleclientInc                    thrpt   15       6476.699    ± 185.468  ops/s
CounterBenchmark.simpleclientNoLabelsInc            thrpt   15       6480.954    ± 184.673  ops/s
HistogramBenchmark.openTelemetryClassic             thrpt   15        680.254     ± 17.949  ops/s
HistogramBenchmark.openTelemetryExponential         thrpt   15        546.789     ± 12.884  ops/s
HistogramBenchmark.prometheusClassic                thrpt   15       5870.750   ± 1068.526  ops/s
HistogramBenchmark.prometheusNative                 thrpt   15       2741.692    ± 331.650  ops/s
HistogramBenchmark.simpleclient                     thrpt   15       4467.154     ± 48.714  ops/s
TextFormatUtilBenchmark.openMetricsWriteToByteArray  thrpt   15     462585.175   ± 4576.033  ops/s
TextFormatUtilBenchmark.openMetricsWriteToNull      thrpt   15     465183.770   ± 8805.770  ops/s
TextFormatUtilBenchmark.prometheusWriteToByteArray  thrpt   15     462511.321  ± 10501.296  ops/s
TextFormatUtilBenchmark.prometheusWriteToNull       thrpt   15     481550.436   ± 2469.203  ops/s
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
