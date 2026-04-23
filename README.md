# Prometheus Java Client Benchmarks

## Run Information

- **Date:** 2026-04-23T06:04:20Z
- **Commit:** [`4b69f40`](https://github.com/psantamaria/client_java/commit/4b69f40bd4e616d69468ce99dc4323162287a577)
- **JDK:** 25.0.2 (OpenJDK 64-Bit Server VM)
- **Benchmark config:** 3 fork(s), 3 warmup, 5 measurement, 4 threads
- **Hardware:** AMD EPYC 7763 64-Core Processor, 4 cores, 16 GB RAM
- **OS:** Linux 6.17.0-1011-azure

## Results

### CounterBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusInc | 59.27K | ± 5.66K | ops/s | **fastest** |
| prometheusNoLabelsInc | 57.15K | ± 126.94 | ops/s | 1.0x slower |
| codahaleIncNoLabels | 49.40K | ± 1.05K | ops/s | 1.2x slower |
| prometheusAdd | 47.88K | ± 2.63K | ops/s | 1.2x slower |
| simpleclientInc | 6.69K | ± 14.28 | ops/s | 8.9x slower |
| simpleclientNoLabelsInc | 6.49K | ± 181.99 | ops/s | 9.1x slower |
| simpleclientAdd | 6.30K | ± 201.65 | ops/s | 9.4x slower |
| openTelemetryIncNoLabels | 1.38K | ± 173.40 | ops/s | 43x slower |
| openTelemetryInc | 1.37K | ± 245.67 | ops/s | 43x slower |
| openTelemetryAdd | 1.28K | ± 87.21 | ops/s | 46x slower |

### HistogramBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusClassic | 5.05K | ± 909.89 | ops/s | **fastest** |
| simpleclient | 4.42K | ± 34.33 | ops/s | 1.1x slower |
| prometheusNative | 3.24K | ± 58.03 | ops/s | 1.6x slower |
| openTelemetryClassic | 711.26 | ± 18.97 | ops/s | 7.1x slower |
| openTelemetryExponential | 558.98 | ± 32.35 | ops/s | 9.0x slower |

### TextFormatUtilBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusWriteToNull | 486.21K | ± 1.49K | ops/s | **fastest** |
| openMetricsWriteToNull | 473.69K | ± 5.35K | ops/s | 1.0x slower |
| prometheusWriteToByteArray | 472.69K | ± 2.02K | ops/s | 1.0x slower |
| openMetricsWriteToByteArray | 464.21K | ± 7.58K | ops/s | 1.0x slower |

### Raw Results

```
Benchmark                                            Mode  Cnt          Score        Error  Units
CounterBenchmark.codahaleIncNoLabels                thrpt   15      49395.451   ± 1047.816  ops/s
CounterBenchmark.openTelemetryAdd                   thrpt   15       1275.430     ± 87.212  ops/s
CounterBenchmark.openTelemetryInc                   thrpt   15       1367.336    ± 245.674  ops/s
CounterBenchmark.openTelemetryIncNoLabels           thrpt   15       1375.696    ± 173.401  ops/s
CounterBenchmark.prometheusAdd                      thrpt   15      47882.056   ± 2629.186  ops/s
CounterBenchmark.prometheusInc                      thrpt   15      59269.103   ± 5658.739  ops/s
CounterBenchmark.prometheusNoLabelsInc              thrpt   15      57145.200    ± 126.939  ops/s
CounterBenchmark.simpleclientAdd                    thrpt   15       6296.360    ± 201.645  ops/s
CounterBenchmark.simpleclientInc                    thrpt   15       6694.212     ± 14.284  ops/s
CounterBenchmark.simpleclientNoLabelsInc            thrpt   15       6489.780    ± 181.991  ops/s
HistogramBenchmark.openTelemetryClassic             thrpt   15        711.262     ± 18.975  ops/s
HistogramBenchmark.openTelemetryExponential         thrpt   15        558.976     ± 32.347  ops/s
HistogramBenchmark.prometheusClassic                thrpt   15       5048.293    ± 909.894  ops/s
HistogramBenchmark.prometheusNative                 thrpt   15       3236.042     ± 58.030  ops/s
HistogramBenchmark.simpleclient                     thrpt   15       4420.337     ± 34.334  ops/s
TextFormatUtilBenchmark.openMetricsWriteToByteArray  thrpt   15     464214.132   ± 7579.228  ops/s
TextFormatUtilBenchmark.openMetricsWriteToNull      thrpt   15     473693.280   ± 5345.134  ops/s
TextFormatUtilBenchmark.prometheusWriteToByteArray  thrpt   15     472691.381   ± 2020.676  ops/s
TextFormatUtilBenchmark.prometheusWriteToNull       thrpt   15     486211.060   ± 1490.587  ops/s
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
