# Prometheus Java Client Benchmarks

## Run Information

- **Date:** 2026-06-11T08:01:04Z
- **Commit:** [`4b69f40`](https://github.com/psantamaria/client_java/commit/4b69f40bd4e616d69468ce99dc4323162287a577)
- **JDK:** 25.0.2 (OpenJDK 64-Bit Server VM)
- **Benchmark config:** 3 fork(s), 3 warmup, 5 measurement, 4 threads
- **Hardware:** AMD EPYC 9V74 80-Core Processor, 4 cores, 16 GB RAM
- **OS:** Linux 6.17.0-1018-azure

## Results

### CounterBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusInc | 58.90K | ± 3.06K | ops/s | **fastest** |
| prometheusNoLabelsInc | 51.35K | ± 511.87 | ops/s | 1.1x slower |
| prometheusAdd | 49.28K | ± 341.90 | ops/s | 1.2x slower |
| codahaleIncNoLabels | 45.12K | ± 1.22K | ops/s | 1.3x slower |
| simpleclientInc | 6.21K | ± 124.54 | ops/s | 9.5x slower |
| simpleclientNoLabelsInc | 6.13K | ± 147.26 | ops/s | 9.6x slower |
| simpleclientAdd | 6.04K | ± 165.91 | ops/s | 9.8x slower |
| openTelemetryAdd | 1.32K | ± 19.49 | ops/s | 45x slower |
| openTelemetryInc | 1.22K | ± 68.24 | ops/s | 48x slower |
| openTelemetryIncNoLabels | 1.20K | ± 81.74 | ops/s | 49x slower |

### HistogramBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusClassic | 5.19K | ± 1.63K | ops/s | **fastest** |
| simpleclient | 4.54K | ± 43.72 | ops/s | 1.1x slower |
| prometheusNative | 2.93K | ± 197.91 | ops/s | 1.8x slower |
| openTelemetryClassic | 578.66 | ± 15.17 | ops/s | 9.0x slower |
| openTelemetryExponential | 500.00 | ± 7.09 | ops/s | 10x slower |

### TextFormatUtilBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusWriteToNull | 551.85K | ± 6.33K | ops/s | **fastest** |
| prometheusWriteToByteArray | 543.83K | ± 7.44K | ops/s | 1.0x slower |
| openMetricsWriteToNull | 535.93K | ± 3.27K | ops/s | 1.0x slower |
| openMetricsWriteToByteArray | 528.98K | ± 5.19K | ops/s | 1.0x slower |

### Raw Results

```
Benchmark                                            Mode  Cnt          Score        Error  Units
CounterBenchmark.codahaleIncNoLabels                thrpt   15      45119.425   ± 1218.547  ops/s
CounterBenchmark.openTelemetryAdd                   thrpt   15       1323.418     ± 19.486  ops/s
CounterBenchmark.openTelemetryInc                   thrpt   15       1219.099     ± 68.244  ops/s
CounterBenchmark.openTelemetryIncNoLabels           thrpt   15       1204.826     ± 81.741  ops/s
CounterBenchmark.prometheusAdd                      thrpt   15      49276.296    ± 341.903  ops/s
CounterBenchmark.prometheusInc                      thrpt   15      58895.615   ± 3060.048  ops/s
CounterBenchmark.prometheusNoLabelsInc              thrpt   15      51350.493    ± 511.866  ops/s
CounterBenchmark.simpleclientAdd                    thrpt   15       6036.160    ± 165.913  ops/s
CounterBenchmark.simpleclientInc                    thrpt   15       6209.701    ± 124.539  ops/s
CounterBenchmark.simpleclientNoLabelsInc            thrpt   15       6134.271    ± 147.255  ops/s
HistogramBenchmark.openTelemetryClassic             thrpt   15        578.659     ± 15.166  ops/s
HistogramBenchmark.openTelemetryExponential         thrpt   15        499.997      ± 7.093  ops/s
HistogramBenchmark.prometheusClassic                thrpt   15       5191.315   ± 1631.842  ops/s
HistogramBenchmark.prometheusNative                 thrpt   15       2925.723    ± 197.906  ops/s
HistogramBenchmark.simpleclient                     thrpt   15       4537.019     ± 43.719  ops/s
TextFormatUtilBenchmark.openMetricsWriteToByteArray  thrpt   15     528979.320   ± 5190.928  ops/s
TextFormatUtilBenchmark.openMetricsWriteToNull      thrpt   15     535931.315   ± 3269.695  ops/s
TextFormatUtilBenchmark.prometheusWriteToByteArray  thrpt   15     543825.198   ± 7443.534  ops/s
TextFormatUtilBenchmark.prometheusWriteToNull       thrpt   15     551845.838   ± 6331.253  ops/s
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
