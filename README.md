# Prometheus Java Client Benchmarks

## Run Information

- **Date:** 2026-05-04T06:46:54Z
- **Commit:** [`4b69f40`](https://github.com/psantamaria/client_java/commit/4b69f40bd4e616d69468ce99dc4323162287a577)
- **JDK:** 25.0.2 (OpenJDK 64-Bit Server VM)
- **Benchmark config:** 3 fork(s), 3 warmup, 5 measurement, 4 threads
- **Hardware:** AMD EPYC 9V74 80-Core Processor, 4 cores, 16 GB RAM
- **OS:** Linux 6.17.0-1010-azure

## Results

### CounterBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusInc | 63.20K | ± 538.92 | ops/s | **fastest** |
| prometheusNoLabelsInc | 54.84K | ± 736.38 | ops/s | 1.2x slower |
| prometheusAdd | 51.81K | ± 1.37K | ops/s | 1.2x slower |
| codahaleIncNoLabels | 47.15K | ± 587.45 | ops/s | 1.3x slower |
| simpleclientInc | 6.52K | ± 133.94 | ops/s | 9.7x slower |
| simpleclientAdd | 6.23K | ± 240.93 | ops/s | 10x slower |
| simpleclientNoLabelsInc | 6.00K | ± 244.25 | ops/s | 11x slower |
| openTelemetryAdd | 1.70K | ± 59.83 | ops/s | 37x slower |
| openTelemetryIncNoLabels | 1.50K | ± 134.82 | ops/s | 42x slower |
| openTelemetryInc | 1.47K | ± 134.21 | ops/s | 43x slower |

### HistogramBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusClassic | 5.60K | ± 1.46K | ops/s | **fastest** |
| simpleclient | 4.48K | ± 79.53 | ops/s | 1.2x slower |
| prometheusNative | 3.17K | ± 262.31 | ops/s | 1.8x slower |
| openTelemetryClassic | 633.12 | ± 9.28 | ops/s | 8.8x slower |
| openTelemetryExponential | 522.01 | ± 10.79 | ops/s | 11x slower |

### TextFormatUtilBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusWriteToNull | 606.30K | ± 8.93K | ops/s | **fastest** |
| prometheusWriteToByteArray | 582.58K | ± 13.40K | ops/s | 1.0x slower |
| openMetricsWriteToNull | 574.51K | ± 7.00K | ops/s | 1.1x slower |
| openMetricsWriteToByteArray | 550.64K | ± 9.13K | ops/s | 1.1x slower |

### Raw Results

```
Benchmark                                            Mode  Cnt          Score        Error  Units
CounterBenchmark.codahaleIncNoLabels                thrpt   15      47147.734    ± 587.449  ops/s
CounterBenchmark.openTelemetryAdd                   thrpt   15       1703.726     ± 59.829  ops/s
CounterBenchmark.openTelemetryInc                   thrpt   15       1467.854    ± 134.208  ops/s
CounterBenchmark.openTelemetryIncNoLabels           thrpt   15       1502.913    ± 134.819  ops/s
CounterBenchmark.prometheusAdd                      thrpt   15      51809.841   ± 1374.589  ops/s
CounterBenchmark.prometheusInc                      thrpt   15      63197.045    ± 538.917  ops/s
CounterBenchmark.prometheusNoLabelsInc              thrpt   15      54844.124    ± 736.385  ops/s
CounterBenchmark.simpleclientAdd                    thrpt   15       6225.760    ± 240.932  ops/s
CounterBenchmark.simpleclientInc                    thrpt   15       6516.234    ± 133.938  ops/s
CounterBenchmark.simpleclientNoLabelsInc            thrpt   15       5999.303    ± 244.247  ops/s
HistogramBenchmark.openTelemetryClassic             thrpt   15        633.120      ± 9.276  ops/s
HistogramBenchmark.openTelemetryExponential         thrpt   15        522.011     ± 10.787  ops/s
HistogramBenchmark.prometheusClassic                thrpt   15       5599.239   ± 1459.866  ops/s
HistogramBenchmark.prometheusNative                 thrpt   15       3174.431    ± 262.315  ops/s
HistogramBenchmark.simpleclient                     thrpt   15       4484.175     ± 79.534  ops/s
TextFormatUtilBenchmark.openMetricsWriteToByteArray  thrpt   15     550637.141   ± 9134.823  ops/s
TextFormatUtilBenchmark.openMetricsWriteToNull      thrpt   15     574510.099   ± 6997.377  ops/s
TextFormatUtilBenchmark.prometheusWriteToByteArray  thrpt   15     582578.264  ± 13401.242  ops/s
TextFormatUtilBenchmark.prometheusWriteToNull       thrpt   15     606299.559   ± 8927.426  ops/s
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
