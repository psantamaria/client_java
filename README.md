# Prometheus Java Client Benchmarks

## Run Information

- **Date:** 2026-07-24T06:32:22Z
- **Commit:** [`4b69f40`](https://github.com/psantamaria/client_java/commit/4b69f40bd4e616d69468ce99dc4323162287a577)
- **JDK:** 25.0.2 (OpenJDK 64-Bit Server VM)
- **Benchmark config:** 3 fork(s), 3 warmup, 5 measurement, 4 threads
- **Hardware:** AMD EPYC 7763 64-Core Processor, 4 cores, 16 GB RAM
- **OS:** Linux 6.17.0-1020-azure

## Results

### CounterBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusInc | 65.07K | ± 1.81K | ops/s | **fastest** |
| prometheusNoLabelsInc | 56.99K | ± 73.90 | ops/s | 1.1x slower |
| prometheusAdd | 50.76K | ± 899.86 | ops/s | 1.3x slower |
| codahaleIncNoLabels | 48.55K | ± 1.28K | ops/s | 1.3x slower |
| simpleclientInc | 6.53K | ± 208.94 | ops/s | 10.0x slower |
| simpleclientNoLabelsInc | 6.50K | ± 189.43 | ops/s | 10x slower |
| simpleclientAdd | 6.34K | ± 206.19 | ops/s | 10x slower |
| openTelemetryAdd | 1.56K | ± 211.06 | ops/s | 42x slower |
| openTelemetryIncNoLabels | 1.37K | ± 155.71 | ops/s | 48x slower |
| openTelemetryInc | 1.33K | ± 178.38 | ops/s | 49x slower |

### HistogramBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusClassic | 4.53K | ± 376.61 | ops/s | **fastest** |
| simpleclient | 4.38K | ± 81.93 | ops/s | 1.0x slower |
| prometheusNative | 2.74K | ± 250.64 | ops/s | 1.7x slower |
| openTelemetryClassic | 705.27 | ± 28.85 | ops/s | 6.4x slower |
| openTelemetryExponential | 586.69 | ± 24.72 | ops/s | 7.7x slower |

### TextFormatUtilBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusWriteToNull | 490.23K | ± 4.88K | ops/s | **fastest** |
| prometheusWriteToByteArray | 485.07K | ± 4.31K | ops/s | 1.0x slower |
| openMetricsWriteToNull | 480.87K | ± 5.90K | ops/s | 1.0x slower |
| openMetricsWriteToByteArray | 473.54K | ± 8.00K | ops/s | 1.0x slower |

### Raw Results

```
Benchmark                                            Mode  Cnt          Score        Error  Units
CounterBenchmark.codahaleIncNoLabels                thrpt   15      48553.817   ± 1278.442  ops/s
CounterBenchmark.openTelemetryAdd                   thrpt   15       1561.051    ± 211.060  ops/s
CounterBenchmark.openTelemetryInc                   thrpt   15       1331.555    ± 178.377  ops/s
CounterBenchmark.openTelemetryIncNoLabels           thrpt   15       1369.229    ± 155.706  ops/s
CounterBenchmark.prometheusAdd                      thrpt   15      50759.568    ± 899.857  ops/s
CounterBenchmark.prometheusInc                      thrpt   15      65067.137   ± 1806.749  ops/s
CounterBenchmark.prometheusNoLabelsInc              thrpt   15      56994.709     ± 73.899  ops/s
CounterBenchmark.simpleclientAdd                    thrpt   15       6336.892    ± 206.189  ops/s
CounterBenchmark.simpleclientInc                    thrpt   15       6530.531    ± 208.938  ops/s
CounterBenchmark.simpleclientNoLabelsInc            thrpt   15       6495.428    ± 189.433  ops/s
HistogramBenchmark.openTelemetryClassic             thrpt   15        705.270     ± 28.854  ops/s
HistogramBenchmark.openTelemetryExponential         thrpt   15        586.695     ± 24.721  ops/s
HistogramBenchmark.prometheusClassic                thrpt   15       4526.437    ± 376.605  ops/s
HistogramBenchmark.prometheusNative                 thrpt   15       2742.228    ± 250.639  ops/s
HistogramBenchmark.simpleclient                     thrpt   15       4379.330     ± 81.926  ops/s
TextFormatUtilBenchmark.openMetricsWriteToByteArray  thrpt   15     473536.574   ± 8003.539  ops/s
TextFormatUtilBenchmark.openMetricsWriteToNull      thrpt   15     480874.556   ± 5896.187  ops/s
TextFormatUtilBenchmark.prometheusWriteToByteArray  thrpt   15     485067.571   ± 4307.881  ops/s
TextFormatUtilBenchmark.prometheusWriteToNull       thrpt   15     490230.486   ± 4881.800  ops/s
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
