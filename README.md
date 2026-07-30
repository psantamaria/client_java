# Prometheus Java Client Benchmarks

## Run Information

- **Date:** 2026-07-30T06:10:34Z
- **Commit:** [`4b69f40`](https://github.com/psantamaria/client_java/commit/4b69f40bd4e616d69468ce99dc4323162287a577)
- **JDK:** 25.0.2 (OpenJDK 64-Bit Server VM)
- **Benchmark config:** 3 fork(s), 3 warmup, 5 measurement, 4 threads
- **Hardware:** AMD EPYC 9V74 80-Core Processor, 4 cores, 16 GB RAM
- **OS:** Linux 6.17.0-1020-azure

## Results

### CounterBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusInc | 77.95K | ± 1.06K | ops/s | **fastest** |
| prometheusNoLabelsInc | 66.44K | ± 1.47K | ops/s | 1.2x slower |
| prometheusAdd | 62.23K | ± 673.03 | ops/s | 1.3x slower |
| codahaleIncNoLabels | 55.23K | ± 2.35K | ops/s | 1.4x slower |
| simpleclientInc | 8.06K | ± 200.08 | ops/s | 9.7x slower |
| simpleclientNoLabelsInc | 7.87K | ± 312.03 | ops/s | 9.9x slower |
| simpleclientAdd | 7.44K | ± 84.90 | ops/s | 10x slower |
| openTelemetryInc | 1.84K | ± 145.50 | ops/s | 42x slower |
| openTelemetryAdd | 1.82K | ± 123.70 | ops/s | 43x slower |
| openTelemetryIncNoLabels | 1.73K | ± 127.09 | ops/s | 45x slower |

### HistogramBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusClassic | 7.01K | ± 1.35K | ops/s | **fastest** |
| simpleclient | 5.81K | ± 183.39 | ops/s | 1.2x slower |
| prometheusNative | 3.91K | ± 302.88 | ops/s | 1.8x slower |
| openTelemetryClassic | 810.82 | ± 8.62 | ops/s | 8.6x slower |
| openTelemetryExponential | 697.48 | ± 24.15 | ops/s | 10x slower |

### TextFormatUtilBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusWriteToNull | 670.40K | ± 3.76K | ops/s | **fastest** |
| prometheusWriteToByteArray | 656.66K | ± 4.33K | ops/s | 1.0x slower |
| openMetricsWriteToNull | 645.96K | ± 5.29K | ops/s | 1.0x slower |
| openMetricsWriteToByteArray | 629.34K | ± 8.65K | ops/s | 1.1x slower |

### Raw Results

```
Benchmark                                            Mode  Cnt          Score        Error  Units
CounterBenchmark.codahaleIncNoLabels                thrpt   15      55228.803   ± 2346.070  ops/s
CounterBenchmark.openTelemetryAdd                   thrpt   15       1821.098    ± 123.700  ops/s
CounterBenchmark.openTelemetryInc                   thrpt   15       1840.396    ± 145.496  ops/s
CounterBenchmark.openTelemetryIncNoLabels           thrpt   15       1734.846    ± 127.088  ops/s
CounterBenchmark.prometheusAdd                      thrpt   15      62231.778    ± 673.026  ops/s
CounterBenchmark.prometheusInc                      thrpt   15      77951.993   ± 1059.233  ops/s
CounterBenchmark.prometheusNoLabelsInc              thrpt   15      66435.991   ± 1469.404  ops/s
CounterBenchmark.simpleclientAdd                    thrpt   15       7439.172     ± 84.897  ops/s
CounterBenchmark.simpleclientInc                    thrpt   15       8055.814    ± 200.077  ops/s
CounterBenchmark.simpleclientNoLabelsInc            thrpt   15       7869.290    ± 312.026  ops/s
HistogramBenchmark.openTelemetryClassic             thrpt   15        810.823      ± 8.616  ops/s
HistogramBenchmark.openTelemetryExponential         thrpt   15        697.476     ± 24.148  ops/s
HistogramBenchmark.prometheusClassic                thrpt   15       7012.124   ± 1354.221  ops/s
HistogramBenchmark.prometheusNative                 thrpt   15       3906.281    ± 302.883  ops/s
HistogramBenchmark.simpleclient                     thrpt   15       5809.672    ± 183.393  ops/s
TextFormatUtilBenchmark.openMetricsWriteToByteArray  thrpt   15     629336.474   ± 8651.346  ops/s
TextFormatUtilBenchmark.openMetricsWriteToNull      thrpt   15     645964.317   ± 5287.840  ops/s
TextFormatUtilBenchmark.prometheusWriteToByteArray  thrpt   15     656664.541   ± 4332.269  ops/s
TextFormatUtilBenchmark.prometheusWriteToNull       thrpt   15     670402.353   ± 3761.141  ops/s
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
