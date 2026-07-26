# Prometheus Java Client Benchmarks

## Run Information

- **Date:** 2026-07-26T06:43:02Z
- **Commit:** [`4b69f40`](https://github.com/psantamaria/client_java/commit/4b69f40bd4e616d69468ce99dc4323162287a577)
- **JDK:** 25.0.2 (OpenJDK 64-Bit Server VM)
- **Benchmark config:** 3 fork(s), 3 warmup, 5 measurement, 4 threads
- **Hardware:** AMD EPYC 7763 64-Core Processor, 4 cores, 16 GB RAM
- **OS:** Linux 6.17.0-1020-azure

## Results

### CounterBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusInc | 65.32K | ± 1.24K | ops/s | **fastest** |
| prometheusNoLabelsInc | 56.92K | ± 359.56 | ops/s | 1.1x slower |
| prometheusAdd | 51.43K | ± 155.43 | ops/s | 1.3x slower |
| codahaleIncNoLabels | 47.83K | ± 1.31K | ops/s | 1.4x slower |
| simpleclientInc | 6.68K | ± 40.03 | ops/s | 9.8x slower |
| simpleclientNoLabelsInc | 6.51K | ± 92.83 | ops/s | 10x slower |
| simpleclientAdd | 6.03K | ± 63.06 | ops/s | 11x slower |
| openTelemetryIncNoLabels | 1.48K | ± 78.34 | ops/s | 44x slower |
| openTelemetryInc | 1.27K | ± 59.96 | ops/s | 51x slower |
| openTelemetryAdd | 1.25K | ± 29.96 | ops/s | 52x slower |

### HistogramBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusClassic | 6.10K | ± 1.13K | ops/s | **fastest** |
| simpleclient | 4.46K | ± 53.99 | ops/s | 1.4x slower |
| prometheusNative | 2.87K | ± 230.89 | ops/s | 2.1x slower |
| openTelemetryClassic | 687.96 | ± 16.12 | ops/s | 8.9x slower |
| openTelemetryExponential | 554.48 | ± 17.22 | ops/s | 11x slower |

### TextFormatUtilBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusWriteToNull | 491.64K | ± 5.37K | ops/s | **fastest** |
| prometheusWriteToByteArray | 487.30K | ± 2.60K | ops/s | 1.0x slower |
| openMetricsWriteToNull | 484.14K | ± 1.47K | ops/s | 1.0x slower |
| openMetricsWriteToByteArray | 471.51K | ± 4.21K | ops/s | 1.0x slower |

### Raw Results

```
Benchmark                                            Mode  Cnt          Score        Error  Units
CounterBenchmark.codahaleIncNoLabels                thrpt   15      47830.549   ± 1309.857  ops/s
CounterBenchmark.openTelemetryAdd                   thrpt   15       1250.011     ± 29.956  ops/s
CounterBenchmark.openTelemetryInc                   thrpt   15       1270.451     ± 59.957  ops/s
CounterBenchmark.openTelemetryIncNoLabels           thrpt   15       1479.238     ± 78.339  ops/s
CounterBenchmark.prometheusAdd                      thrpt   15      51433.099    ± 155.427  ops/s
CounterBenchmark.prometheusInc                      thrpt   15      65316.366   ± 1237.727  ops/s
CounterBenchmark.prometheusNoLabelsInc              thrpt   15      56921.443    ± 359.560  ops/s
CounterBenchmark.simpleclientAdd                    thrpt   15       6029.000     ± 63.062  ops/s
CounterBenchmark.simpleclientInc                    thrpt   15       6675.028     ± 40.030  ops/s
CounterBenchmark.simpleclientNoLabelsInc            thrpt   15       6514.388     ± 92.829  ops/s
HistogramBenchmark.openTelemetryClassic             thrpt   15        687.957     ± 16.124  ops/s
HistogramBenchmark.openTelemetryExponential         thrpt   15        554.481     ± 17.225  ops/s
HistogramBenchmark.prometheusClassic                thrpt   15       6100.794   ± 1129.581  ops/s
HistogramBenchmark.prometheusNative                 thrpt   15       2867.631    ± 230.893  ops/s
HistogramBenchmark.simpleclient                     thrpt   15       4464.288     ± 53.991  ops/s
TextFormatUtilBenchmark.openMetricsWriteToByteArray  thrpt   15     471514.667   ± 4214.093  ops/s
TextFormatUtilBenchmark.openMetricsWriteToNull      thrpt   15     484136.243   ± 1466.681  ops/s
TextFormatUtilBenchmark.prometheusWriteToByteArray  thrpt   15     487301.182   ± 2598.759  ops/s
TextFormatUtilBenchmark.prometheusWriteToNull       thrpt   15     491637.069   ± 5372.059  ops/s
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
