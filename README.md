# Prometheus Java Client Benchmarks

## Run Information

- **Date:** 2026-10-02T09:07:08Z
- **Commit:** [`4b69f40`](https://github.com/psantamaria/client_java/commit/4b69f40bd4e616d69468ce99dc4323162287a577)
- **JDK:** 25.0.2 (OpenJDK 64-Bit Server VM)
- **Benchmark config:** 3 fork(s), 3 warmup, 5 measurement, 4 threads
- **Hardware:** AMD EPYC 7763 64-Core Processor, 4 cores, 16 GB RAM
- **OS:** Linux 6.17.0-1022-azure

## Results

### CounterBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusInc | 65.12K | ± 1.13K | ops/s | **fastest** |
| prometheusNoLabelsInc | 55.11K | ± 484.91 | ops/s | 1.2x slower |
| prometheusAdd | 48.53K | ± 3.77K | ops/s | 1.3x slower |
| codahaleIncNoLabels | 47.77K | ± 1.16K | ops/s | 1.4x slower |
| simpleclientInc | 6.53K | ± 157.11 | ops/s | 10.0x slower |
| simpleclientNoLabelsInc | 6.52K | ± 106.95 | ops/s | 10.0x slower |
| simpleclientAdd | 5.93K | ± 116.29 | ops/s | 11x slower |
| openTelemetryIncNoLabels | 1.42K | ± 172.59 | ops/s | 46x slower |
| openTelemetryAdd | 1.40K | ± 196.78 | ops/s | 47x slower |
| openTelemetryInc | 1.39K | ± 164.56 | ops/s | 47x slower |

### HistogramBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusClassic | 5.78K | ± 1.02K | ops/s | **fastest** |
| simpleclient | 4.45K | ± 50.46 | ops/s | 1.3x slower |
| prometheusNative | 2.95K | ± 309.34 | ops/s | 2.0x slower |
| openTelemetryClassic | 665.91 | ± 12.99 | ops/s | 8.7x slower |
| openTelemetryExponential | 553.45 | ± 5.15 | ops/s | 10x slower |

### TextFormatUtilBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusWriteToNull | 478.72K | ± 4.45K | ops/s | **fastest** |
| prometheusWriteToByteArray | 476.66K | ± 4.73K | ops/s | 1.0x slower |
| openMetricsWriteToNull | 468.11K | ± 4.04K | ops/s | 1.0x slower |
| openMetricsWriteToByteArray | 464.97K | ± 4.58K | ops/s | 1.0x slower |

### Raw Results

```
Benchmark                                            Mode  Cnt          Score        Error  Units
CounterBenchmark.codahaleIncNoLabels                thrpt   15      47767.509   ± 1158.042  ops/s
CounterBenchmark.openTelemetryAdd                   thrpt   15       1397.216    ± 196.777  ops/s
CounterBenchmark.openTelemetryInc                   thrpt   15       1393.602    ± 164.560  ops/s
CounterBenchmark.openTelemetryIncNoLabels           thrpt   15       1415.250    ± 172.589  ops/s
CounterBenchmark.prometheusAdd                      thrpt   15      48525.886   ± 3768.222  ops/s
CounterBenchmark.prometheusInc                      thrpt   15      65115.601   ± 1132.739  ops/s
CounterBenchmark.prometheusNoLabelsInc              thrpt   15      55111.397    ± 484.912  ops/s
CounterBenchmark.simpleclientAdd                    thrpt   15       5926.554    ± 116.292  ops/s
CounterBenchmark.simpleclientInc                    thrpt   15       6532.232    ± 157.114  ops/s
CounterBenchmark.simpleclientNoLabelsInc            thrpt   15       6518.025    ± 106.951  ops/s
HistogramBenchmark.openTelemetryClassic             thrpt   15        665.915     ± 12.991  ops/s
HistogramBenchmark.openTelemetryExponential         thrpt   15        553.445      ± 5.153  ops/s
HistogramBenchmark.prometheusClassic                thrpt   15       5778.414   ± 1016.433  ops/s
HistogramBenchmark.prometheusNative                 thrpt   15       2954.467    ± 309.336  ops/s
HistogramBenchmark.simpleclient                     thrpt   15       4448.613     ± 50.463  ops/s
TextFormatUtilBenchmark.openMetricsWriteToByteArray  thrpt   15     464971.857   ± 4582.883  ops/s
TextFormatUtilBenchmark.openMetricsWriteToNull      thrpt   15     468108.037   ± 4039.182  ops/s
TextFormatUtilBenchmark.prometheusWriteToByteArray  thrpt   15     476661.936   ± 4728.505  ops/s
TextFormatUtilBenchmark.prometheusWriteToNull       thrpt   15     478718.568   ± 4453.210  ops/s
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
