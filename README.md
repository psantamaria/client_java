# Prometheus Java Client Benchmarks

## Run Information

- **Date:** 2026-05-28T07:23:30Z
- **Commit:** [`4b69f40`](https://github.com/psantamaria/client_java/commit/4b69f40bd4e616d69468ce99dc4323162287a577)
- **JDK:** 25.0.2 (OpenJDK 64-Bit Server VM)
- **Benchmark config:** 3 fork(s), 3 warmup, 5 measurement, 4 threads
- **Hardware:** AMD EPYC 9V74 80-Core Processor, 4 cores, 16 GB RAM
- **OS:** Linux 6.17.0-1013-azure

## Results

### CounterBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusInc | 58.16K | ± 3.85K | ops/s | **fastest** |
| prometheusNoLabelsInc | 51.89K | ± 825.96 | ops/s | 1.1x slower |
| prometheusAdd | 48.83K | ± 896.95 | ops/s | 1.2x slower |
| codahaleIncNoLabels | 43.09K | ± 1.89K | ops/s | 1.3x slower |
| simpleclientInc | 6.22K | ± 119.13 | ops/s | 9.4x slower |
| simpleclientAdd | 6.05K | ± 171.16 | ops/s | 9.6x slower |
| simpleclientNoLabelsInc | 5.98K | ± 213.39 | ops/s | 9.7x slower |
| openTelemetryIncNoLabels | 1.36K | ± 72.59 | ops/s | 43x slower |
| openTelemetryInc | 1.30K | ± 112.82 | ops/s | 45x slower |
| openTelemetryAdd | 1.28K | ± 41.07 | ops/s | 46x slower |

### HistogramBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| simpleclient | 4.34K | ± 55.78 | ops/s | **fastest** |
| prometheusClassic | 4.34K | ± 580.15 | ops/s | 1.0x slower |
| prometheusNative | 2.98K | ± 263.53 | ops/s | 1.5x slower |
| openTelemetryClassic | 618.90 | ± 36.22 | ops/s | 7.0x slower |
| openTelemetryExponential | 513.27 | ± 5.80 | ops/s | 8.5x slower |

### TextFormatUtilBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusWriteToNull | 555.47K | ± 6.06K | ops/s | **fastest** |
| prometheusWriteToByteArray | 550.89K | ± 4.05K | ops/s | 1.0x slower |
| openMetricsWriteToNull | 531.22K | ± 7.66K | ops/s | 1.0x slower |
| openMetricsWriteToByteArray | 522.72K | ± 6.53K | ops/s | 1.1x slower |

### Raw Results

```
Benchmark                                            Mode  Cnt          Score        Error  Units
CounterBenchmark.codahaleIncNoLabels                thrpt   15      43094.076   ± 1891.868  ops/s
CounterBenchmark.openTelemetryAdd                   thrpt   15       1277.601     ± 41.073  ops/s
CounterBenchmark.openTelemetryInc                   thrpt   15       1304.264    ± 112.821  ops/s
CounterBenchmark.openTelemetryIncNoLabels           thrpt   15       1364.202     ± 72.588  ops/s
CounterBenchmark.prometheusAdd                      thrpt   15      48834.925    ± 896.946  ops/s
CounterBenchmark.prometheusInc                      thrpt   15      58160.034   ± 3847.530  ops/s
CounterBenchmark.prometheusNoLabelsInc              thrpt   15      51888.573    ± 825.959  ops/s
CounterBenchmark.simpleclientAdd                    thrpt   15       6049.312    ± 171.160  ops/s
CounterBenchmark.simpleclientInc                    thrpt   15       6217.047    ± 119.129  ops/s
CounterBenchmark.simpleclientNoLabelsInc            thrpt   15       5982.524    ± 213.386  ops/s
HistogramBenchmark.openTelemetryClassic             thrpt   15        618.899     ± 36.219  ops/s
HistogramBenchmark.openTelemetryExponential         thrpt   15        513.271      ± 5.804  ops/s
HistogramBenchmark.prometheusClassic                thrpt   15       4337.671    ± 580.148  ops/s
HistogramBenchmark.prometheusNative                 thrpt   15       2979.624    ± 263.535  ops/s
HistogramBenchmark.simpleclient                     thrpt   15       4342.441     ± 55.779  ops/s
TextFormatUtilBenchmark.openMetricsWriteToByteArray  thrpt   15     522717.832   ± 6530.291  ops/s
TextFormatUtilBenchmark.openMetricsWriteToNull      thrpt   15     531219.813   ± 7663.074  ops/s
TextFormatUtilBenchmark.prometheusWriteToByteArray  thrpt   15     550892.970   ± 4052.548  ops/s
TextFormatUtilBenchmark.prometheusWriteToNull       thrpt   15     555469.767   ± 6056.278  ops/s
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
