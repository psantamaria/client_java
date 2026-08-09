# Prometheus Java Client Benchmarks

## Run Information

- **Date:** 2026-08-09T04:44:25Z
- **Commit:** [`4b69f40`](https://github.com/psantamaria/client_java/commit/4b69f40bd4e616d69468ce99dc4323162287a577)
- **JDK:** 25.0.2 (OpenJDK 64-Bit Server VM)
- **Benchmark config:** 3 fork(s), 3 warmup, 5 measurement, 4 threads
- **Hardware:** AMD EPYC 7763 64-Core Processor, 4 cores, 16 GB RAM
- **OS:** Linux 6.17.0-1020-azure

## Results

### CounterBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusInc | 66.82K | ± 1.93K | ops/s | **fastest** |
| prometheusNoLabelsInc | 58.19K | ± 713.19 | ops/s | 1.1x slower |
| prometheusAdd | 51.60K | ± 415.51 | ops/s | 1.3x slower |
| codahaleIncNoLabels | 46.59K | ± 5.87K | ops/s | 1.4x slower |
| simpleclientInc | 6.65K | ± 247.70 | ops/s | 10x slower |
| simpleclientNoLabelsInc | 6.62K | ± 132.49 | ops/s | 10x slower |
| simpleclientAdd | 6.43K | ± 31.63 | ops/s | 10x slower |
| openTelemetryAdd | 1.46K | ± 308.63 | ops/s | 46x slower |
| openTelemetryInc | 1.42K | ± 193.36 | ops/s | 47x slower |
| openTelemetryIncNoLabels | 1.31K | ± 147.19 | ops/s | 51x slower |

### HistogramBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusClassic | 5.83K | ± 1.16K | ops/s | **fastest** |
| simpleclient | 4.24K | ± 418.77 | ops/s | 1.4x slower |
| prometheusNative | 2.88K | ± 262.52 | ops/s | 2.0x slower |
| openTelemetryClassic | 687.06 | ± 33.34 | ops/s | 8.5x slower |
| openTelemetryExponential | 546.68 | ± 24.76 | ops/s | 11x slower |

### TextFormatUtilBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusWriteToNull | 497.14K | ± 5.54K | ops/s | **fastest** |
| prometheusWriteToByteArray | 490.16K | ± 3.92K | ops/s | 1.0x slower |
| openMetricsWriteToNull | 488.26K | ± 5.66K | ops/s | 1.0x slower |
| openMetricsWriteToByteArray | 473.83K | ± 7.62K | ops/s | 1.0x slower |

### Raw Results

```
Benchmark                                            Mode  Cnt          Score        Error  Units
CounterBenchmark.codahaleIncNoLabels                thrpt   15      46590.644   ± 5873.350  ops/s
CounterBenchmark.openTelemetryAdd                   thrpt   15       1462.484    ± 308.632  ops/s
CounterBenchmark.openTelemetryInc                   thrpt   15       1420.296    ± 193.357  ops/s
CounterBenchmark.openTelemetryIncNoLabels           thrpt   15       1309.663    ± 147.188  ops/s
CounterBenchmark.prometheusAdd                      thrpt   15      51602.947    ± 415.510  ops/s
CounterBenchmark.prometheusInc                      thrpt   15      66816.113   ± 1926.898  ops/s
CounterBenchmark.prometheusNoLabelsInc              thrpt   15      58191.282    ± 713.195  ops/s
CounterBenchmark.simpleclientAdd                    thrpt   15       6429.771     ± 31.633  ops/s
CounterBenchmark.simpleclientInc                    thrpt   15       6646.839    ± 247.698  ops/s
CounterBenchmark.simpleclientNoLabelsInc            thrpt   15       6617.691    ± 132.494  ops/s
HistogramBenchmark.openTelemetryClassic             thrpt   15        687.057     ± 33.345  ops/s
HistogramBenchmark.openTelemetryExponential         thrpt   15        546.681     ± 24.758  ops/s
HistogramBenchmark.prometheusClassic                thrpt   15       5834.914   ± 1161.190  ops/s
HistogramBenchmark.prometheusNative                 thrpt   15       2880.076    ± 262.516  ops/s
HistogramBenchmark.simpleclient                     thrpt   15       4241.351    ± 418.770  ops/s
TextFormatUtilBenchmark.openMetricsWriteToByteArray  thrpt   15     473834.128   ± 7616.165  ops/s
TextFormatUtilBenchmark.openMetricsWriteToNull      thrpt   15     488260.716   ± 5657.469  ops/s
TextFormatUtilBenchmark.prometheusWriteToByteArray  thrpt   15     490163.847   ± 3920.056  ops/s
TextFormatUtilBenchmark.prometheusWriteToNull       thrpt   15     497138.869   ± 5535.573  ops/s
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
