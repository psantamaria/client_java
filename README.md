# Prometheus Java Client Benchmarks

## Run Information

- **Date:** 2026-05-13T07:00:53Z
- **Commit:** [`4b69f40`](https://github.com/psantamaria/client_java/commit/4b69f40bd4e616d69468ce99dc4323162287a577)
- **JDK:** 25.0.2 (OpenJDK 64-Bit Server VM)
- **Benchmark config:** 3 fork(s), 3 warmup, 5 measurement, 4 threads
- **Hardware:** AMD EPYC 9V74 80-Core Processor, 4 cores, 16 GB RAM
- **OS:** Linux 6.17.0-1010-azure

## Results

### CounterBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusInc | 60.11K | ± 1.10K | ops/s | **fastest** |
| prometheusNoLabelsInc | 51.29K | ± 331.95 | ops/s | 1.2x slower |
| prometheusAdd | 49.26K | ± 1.09K | ops/s | 1.2x slower |
| codahaleIncNoLabels | 43.76K | ± 387.84 | ops/s | 1.4x slower |
| simpleclientNoLabelsInc | 6.26K | ± 29.70 | ops/s | 9.6x slower |
| simpleclientInc | 6.23K | ± 109.69 | ops/s | 9.6x slower |
| simpleclientAdd | 5.67K | ± 109.77 | ops/s | 11x slower |
| openTelemetryIncNoLabels | 1.57K | ± 52.70 | ops/s | 38x slower |
| openTelemetryInc | 1.36K | ± 62.51 | ops/s | 44x slower |
| openTelemetryAdd | 1.35K | ± 16.94 | ops/s | 45x slower |

### HistogramBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusClassic | 5.31K | ± 1.72K | ops/s | **fastest** |
| simpleclient | 4.20K | ± 65.48 | ops/s | 1.3x slower |
| prometheusNative | 3.01K | ± 220.92 | ops/s | 1.8x slower |
| openTelemetryClassic | 621.01 | ± 11.13 | ops/s | 8.6x slower |
| openTelemetryExponential | 556.11 | ± 14.53 | ops/s | 9.5x slower |

### TextFormatUtilBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusWriteToNull | 559.36K | ± 1.96K | ops/s | **fastest** |
| openMetricsWriteToNull | 542.62K | ± 2.34K | ops/s | 1.0x slower |
| prometheusWriteToByteArray | 542.30K | ± 4.36K | ops/s | 1.0x slower |
| openMetricsWriteToByteArray | 526.85K | ± 5.92K | ops/s | 1.1x slower |

### Raw Results

```
Benchmark                                            Mode  Cnt          Score        Error  Units
CounterBenchmark.codahaleIncNoLabels                thrpt   15      43762.427    ± 387.844  ops/s
CounterBenchmark.openTelemetryAdd                   thrpt   15       1347.962     ± 16.941  ops/s
CounterBenchmark.openTelemetryInc                   thrpt   15       1357.983     ± 62.509  ops/s
CounterBenchmark.openTelemetryIncNoLabels           thrpt   15       1570.201     ± 52.700  ops/s
CounterBenchmark.prometheusAdd                      thrpt   15      49257.632   ± 1089.039  ops/s
CounterBenchmark.prometheusInc                      thrpt   15      60109.628   ± 1104.204  ops/s
CounterBenchmark.prometheusNoLabelsInc              thrpt   15      51293.875    ± 331.949  ops/s
CounterBenchmark.simpleclientAdd                    thrpt   15       5673.599    ± 109.775  ops/s
CounterBenchmark.simpleclientInc                    thrpt   15       6232.234    ± 109.690  ops/s
CounterBenchmark.simpleclientNoLabelsInc            thrpt   15       6255.218     ± 29.697  ops/s
HistogramBenchmark.openTelemetryClassic             thrpt   15        621.009     ± 11.128  ops/s
HistogramBenchmark.openTelemetryExponential         thrpt   15        556.112     ± 14.532  ops/s
HistogramBenchmark.prometheusClassic                thrpt   15       5309.986   ± 1720.120  ops/s
HistogramBenchmark.prometheusNative                 thrpt   15       3008.970    ± 220.921  ops/s
HistogramBenchmark.simpleclient                     thrpt   15       4198.108     ± 65.483  ops/s
TextFormatUtilBenchmark.openMetricsWriteToByteArray  thrpt   15     526846.373   ± 5918.094  ops/s
TextFormatUtilBenchmark.openMetricsWriteToNull      thrpt   15     542621.911   ± 2341.552  ops/s
TextFormatUtilBenchmark.prometheusWriteToByteArray  thrpt   15     542302.812   ± 4364.904  ops/s
TextFormatUtilBenchmark.prometheusWriteToNull       thrpt   15     559360.216   ± 1957.847  ops/s
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
