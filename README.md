# Prometheus Java Client Benchmarks

## Run Information

- **Date:** 2026-09-08T08:06:18Z
- **Commit:** [`4b69f40`](https://github.com/psantamaria/client_java/commit/4b69f40bd4e616d69468ce99dc4323162287a577)
- **JDK:** 25.0.2 (OpenJDK 64-Bit Server VM)
- **Benchmark config:** 3 fork(s), 3 warmup, 5 measurement, 4 threads
- **Hardware:** AMD EPYC 7763 64-Core Processor, 4 cores, 16 GB RAM
- **OS:** Linux 6.17.0-1022-azure

## Results

### CounterBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusInc | 65.76K | ± 1.75K | ops/s | **fastest** |
| prometheusNoLabelsInc | 55.44K | ± 2.64K | ops/s | 1.2x slower |
| prometheusAdd | 51.15K | ± 646.45 | ops/s | 1.3x slower |
| codahaleIncNoLabels | 48.25K | ± 1.53K | ops/s | 1.4x slower |
| simpleclientInc | 6.50K | ± 182.85 | ops/s | 10x slower |
| simpleclientAdd | 6.32K | ± 191.72 | ops/s | 10x slower |
| simpleclientNoLabelsInc | 6.23K | ± 14.66 | ops/s | 11x slower |
| openTelemetryAdd | 1.44K | ± 246.89 | ops/s | 46x slower |
| openTelemetryInc | 1.26K | ± 48.89 | ops/s | 52x slower |
| openTelemetryIncNoLabels | 1.21K | ± 37.84 | ops/s | 54x slower |

### HistogramBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusClassic | 7.80K | ± 1.44K | ops/s | **fastest** |
| simpleclient | 4.46K | ± 51.90 | ops/s | 1.8x slower |
| prometheusNative | 2.70K | ± 77.72 | ops/s | 2.9x slower |
| openTelemetryClassic | 668.40 | ± 10.71 | ops/s | 12x slower |
| openTelemetryExponential | 586.22 | ± 29.87 | ops/s | 13x slower |

### TextFormatUtilBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusWriteToByteArray | 481.11K | ± 4.70K | ops/s | **fastest** |
| prometheusWriteToNull | 476.33K | ± 3.58K | ops/s | 1.0x slower |
| openMetricsWriteToByteArray | 467.04K | ± 2.41K | ops/s | 1.0x slower |
| openMetricsWriteToNull | 461.20K | ± 8.18K | ops/s | 1.0x slower |

### Raw Results

```
Benchmark                                            Mode  Cnt          Score        Error  Units
CounterBenchmark.codahaleIncNoLabels                thrpt   15      48245.142   ± 1526.294  ops/s
CounterBenchmark.openTelemetryAdd                   thrpt   15       1444.576    ± 246.889  ops/s
CounterBenchmark.openTelemetryInc                   thrpt   15       1259.377     ± 48.885  ops/s
CounterBenchmark.openTelemetryIncNoLabels           thrpt   15       1208.915     ± 37.836  ops/s
CounterBenchmark.prometheusAdd                      thrpt   15      51146.097    ± 646.453  ops/s
CounterBenchmark.prometheusInc                      thrpt   15      65755.888   ± 1753.443  ops/s
CounterBenchmark.prometheusNoLabelsInc              thrpt   15      55438.092   ± 2643.102  ops/s
CounterBenchmark.simpleclientAdd                    thrpt   15       6315.997    ± 191.721  ops/s
CounterBenchmark.simpleclientInc                    thrpt   15       6499.915    ± 182.850  ops/s
CounterBenchmark.simpleclientNoLabelsInc            thrpt   15       6225.526     ± 14.658  ops/s
HistogramBenchmark.openTelemetryClassic             thrpt   15        668.401     ± 10.708  ops/s
HistogramBenchmark.openTelemetryExponential         thrpt   15        586.217     ± 29.870  ops/s
HistogramBenchmark.prometheusClassic                thrpt   15       7801.704   ± 1444.600  ops/s
HistogramBenchmark.prometheusNative                 thrpt   15       2703.420     ± 77.718  ops/s
HistogramBenchmark.simpleclient                     thrpt   15       4457.489     ± 51.896  ops/s
TextFormatUtilBenchmark.openMetricsWriteToByteArray  thrpt   15     467038.953   ± 2413.723  ops/s
TextFormatUtilBenchmark.openMetricsWriteToNull      thrpt   15     461204.869   ± 8175.623  ops/s
TextFormatUtilBenchmark.prometheusWriteToByteArray  thrpt   15     481106.049   ± 4701.008  ops/s
TextFormatUtilBenchmark.prometheusWriteToNull       thrpt   15     476330.572   ± 3580.256  ops/s
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
