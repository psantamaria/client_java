# Prometheus Java Client Benchmarks

## Run Information

- **Date:** 2026-08-26T04:15:27Z
- **Commit:** [`4b69f40`](https://github.com/psantamaria/client_java/commit/4b69f40bd4e616d69468ce99dc4323162287a577)
- **JDK:** 25.0.2 (OpenJDK 64-Bit Server VM)
- **Benchmark config:** 3 fork(s), 3 warmup, 5 measurement, 4 threads
- **Hardware:** AMD EPYC 7763 64-Core Processor, 4 cores, 16 GB RAM
- **OS:** Linux 6.17.0-1022-azure

## Results

### CounterBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusInc | 66.31K | ± 589.88 | ops/s | **fastest** |
| prometheusNoLabelsInc | 56.93K | ± 386.87 | ops/s | 1.2x slower |
| prometheusAdd | 51.47K | ± 256.21 | ops/s | 1.3x slower |
| codahaleIncNoLabels | 50.38K | ± 565.01 | ops/s | 1.3x slower |
| simpleclientInc | 6.58K | ± 174.52 | ops/s | 10x slower |
| simpleclientNoLabelsInc | 6.39K | ± 203.11 | ops/s | 10x slower |
| simpleclientAdd | 6.07K | ± 102.86 | ops/s | 11x slower |
| openTelemetryInc | 1.56K | ± 79.74 | ops/s | 43x slower |
| openTelemetryAdd | 1.45K | ± 246.15 | ops/s | 46x slower |
| openTelemetryIncNoLabels | 1.18K | ± 28.36 | ops/s | 56x slower |

### HistogramBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusClassic | 5.94K | ± 1.36K | ops/s | **fastest** |
| simpleclient | 4.40K | ± 38.66 | ops/s | 1.3x slower |
| prometheusNative | 2.83K | ± 380.70 | ops/s | 2.1x slower |
| openTelemetryClassic | 659.68 | ± 14.74 | ops/s | 9.0x slower |
| openTelemetryExponential | 539.45 | ± 17.53 | ops/s | 11x slower |

### TextFormatUtilBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusWriteToNull | 493.65K | ± 980.36 | ops/s | **fastest** |
| prometheusWriteToByteArray | 484.82K | ± 3.66K | ops/s | 1.0x slower |
| openMetricsWriteToNull | 483.75K | ± 3.90K | ops/s | 1.0x slower |
| openMetricsWriteToByteArray | 470.68K | ± 3.30K | ops/s | 1.0x slower |

### Raw Results

```
Benchmark                                            Mode  Cnt          Score        Error  Units
CounterBenchmark.codahaleIncNoLabels                thrpt   15      50376.182    ± 565.008  ops/s
CounterBenchmark.openTelemetryAdd                   thrpt   15       1449.854    ± 246.153  ops/s
CounterBenchmark.openTelemetryInc                   thrpt   15       1556.655     ± 79.737  ops/s
CounterBenchmark.openTelemetryIncNoLabels           thrpt   15       1184.741     ± 28.361  ops/s
CounterBenchmark.prometheusAdd                      thrpt   15      51465.133    ± 256.214  ops/s
CounterBenchmark.prometheusInc                      thrpt   15      66313.289    ± 589.881  ops/s
CounterBenchmark.prometheusNoLabelsInc              thrpt   15      56925.427    ± 386.868  ops/s
CounterBenchmark.simpleclientAdd                    thrpt   15       6073.730    ± 102.860  ops/s
CounterBenchmark.simpleclientInc                    thrpt   15       6582.766    ± 174.521  ops/s
CounterBenchmark.simpleclientNoLabelsInc            thrpt   15       6390.270    ± 203.111  ops/s
HistogramBenchmark.openTelemetryClassic             thrpt   15        659.675     ± 14.737  ops/s
HistogramBenchmark.openTelemetryExponential         thrpt   15        539.452     ± 17.534  ops/s
HistogramBenchmark.prometheusClassic                thrpt   15       5937.339   ± 1359.692  ops/s
HistogramBenchmark.prometheusNative                 thrpt   15       2829.953    ± 380.705  ops/s
HistogramBenchmark.simpleclient                     thrpt   15       4403.053     ± 38.662  ops/s
TextFormatUtilBenchmark.openMetricsWriteToByteArray  thrpt   15     470678.578   ± 3295.540  ops/s
TextFormatUtilBenchmark.openMetricsWriteToNull      thrpt   15     483753.695   ± 3895.789  ops/s
TextFormatUtilBenchmark.prometheusWriteToByteArray  thrpt   15     484820.251   ± 3663.044  ops/s
TextFormatUtilBenchmark.prometheusWriteToNull       thrpt   15     493650.920    ± 980.362  ops/s
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
