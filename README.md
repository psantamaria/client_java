# Prometheus Java Client Benchmarks

## Run Information

- **Date:** 2026-09-23T08:26:51Z
- **Commit:** [`4b69f40`](https://github.com/psantamaria/client_java/commit/4b69f40bd4e616d69468ce99dc4323162287a577)
- **JDK:** 25.0.2 (OpenJDK 64-Bit Server VM)
- **Benchmark config:** 3 fork(s), 3 warmup, 5 measurement, 4 threads
- **Hardware:** AMD EPYC 7763 64-Core Processor, 4 cores, 16 GB RAM
- **OS:** Linux 6.17.0-1022-azure

## Results

### CounterBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusInc | 66.19K | ± 517.37 | ops/s | **fastest** |
| prometheusNoLabelsInc | 56.39K | ± 1.09K | ops/s | 1.2x slower |
| prometheusAdd | 51.50K | ± 107.04 | ops/s | 1.3x slower |
| codahaleIncNoLabels | 48.65K | ± 1.42K | ops/s | 1.4x slower |
| simpleclientNoLabelsInc | 6.60K | ± 36.20 | ops/s | 10x slower |
| simpleclientInc | 6.60K | ± 175.37 | ops/s | 10x slower |
| simpleclientAdd | 6.31K | ± 250.44 | ops/s | 10x slower |
| openTelemetryAdd | 1.43K | ± 267.89 | ops/s | 46x slower |
| openTelemetryInc | 1.37K | ± 185.36 | ops/s | 48x slower |
| openTelemetryIncNoLabels | 1.27K | ± 14.10 | ops/s | 52x slower |

### HistogramBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusClassic | 4.96K | ± 1.43K | ops/s | **fastest** |
| simpleclient | 4.44K | ± 52.74 | ops/s | 1.1x slower |
| prometheusNative | 2.76K | ± 325.36 | ops/s | 1.8x slower |
| openTelemetryClassic | 666.91 | ± 12.20 | ops/s | 7.4x slower |
| openTelemetryExponential | 571.34 | ± 20.69 | ops/s | 8.7x slower |

### TextFormatUtilBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusWriteToNull | 489.65K | ± 2.80K | ops/s | **fastest** |
| prometheusWriteToByteArray | 487.81K | ± 2.96K | ops/s | 1.0x slower |
| openMetricsWriteToNull | 485.31K | ± 2.21K | ops/s | 1.0x slower |
| openMetricsWriteToByteArray | 473.34K | ± 1.41K | ops/s | 1.0x slower |

### Raw Results

```
Benchmark                                            Mode  Cnt          Score        Error  Units
CounterBenchmark.codahaleIncNoLabels                thrpt   15      48653.059   ± 1422.020  ops/s
CounterBenchmark.openTelemetryAdd                   thrpt   15       1425.437    ± 267.889  ops/s
CounterBenchmark.openTelemetryInc                   thrpt   15       1374.379    ± 185.356  ops/s
CounterBenchmark.openTelemetryIncNoLabels           thrpt   15       1273.545     ± 14.100  ops/s
CounterBenchmark.prometheusAdd                      thrpt   15      51504.117    ± 107.037  ops/s
CounterBenchmark.prometheusInc                      thrpt   15      66193.589    ± 517.373  ops/s
CounterBenchmark.prometheusNoLabelsInc              thrpt   15      56392.005   ± 1088.561  ops/s
CounterBenchmark.simpleclientAdd                    thrpt   15       6313.862    ± 250.436  ops/s
CounterBenchmark.simpleclientInc                    thrpt   15       6595.235    ± 175.370  ops/s
CounterBenchmark.simpleclientNoLabelsInc            thrpt   15       6597.896     ± 36.200  ops/s
HistogramBenchmark.openTelemetryClassic             thrpt   15        666.913     ± 12.200  ops/s
HistogramBenchmark.openTelemetryExponential         thrpt   15        571.344     ± 20.686  ops/s
HistogramBenchmark.prometheusClassic                thrpt   15       4955.023   ± 1425.938  ops/s
HistogramBenchmark.prometheusNative                 thrpt   15       2756.030    ± 325.357  ops/s
HistogramBenchmark.simpleclient                     thrpt   15       4442.227     ± 52.740  ops/s
TextFormatUtilBenchmark.openMetricsWriteToByteArray  thrpt   15     473339.133   ± 1409.872  ops/s
TextFormatUtilBenchmark.openMetricsWriteToNull      thrpt   15     485314.908   ± 2205.212  ops/s
TextFormatUtilBenchmark.prometheusWriteToByteArray  thrpt   15     487812.197   ± 2959.877  ops/s
TextFormatUtilBenchmark.prometheusWriteToNull       thrpt   15     489648.197   ± 2803.096  ops/s
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
