# Prometheus Java Client Benchmarks

## Run Information

- **Date:** 2026-08-03T06:53:16Z
- **Commit:** [`4b69f40`](https://github.com/psantamaria/client_java/commit/4b69f40bd4e616d69468ce99dc4323162287a577)
- **JDK:** 25.0.2 (OpenJDK 64-Bit Server VM)
- **Benchmark config:** 3 fork(s), 3 warmup, 5 measurement, 4 threads
- **Hardware:** AMD EPYC 7763 64-Core Processor, 4 cores, 16 GB RAM
- **OS:** Linux 6.17.0-1020-azure

## Results

### CounterBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusInc | 66.36K | ± 537.12 | ops/s | **fastest** |
| prometheusNoLabelsInc | 57.08K | ± 114.56 | ops/s | 1.2x slower |
| prometheusAdd | 50.83K | ± 698.95 | ops/s | 1.3x slower |
| codahaleIncNoLabels | 49.04K | ± 841.93 | ops/s | 1.4x slower |
| simpleclientNoLabelsInc | 6.51K | ± 129.67 | ops/s | 10x slower |
| simpleclientInc | 6.38K | ± 245.90 | ops/s | 10x slower |
| simpleclientAdd | 6.16K | ± 247.96 | ops/s | 11x slower |
| openTelemetryInc | 1.51K | ± 200.38 | ops/s | 44x slower |
| openTelemetryAdd | 1.46K | ± 234.30 | ops/s | 45x slower |
| openTelemetryIncNoLabels | 1.40K | ± 116.77 | ops/s | 48x slower |

### HistogramBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusClassic | 7.10K | ± 134.11 | ops/s | **fastest** |
| simpleclient | 4.47K | ± 45.29 | ops/s | 1.6x slower |
| prometheusNative | 3.04K | ± 253.33 | ops/s | 2.3x slower |
| openTelemetryClassic | 693.81 | ± 20.82 | ops/s | 10x slower |
| openTelemetryExponential | 565.96 | ± 11.63 | ops/s | 13x slower |

### TextFormatUtilBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| openMetricsWriteToNull | 476.75K | ± 10.07K | ops/s | **fastest** |
| prometheusWriteToByteArray | 472.03K | ± 13.12K | ops/s | 1.0x slower |
| openMetricsWriteToByteArray | 467.56K | ± 2.50K | ops/s | 1.0x slower |
| prometheusWriteToNull | 466.89K | ± 2.87K | ops/s | 1.0x slower |

### Raw Results

```
Benchmark                                            Mode  Cnt          Score        Error  Units
CounterBenchmark.codahaleIncNoLabels                thrpt   15      49036.907    ± 841.928  ops/s
CounterBenchmark.openTelemetryAdd                   thrpt   15       1462.811    ± 234.304  ops/s
CounterBenchmark.openTelemetryInc                   thrpt   15       1506.709    ± 200.378  ops/s
CounterBenchmark.openTelemetryIncNoLabels           thrpt   15       1396.674    ± 116.769  ops/s
CounterBenchmark.prometheusAdd                      thrpt   15      50834.301    ± 698.945  ops/s
CounterBenchmark.prometheusInc                      thrpt   15      66361.451    ± 537.119  ops/s
CounterBenchmark.prometheusNoLabelsInc              thrpt   15      57081.780    ± 114.564  ops/s
CounterBenchmark.simpleclientAdd                    thrpt   15       6163.018    ± 247.964  ops/s
CounterBenchmark.simpleclientInc                    thrpt   15       6383.029    ± 245.900  ops/s
CounterBenchmark.simpleclientNoLabelsInc            thrpt   15       6506.654    ± 129.665  ops/s
HistogramBenchmark.openTelemetryClassic             thrpt   15        693.811     ± 20.816  ops/s
HistogramBenchmark.openTelemetryExponential         thrpt   15        565.960     ± 11.632  ops/s
HistogramBenchmark.prometheusClassic                thrpt   15       7099.857    ± 134.114  ops/s
HistogramBenchmark.prometheusNative                 thrpt   15       3035.651    ± 253.326  ops/s
HistogramBenchmark.simpleclient                     thrpt   15       4469.839     ± 45.292  ops/s
TextFormatUtilBenchmark.openMetricsWriteToByteArray  thrpt   15     467557.254   ± 2496.166  ops/s
TextFormatUtilBenchmark.openMetricsWriteToNull      thrpt   15     476748.516  ± 10072.646  ops/s
TextFormatUtilBenchmark.prometheusWriteToByteArray  thrpt   15     472025.702  ± 13118.014  ops/s
TextFormatUtilBenchmark.prometheusWriteToNull       thrpt   15     466887.826   ± 2874.529  ops/s
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
