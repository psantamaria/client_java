# Prometheus Java Client Benchmarks

## Run Information

- **Date:** 2026-09-05T07:51:55Z
- **Commit:** [`4b69f40`](https://github.com/psantamaria/client_java/commit/4b69f40bd4e616d69468ce99dc4323162287a577)
- **JDK:** 25.0.2 (OpenJDK 64-Bit Server VM)
- **Benchmark config:** 3 fork(s), 3 warmup, 5 measurement, 4 threads
- **Hardware:** AMD EPYC 9V74 80-Core Processor, 4 cores, 16 GB RAM
- **OS:** Linux 6.17.0-1022-azure

## Results

### CounterBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusInc | 59.53K | ± 448.44 | ops/s | **fastest** |
| prometheusNoLabelsInc | 50.60K | ± 168.20 | ops/s | 1.2x slower |
| prometheusAdd | 47.87K | ± 561.99 | ops/s | 1.2x slower |
| codahaleIncNoLabels | 44.74K | ± 654.11 | ops/s | 1.3x slower |
| simpleclientInc | 6.24K | ± 107.09 | ops/s | 9.5x slower |
| simpleclientNoLabelsInc | 5.97K | ± 210.41 | ops/s | 10.0x slower |
| simpleclientAdd | 5.80K | ± 272.64 | ops/s | 10x slower |
| openTelemetryIncNoLabels | 1.47K | ± 118.95 | ops/s | 40x slower |
| openTelemetryInc | 1.41K | ± 84.74 | ops/s | 42x slower |
| openTelemetryAdd | 1.34K | ± 49.30 | ops/s | 44x slower |

### HistogramBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusClassic | 5.71K | ± 1.27K | ops/s | **fastest** |
| simpleclient | 4.31K | ± 166.63 | ops/s | 1.3x slower |
| prometheusNative | 2.87K | ± 229.94 | ops/s | 2.0x slower |
| openTelemetryClassic | 594.24 | ± 7.61 | ops/s | 9.6x slower |
| openTelemetryExponential | 501.15 | ± 29.18 | ops/s | 11x slower |

### TextFormatUtilBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusWriteToNull | 561.74K | ± 4.60K | ops/s | **fastest** |
| prometheusWriteToByteArray | 549.37K | ± 18.00K | ops/s | 1.0x slower |
| openMetricsWriteToNull | 538.80K | ± 1.62K | ops/s | 1.0x slower |
| openMetricsWriteToByteArray | 531.50K | ± 2.80K | ops/s | 1.1x slower |

### Raw Results

```
Benchmark                                            Mode  Cnt          Score        Error  Units
CounterBenchmark.codahaleIncNoLabels                thrpt   15      44739.490    ± 654.109  ops/s
CounterBenchmark.openTelemetryAdd                   thrpt   15       1343.233     ± 49.298  ops/s
CounterBenchmark.openTelemetryInc                   thrpt   15       1414.703     ± 84.740  ops/s
CounterBenchmark.openTelemetryIncNoLabels           thrpt   15       1474.314    ± 118.947  ops/s
CounterBenchmark.prometheusAdd                      thrpt   15      47866.278    ± 561.991  ops/s
CounterBenchmark.prometheusInc                      thrpt   15      59528.768    ± 448.437  ops/s
CounterBenchmark.prometheusNoLabelsInc              thrpt   15      50604.828    ± 168.197  ops/s
CounterBenchmark.simpleclientAdd                    thrpt   15       5795.311    ± 272.638  ops/s
CounterBenchmark.simpleclientInc                    thrpt   15       6239.883    ± 107.093  ops/s
CounterBenchmark.simpleclientNoLabelsInc            thrpt   15       5969.848    ± 210.410  ops/s
HistogramBenchmark.openTelemetryClassic             thrpt   15        594.239      ± 7.613  ops/s
HistogramBenchmark.openTelemetryExponential         thrpt   15        501.146     ± 29.177  ops/s
HistogramBenchmark.prometheusClassic                thrpt   15       5709.535   ± 1266.637  ops/s
HistogramBenchmark.prometheusNative                 thrpt   15       2874.194    ± 229.938  ops/s
HistogramBenchmark.simpleclient                     thrpt   15       4309.044    ± 166.632  ops/s
TextFormatUtilBenchmark.openMetricsWriteToByteArray  thrpt   15     531504.625   ± 2800.785  ops/s
TextFormatUtilBenchmark.openMetricsWriteToNull      thrpt   15     538803.636   ± 1620.306  ops/s
TextFormatUtilBenchmark.prometheusWriteToByteArray  thrpt   15     549366.676  ± 18004.779  ops/s
TextFormatUtilBenchmark.prometheusWriteToNull       thrpt   15     561736.693   ± 4604.620  ops/s
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
