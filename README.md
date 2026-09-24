# Prometheus Java Client Benchmarks

## Run Information

- **Date:** 2026-09-24T08:19:53Z
- **Commit:** [`4b69f40`](https://github.com/psantamaria/client_java/commit/4b69f40bd4e616d69468ce99dc4323162287a577)
- **JDK:** 25.0.2 (OpenJDK 64-Bit Server VM)
- **Benchmark config:** 3 fork(s), 3 warmup, 5 measurement, 4 threads
- **Hardware:** AMD EPYC 7763 64-Core Processor, 4 cores, 16 GB RAM
- **OS:** Linux 6.17.0-1022-azure

## Results

### CounterBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusInc | 65.76K | ± 665.93 | ops/s | **fastest** |
| prometheusNoLabelsInc | 56.40K | ± 680.12 | ops/s | 1.2x slower |
| prometheusAdd | 51.27K | ± 408.23 | ops/s | 1.3x slower |
| codahaleIncNoLabels | 48.84K | ± 2.31K | ops/s | 1.3x slower |
| simpleclientInc | 6.69K | ± 14.47 | ops/s | 9.8x slower |
| simpleclientNoLabelsInc | 6.41K | ± 126.46 | ops/s | 10x slower |
| simpleclientAdd | 6.30K | ± 258.33 | ops/s | 10x slower |
| openTelemetryAdd | 1.52K | ± 271.70 | ops/s | 43x slower |
| openTelemetryInc | 1.47K | ± 250.53 | ops/s | 45x slower |
| openTelemetryIncNoLabels | 1.42K | ± 198.17 | ops/s | 46x slower |

### HistogramBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusClassic | 6.23K | ± 1.61K | ops/s | **fastest** |
| simpleclient | 4.42K | ± 31.59 | ops/s | 1.4x slower |
| prometheusNative | 2.76K | ± 326.80 | ops/s | 2.3x slower |
| openTelemetryClassic | 665.00 | ± 12.82 | ops/s | 9.4x slower |
| openTelemetryExponential | 521.53 | ± 12.51 | ops/s | 12x slower |

### TextFormatUtilBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusWriteToNull | 489.68K | ± 3.11K | ops/s | **fastest** |
| prometheusWriteToByteArray | 480.22K | ± 4.53K | ops/s | 1.0x slower |
| openMetricsWriteToNull | 476.57K | ± 5.66K | ops/s | 1.0x slower |
| openMetricsWriteToByteArray | 470.62K | ± 2.93K | ops/s | 1.0x slower |

### Raw Results

```
Benchmark                                            Mode  Cnt          Score        Error  Units
CounterBenchmark.codahaleIncNoLabels                thrpt   15      48835.824   ± 2308.733  ops/s
CounterBenchmark.openTelemetryAdd                   thrpt   15       1520.288    ± 271.700  ops/s
CounterBenchmark.openTelemetryInc                   thrpt   15       1474.293    ± 250.531  ops/s
CounterBenchmark.openTelemetryIncNoLabels           thrpt   15       1420.024    ± 198.169  ops/s
CounterBenchmark.prometheusAdd                      thrpt   15      51270.974    ± 408.227  ops/s
CounterBenchmark.prometheusInc                      thrpt   15      65760.677    ± 665.933  ops/s
CounterBenchmark.prometheusNoLabelsInc              thrpt   15      56404.821    ± 680.123  ops/s
CounterBenchmark.simpleclientAdd                    thrpt   15       6300.393    ± 258.331  ops/s
CounterBenchmark.simpleclientInc                    thrpt   15       6693.734     ± 14.469  ops/s
CounterBenchmark.simpleclientNoLabelsInc            thrpt   15       6413.319    ± 126.460  ops/s
HistogramBenchmark.openTelemetryClassic             thrpt   15        665.000     ± 12.817  ops/s
HistogramBenchmark.openTelemetryExponential         thrpt   15        521.527     ± 12.510  ops/s
HistogramBenchmark.prometheusClassic                thrpt   15       6231.044   ± 1606.579  ops/s
HistogramBenchmark.prometheusNative                 thrpt   15       2764.848    ± 326.805  ops/s
HistogramBenchmark.simpleclient                     thrpt   15       4423.863     ± 31.589  ops/s
TextFormatUtilBenchmark.openMetricsWriteToByteArray  thrpt   15     470622.373   ± 2927.445  ops/s
TextFormatUtilBenchmark.openMetricsWriteToNull      thrpt   15     476572.338   ± 5662.605  ops/s
TextFormatUtilBenchmark.prometheusWriteToByteArray  thrpt   15     480224.232   ± 4526.428  ops/s
TextFormatUtilBenchmark.prometheusWriteToNull       thrpt   15     489679.413   ± 3107.226  ops/s
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
