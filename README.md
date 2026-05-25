# Prometheus Java Client Benchmarks

## Run Information

- **Date:** 2026-05-25T07:39:03Z
- **Commit:** [`4b69f40`](https://github.com/psantamaria/client_java/commit/4b69f40bd4e616d69468ce99dc4323162287a577)
- **JDK:** 25.0.2 (OpenJDK 64-Bit Server VM)
- **Benchmark config:** 3 fork(s), 3 warmup, 5 measurement, 4 threads
- **Hardware:** AMD EPYC 7763 64-Core Processor, 4 cores, 16 GB RAM
- **OS:** Linux 6.17.0-1013-azure

## Results

### CounterBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusInc | 63.44K | ± 319.01 | ops/s | **fastest** |
| prometheusNoLabelsInc | 57.21K | ± 216.91 | ops/s | 1.1x slower |
| prometheusAdd | 51.21K | ± 392.80 | ops/s | 1.2x slower |
| codahaleIncNoLabels | 50.11K | ± 155.65 | ops/s | 1.3x slower |
| simpleclientInc | 6.65K | ± 50.21 | ops/s | 9.5x slower |
| simpleclientNoLabelsInc | 6.52K | ± 146.31 | ops/s | 9.7x slower |
| simpleclientAdd | 6.31K | ± 210.51 | ops/s | 10x slower |
| openTelemetryAdd | 1.47K | ± 200.39 | ops/s | 43x slower |
| openTelemetryIncNoLabels | 1.32K | ± 197.72 | ops/s | 48x slower |
| openTelemetryInc | 1.22K | ± 45.68 | ops/s | 52x slower |

### HistogramBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusClassic | 5.33K | ± 1.49K | ops/s | **fastest** |
| simpleclient | 4.44K | ± 48.24 | ops/s | 1.2x slower |
| prometheusNative | 3.17K | ± 115.73 | ops/s | 1.7x slower |
| openTelemetryClassic | 739.31 | ± 17.92 | ops/s | 7.2x slower |
| openTelemetryExponential | 571.57 | ± 7.70 | ops/s | 9.3x slower |

### TextFormatUtilBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusWriteToNull | 481.05K | ± 3.34K | ops/s | **fastest** |
| prometheusWriteToByteArray | 476.41K | ± 2.90K | ops/s | 1.0x slower |
| openMetricsWriteToNull | 469.92K | ± 7.02K | ops/s | 1.0x slower |
| openMetricsWriteToByteArray | 453.98K | ± 5.42K | ops/s | 1.1x slower |

### Raw Results

```
Benchmark                                            Mode  Cnt          Score        Error  Units
CounterBenchmark.codahaleIncNoLabels                thrpt   15      50113.375    ± 155.654  ops/s
CounterBenchmark.openTelemetryAdd                   thrpt   15       1468.470    ± 200.389  ops/s
CounterBenchmark.openTelemetryInc                   thrpt   15       1224.773     ± 45.676  ops/s
CounterBenchmark.openTelemetryIncNoLabels           thrpt   15       1324.001    ± 197.716  ops/s
CounterBenchmark.prometheusAdd                      thrpt   15      51208.999    ± 392.804  ops/s
CounterBenchmark.prometheusInc                      thrpt   15      63440.049    ± 319.009  ops/s
CounterBenchmark.prometheusNoLabelsInc              thrpt   15      57205.574    ± 216.914  ops/s
CounterBenchmark.simpleclientAdd                    thrpt   15       6312.289    ± 210.507  ops/s
CounterBenchmark.simpleclientInc                    thrpt   15       6654.825     ± 50.209  ops/s
CounterBenchmark.simpleclientNoLabelsInc            thrpt   15       6524.950    ± 146.310  ops/s
HistogramBenchmark.openTelemetryClassic             thrpt   15        739.311     ± 17.924  ops/s
HistogramBenchmark.openTelemetryExponential         thrpt   15        571.572      ± 7.700  ops/s
HistogramBenchmark.prometheusClassic                thrpt   15       5334.333   ± 1485.638  ops/s
HistogramBenchmark.prometheusNative                 thrpt   15       3168.674    ± 115.728  ops/s
HistogramBenchmark.simpleclient                     thrpt   15       4436.612     ± 48.240  ops/s
TextFormatUtilBenchmark.openMetricsWriteToByteArray  thrpt   15     453979.397   ± 5421.438  ops/s
TextFormatUtilBenchmark.openMetricsWriteToNull      thrpt   15     469918.158   ± 7024.945  ops/s
TextFormatUtilBenchmark.prometheusWriteToByteArray  thrpt   15     476406.852   ± 2897.879  ops/s
TextFormatUtilBenchmark.prometheusWriteToNull       thrpt   15     481052.225   ± 3340.031  ops/s
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
