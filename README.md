# Prometheus Java Client Benchmarks

## Run Information

- **Date:** 2026-05-31T07:29:56Z
- **Commit:** [`4b69f40`](https://github.com/psantamaria/client_java/commit/4b69f40bd4e616d69468ce99dc4323162287a577)
- **JDK:** 25.0.2 (OpenJDK 64-Bit Server VM)
- **Benchmark config:** 3 fork(s), 3 warmup, 5 measurement, 4 threads
- **Hardware:** Intel(R) Xeon(R) Platinum 8370C CPU @ 2.80GHz, 4 cores, 16 GB RAM
- **OS:** Linux 6.17.0-1015-azure

## Results

### CounterBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusInc | 31.41K | ± 47.32 | ops/s | **fastest** |
| prometheusNoLabelsInc | 30.43K | ± 825.62 | ops/s | 1.0x slower |
| codahaleIncNoLabels | 29.00K | ± 728.30 | ops/s | 1.1x slower |
| prometheusAdd | 27.53K | ± 1.30K | ops/s | 1.1x slower |
| simpleclientNoLabelsInc | 6.92K | ± 64.99 | ops/s | 4.5x slower |
| simpleclientInc | 6.89K | ± 147.02 | ops/s | 4.6x slower |
| simpleclientAdd | 6.55K | ± 294.04 | ops/s | 4.8x slower |
| openTelemetryIncNoLabels | 1.33K | ± 116.23 | ops/s | 24x slower |
| openTelemetryAdd | 1.32K | ± 79.02 | ops/s | 24x slower |
| openTelemetryInc | 1.28K | ± 69.82 | ops/s | 25x slower |

### HistogramBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| simpleclient | 4.50K | ± 9.87 | ops/s | **fastest** |
| prometheusClassic | 3.22K | ± 260.36 | ops/s | 1.4x slower |
| prometheusNative | 2.23K | ± 311.45 | ops/s | 2.0x slower |
| openTelemetryClassic | 493.21 | ± 27.00 | ops/s | 9.1x slower |
| openTelemetryExponential | 382.09 | ± 16.91 | ops/s | 12x slower |

### TextFormatUtilBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusWriteToByteArray | 260.57K | ± 1.76K | ops/s | **fastest** |
| prometheusWriteToNull | 260.40K | ± 1.98K | ops/s | 1.0x slower |
| openMetricsWriteToNull | 248.10K | ± 1.78K | ops/s | 1.1x slower |
| openMetricsWriteToByteArray | 246.72K | ± 588.05 | ops/s | 1.1x slower |

### Raw Results

```
Benchmark                                            Mode  Cnt          Score        Error  Units
CounterBenchmark.codahaleIncNoLabels                thrpt   15      28997.942    ± 728.304  ops/s
CounterBenchmark.openTelemetryAdd                   thrpt   15       1323.090     ± 79.020  ops/s
CounterBenchmark.openTelemetryInc                   thrpt   15       1276.690     ± 69.816  ops/s
CounterBenchmark.openTelemetryIncNoLabels           thrpt   15       1332.035    ± 116.230  ops/s
CounterBenchmark.prometheusAdd                      thrpt   15      27527.229   ± 1299.864  ops/s
CounterBenchmark.prometheusInc                      thrpt   15      31412.928     ± 47.317  ops/s
CounterBenchmark.prometheusNoLabelsInc              thrpt   15      30431.334    ± 825.618  ops/s
CounterBenchmark.simpleclientAdd                    thrpt   15       6546.121    ± 294.044  ops/s
CounterBenchmark.simpleclientInc                    thrpt   15       6892.982    ± 147.019  ops/s
CounterBenchmark.simpleclientNoLabelsInc            thrpt   15       6923.012     ± 64.991  ops/s
HistogramBenchmark.openTelemetryClassic             thrpt   15        493.206     ± 26.997  ops/s
HistogramBenchmark.openTelemetryExponential         thrpt   15        382.089     ± 16.907  ops/s
HistogramBenchmark.prometheusClassic                thrpt   15       3217.410    ± 260.360  ops/s
HistogramBenchmark.prometheusNative                 thrpt   15       2226.519    ± 311.453  ops/s
HistogramBenchmark.simpleclient                     thrpt   15       4496.142      ± 9.871  ops/s
TextFormatUtilBenchmark.openMetricsWriteToByteArray  thrpt   15     246723.507    ± 588.051  ops/s
TextFormatUtilBenchmark.openMetricsWriteToNull      thrpt   15     248104.144   ± 1781.754  ops/s
TextFormatUtilBenchmark.prometheusWriteToByteArray  thrpt   15     260573.236   ± 1764.194  ops/s
TextFormatUtilBenchmark.prometheusWriteToNull       thrpt   15     260400.676   ± 1984.049  ops/s
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
