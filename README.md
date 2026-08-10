# Prometheus Java Client Benchmarks

## Run Information

- **Date:** 2026-08-10T05:04:05Z
- **Commit:** [`4b69f40`](https://github.com/psantamaria/client_java/commit/4b69f40bd4e616d69468ce99dc4323162287a577)
- **JDK:** 25.0.2 (OpenJDK 64-Bit Server VM)
- **Benchmark config:** 3 fork(s), 3 warmup, 5 measurement, 4 threads
- **Hardware:** AMD EPYC 9V74 80-Core Processor, 4 cores, 16 GB RAM
- **OS:** Linux 6.17.0-1020-azure

## Results

### CounterBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusInc | 58.74K | ± 2.93K | ops/s | **fastest** |
| prometheusNoLabelsInc | 52.49K | ± 351.69 | ops/s | 1.1x slower |
| prometheusAdd | 48.31K | ± 310.37 | ops/s | 1.2x slower |
| codahaleIncNoLabels | 43.92K | ± 124.68 | ops/s | 1.3x slower |
| simpleclientInc | 6.23K | ± 124.86 | ops/s | 9.4x slower |
| simpleclientNoLabelsInc | 6.00K | ± 236.22 | ops/s | 9.8x slower |
| simpleclientAdd | 5.83K | ± 5.69 | ops/s | 10x slower |
| openTelemetryAdd | 1.50K | ± 50.50 | ops/s | 39x slower |
| openTelemetryInc | 1.40K | ± 56.84 | ops/s | 42x slower |
| openTelemetryIncNoLabels | 1.36K | ± 21.92 | ops/s | 43x slower |

### HistogramBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusClassic | 5.93K | ± 1.52K | ops/s | **fastest** |
| simpleclient | 4.26K | ± 222.69 | ops/s | 1.4x slower |
| prometheusNative | 3.16K | ± 179.77 | ops/s | 1.9x slower |
| openTelemetryClassic | 612.81 | ± 10.13 | ops/s | 9.7x slower |
| openTelemetryExponential | 534.78 | ± 14.21 | ops/s | 11x slower |

### TextFormatUtilBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusWriteToNull | 548.28K | ± 4.09K | ops/s | **fastest** |
| prometheusWriteToByteArray | 543.80K | ± 2.36K | ops/s | 1.0x slower |
| openMetricsWriteToNull | 533.96K | ± 6.08K | ops/s | 1.0x slower |
| openMetricsWriteToByteArray | 523.71K | ± 3.57K | ops/s | 1.0x slower |

### Raw Results

```
Benchmark                                            Mode  Cnt          Score        Error  Units
CounterBenchmark.codahaleIncNoLabels                thrpt   15      43922.748    ± 124.677  ops/s
CounterBenchmark.openTelemetryAdd                   thrpt   15       1495.466     ± 50.502  ops/s
CounterBenchmark.openTelemetryInc                   thrpt   15       1404.085     ± 56.836  ops/s
CounterBenchmark.openTelemetryIncNoLabels           thrpt   15       1361.554     ± 21.917  ops/s
CounterBenchmark.prometheusAdd                      thrpt   15      48312.839    ± 310.368  ops/s
CounterBenchmark.prometheusInc                      thrpt   15      58743.950   ± 2932.820  ops/s
CounterBenchmark.prometheusNoLabelsInc              thrpt   15      52485.209    ± 351.687  ops/s
CounterBenchmark.simpleclientAdd                    thrpt   15       5827.365      ± 5.687  ops/s
CounterBenchmark.simpleclientInc                    thrpt   15       6226.564    ± 124.865  ops/s
CounterBenchmark.simpleclientNoLabelsInc            thrpt   15       5995.332    ± 236.221  ops/s
HistogramBenchmark.openTelemetryClassic             thrpt   15        612.813     ± 10.131  ops/s
HistogramBenchmark.openTelemetryExponential         thrpt   15        534.781     ± 14.206  ops/s
HistogramBenchmark.prometheusClassic                thrpt   15       5934.369   ± 1523.094  ops/s
HistogramBenchmark.prometheusNative                 thrpt   15       3156.265    ± 179.770  ops/s
HistogramBenchmark.simpleclient                     thrpt   15       4256.698    ± 222.688  ops/s
TextFormatUtilBenchmark.openMetricsWriteToByteArray  thrpt   15     523709.988   ± 3571.929  ops/s
TextFormatUtilBenchmark.openMetricsWriteToNull      thrpt   15     533960.913   ± 6075.818  ops/s
TextFormatUtilBenchmark.prometheusWriteToByteArray  thrpt   15     543800.273   ± 2362.525  ops/s
TextFormatUtilBenchmark.prometheusWriteToNull       thrpt   15     548282.661   ± 4093.003  ops/s
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
