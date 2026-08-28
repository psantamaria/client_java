# Prometheus Java Client Benchmarks

## Run Information

- **Date:** 2026-08-28T14:57:13Z
- **Commit:** [`4b69f40`](https://github.com/psantamaria/client_java/commit/4b69f40bd4e616d69468ce99dc4323162287a577)
- **JDK:** 25.0.2 (OpenJDK 64-Bit Server VM)
- **Benchmark config:** 3 fork(s), 3 warmup, 5 measurement, 4 threads
- **Hardware:** AMD EPYC 7763 64-Core Processor, 4 cores, 16 GB RAM
- **OS:** Linux 6.17.0-1022-azure

## Results

### CounterBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusInc | 65.77K | ± 1.88K | ops/s | **fastest** |
| prometheusNoLabelsInc | 56.54K | ± 560.48 | ops/s | 1.2x slower |
| prometheusAdd | 51.14K | ± 554.85 | ops/s | 1.3x slower |
| codahaleIncNoLabels | 49.13K | ± 1.66K | ops/s | 1.3x slower |
| simpleclientInc | 6.66K | ± 51.36 | ops/s | 9.9x slower |
| simpleclientNoLabelsInc | 6.49K | ± 183.31 | ops/s | 10x slower |
| simpleclientAdd | 6.12K | ± 255.54 | ops/s | 11x slower |
| openTelemetryInc | 1.50K | ± 195.59 | ops/s | 44x slower |
| openTelemetryAdd | 1.42K | ± 234.32 | ops/s | 46x slower |
| openTelemetryIncNoLabels | 1.24K | ± 37.94 | ops/s | 53x slower |

### HistogramBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusClassic | 6.30K | ± 1.89K | ops/s | **fastest** |
| simpleclient | 4.43K | ± 59.58 | ops/s | 1.4x slower |
| prometheusNative | 2.99K | ± 386.01 | ops/s | 2.1x slower |
| openTelemetryClassic | 697.71 | ± 22.88 | ops/s | 9.0x slower |
| openTelemetryExponential | 536.30 | ± 14.62 | ops/s | 12x slower |

### TextFormatUtilBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusWriteToByteArray | 478.54K | ± 2.37K | ops/s | **fastest** |
| prometheusWriteToNull | 476.84K | ± 3.42K | ops/s | 1.0x slower |
| openMetricsWriteToNull | 470.92K | ± 4.28K | ops/s | 1.0x slower |
| openMetricsWriteToByteArray | 463.90K | ± 2.78K | ops/s | 1.0x slower |

### Raw Results

```
Benchmark                                            Mode  Cnt          Score        Error  Units
CounterBenchmark.codahaleIncNoLabels                thrpt   15      49127.285   ± 1663.976  ops/s
CounterBenchmark.openTelemetryAdd                   thrpt   15       1420.403    ± 234.324  ops/s
CounterBenchmark.openTelemetryInc                   thrpt   15       1502.369    ± 195.593  ops/s
CounterBenchmark.openTelemetryIncNoLabels           thrpt   15       1238.513     ± 37.936  ops/s
CounterBenchmark.prometheusAdd                      thrpt   15      51142.932    ± 554.847  ops/s
CounterBenchmark.prometheusInc                      thrpt   15      65769.838   ± 1881.502  ops/s
CounterBenchmark.prometheusNoLabelsInc              thrpt   15      56537.858    ± 560.485  ops/s
CounterBenchmark.simpleclientAdd                    thrpt   15       6124.830    ± 255.543  ops/s
CounterBenchmark.simpleclientInc                    thrpt   15       6658.658     ± 51.356  ops/s
CounterBenchmark.simpleclientNoLabelsInc            thrpt   15       6490.344    ± 183.314  ops/s
HistogramBenchmark.openTelemetryClassic             thrpt   15        697.715     ± 22.881  ops/s
HistogramBenchmark.openTelemetryExponential         thrpt   15        536.300     ± 14.616  ops/s
HistogramBenchmark.prometheusClassic                thrpt   15       6300.731   ± 1891.186  ops/s
HistogramBenchmark.prometheusNative                 thrpt   15       2992.712    ± 386.014  ops/s
HistogramBenchmark.simpleclient                     thrpt   15       4426.924     ± 59.578  ops/s
TextFormatUtilBenchmark.openMetricsWriteToByteArray  thrpt   15     463897.766   ± 2781.560  ops/s
TextFormatUtilBenchmark.openMetricsWriteToNull      thrpt   15     470916.083   ± 4277.022  ops/s
TextFormatUtilBenchmark.prometheusWriteToByteArray  thrpt   15     478536.043   ± 2368.053  ops/s
TextFormatUtilBenchmark.prometheusWriteToNull       thrpt   15     476835.522   ± 3423.882  ops/s
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
