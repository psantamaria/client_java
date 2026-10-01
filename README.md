# Prometheus Java Client Benchmarks

## Run Information

- **Date:** 2026-10-01T09:26:03Z
- **Commit:** [`4b69f40`](https://github.com/psantamaria/client_java/commit/4b69f40bd4e616d69468ce99dc4323162287a577)
- **JDK:** 25.0.2 (OpenJDK 64-Bit Server VM)
- **Benchmark config:** 3 fork(s), 3 warmup, 5 measurement, 4 threads
- **Hardware:** AMD EPYC 7763 64-Core Processor, 4 cores, 16 GB RAM
- **OS:** Linux 6.17.0-1022-azure

## Results

### CounterBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusInc | 65.40K | ± 1.65K | ops/s | **fastest** |
| prometheusNoLabelsInc | 56.88K | ± 278.58 | ops/s | 1.1x slower |
| prometheusAdd | 51.17K | ± 488.77 | ops/s | 1.3x slower |
| codahaleIncNoLabels | 49.30K | ± 1.30K | ops/s | 1.3x slower |
| simpleclientInc | 6.44K | ± 111.40 | ops/s | 10x slower |
| simpleclientNoLabelsInc | 6.39K | ± 181.89 | ops/s | 10x slower |
| simpleclientAdd | 5.96K | ± 215.22 | ops/s | 11x slower |
| openTelemetryAdd | 1.70K | ± 179.07 | ops/s | 38x slower |
| openTelemetryIncNoLabels | 1.23K | ± 61.09 | ops/s | 53x slower |
| openTelemetryInc | 1.19K | ± 32.11 | ops/s | 55x slower |

### HistogramBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusClassic | 5.91K | ± 1.02K | ops/s | **fastest** |
| simpleclient | 4.41K | ± 69.82 | ops/s | 1.3x slower |
| prometheusNative | 2.75K | ± 272.32 | ops/s | 2.1x slower |
| openTelemetryClassic | 660.50 | ± 26.56 | ops/s | 8.9x slower |
| openTelemetryExponential | 549.30 | ± 17.02 | ops/s | 11x slower |

### TextFormatUtilBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusWriteToNull | 494.19K | ± 2.63K | ops/s | **fastest** |
| prometheusWriteToByteArray | 488.51K | ± 3.90K | ops/s | 1.0x slower |
| openMetricsWriteToNull | 486.60K | ± 3.07K | ops/s | 1.0x slower |
| openMetricsWriteToByteArray | 481.92K | ± 5.57K | ops/s | 1.0x slower |

### Raw Results

```
Benchmark                                            Mode  Cnt          Score        Error  Units
CounterBenchmark.codahaleIncNoLabels                thrpt   15      49300.086   ± 1303.686  ops/s
CounterBenchmark.openTelemetryAdd                   thrpt   15       1701.645    ± 179.066  ops/s
CounterBenchmark.openTelemetryInc                   thrpt   15       1188.968     ± 32.107  ops/s
CounterBenchmark.openTelemetryIncNoLabels           thrpt   15       1230.800     ± 61.088  ops/s
CounterBenchmark.prometheusAdd                      thrpt   15      51174.351    ± 488.767  ops/s
CounterBenchmark.prometheusInc                      thrpt   15      65395.091   ± 1652.735  ops/s
CounterBenchmark.prometheusNoLabelsInc              thrpt   15      56883.685    ± 278.579  ops/s
CounterBenchmark.simpleclientAdd                    thrpt   15       5957.593    ± 215.220  ops/s
CounterBenchmark.simpleclientInc                    thrpt   15       6439.062    ± 111.398  ops/s
CounterBenchmark.simpleclientNoLabelsInc            thrpt   15       6388.319    ± 181.889  ops/s
HistogramBenchmark.openTelemetryClassic             thrpt   15        660.502     ± 26.560  ops/s
HistogramBenchmark.openTelemetryExponential         thrpt   15        549.297     ± 17.018  ops/s
HistogramBenchmark.prometheusClassic                thrpt   15       5909.304   ± 1019.038  ops/s
HistogramBenchmark.prometheusNative                 thrpt   15       2752.440    ± 272.323  ops/s
HistogramBenchmark.simpleclient                     thrpt   15       4408.466     ± 69.822  ops/s
TextFormatUtilBenchmark.openMetricsWriteToByteArray  thrpt   15     481917.622   ± 5566.511  ops/s
TextFormatUtilBenchmark.openMetricsWriteToNull      thrpt   15     486602.492   ± 3066.734  ops/s
TextFormatUtilBenchmark.prometheusWriteToByteArray  thrpt   15     488511.544   ± 3903.118  ops/s
TextFormatUtilBenchmark.prometheusWriteToNull       thrpt   15     494191.797   ± 2633.309  ops/s
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
