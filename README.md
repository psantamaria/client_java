# Prometheus Java Client Benchmarks

## Run Information

- **Date:** 2026-07-25T06:26:59Z
- **Commit:** [`4b69f40`](https://github.com/psantamaria/client_java/commit/4b69f40bd4e616d69468ce99dc4323162287a577)
- **JDK:** 25.0.2 (OpenJDK 64-Bit Server VM)
- **Benchmark config:** 3 fork(s), 3 warmup, 5 measurement, 4 threads
- **Hardware:** AMD EPYC 9V74 80-Core Processor, 4 cores, 16 GB RAM
- **OS:** Linux 6.17.0-1020-azure

## Results

### CounterBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusInc | 59.86K | ± 1.17K | ops/s | **fastest** |
| prometheusNoLabelsInc | 50.12K | ± 2.50K | ops/s | 1.2x slower |
| prometheusAdd | 48.34K | ± 1.12K | ops/s | 1.2x slower |
| codahaleIncNoLabels | 42.91K | ± 1.74K | ops/s | 1.4x slower |
| simpleclientInc | 6.37K | ± 5.31 | ops/s | 9.4x slower |
| simpleclientAdd | 6.10K | ± 94.61 | ops/s | 9.8x slower |
| simpleclientNoLabelsInc | 6.10K | ± 271.72 | ops/s | 9.8x slower |
| openTelemetryInc | 1.56K | ± 20.82 | ops/s | 38x slower |
| openTelemetryIncNoLabels | 1.48K | ± 149.80 | ops/s | 40x slower |
| openTelemetryAdd | 1.36K | ± 19.12 | ops/s | 44x slower |

### HistogramBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| simpleclient | 4.38K | ± 47.07 | ops/s | **fastest** |
| prometheusClassic | 4.10K | ± 246.34 | ops/s | 1.1x slower |
| prometheusNative | 3.11K | ± 101.51 | ops/s | 1.4x slower |
| openTelemetryClassic | 627.31 | ± 25.05 | ops/s | 7.0x slower |
| openTelemetryExponential | 528.48 | ± 19.45 | ops/s | 8.3x slower |

### TextFormatUtilBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusWriteToNull | 540.36K | ± 3.13K | ops/s | **fastest** |
| prometheusWriteToByteArray | 528.22K | ± 6.53K | ops/s | 1.0x slower |
| openMetricsWriteToNull | 523.46K | ± 3.49K | ops/s | 1.0x slower |
| openMetricsWriteToByteArray | 509.80K | ± 2.06K | ops/s | 1.1x slower |

### Raw Results

```
Benchmark                                            Mode  Cnt          Score        Error  Units
CounterBenchmark.codahaleIncNoLabels                thrpt   15      42911.257   ± 1739.481  ops/s
CounterBenchmark.openTelemetryAdd                   thrpt   15       1355.809     ± 19.118  ops/s
CounterBenchmark.openTelemetryInc                   thrpt   15       1557.028     ± 20.822  ops/s
CounterBenchmark.openTelemetryIncNoLabels           thrpt   15       1478.228    ± 149.800  ops/s
CounterBenchmark.prometheusAdd                      thrpt   15      48335.422   ± 1122.626  ops/s
CounterBenchmark.prometheusInc                      thrpt   15      59861.040   ± 1171.925  ops/s
CounterBenchmark.prometheusNoLabelsInc              thrpt   15      50118.709   ± 2496.766  ops/s
CounterBenchmark.simpleclientAdd                    thrpt   15       6102.336     ± 94.609  ops/s
CounterBenchmark.simpleclientInc                    thrpt   15       6374.323      ± 5.309  ops/s
CounterBenchmark.simpleclientNoLabelsInc            thrpt   15       6099.025    ± 271.719  ops/s
HistogramBenchmark.openTelemetryClassic             thrpt   15        627.307     ± 25.051  ops/s
HistogramBenchmark.openTelemetryExponential         thrpt   15        528.483     ± 19.446  ops/s
HistogramBenchmark.prometheusClassic                thrpt   15       4098.528    ± 246.344  ops/s
HistogramBenchmark.prometheusNative                 thrpt   15       3105.665    ± 101.509  ops/s
HistogramBenchmark.simpleclient                     thrpt   15       4380.489     ± 47.068  ops/s
TextFormatUtilBenchmark.openMetricsWriteToByteArray  thrpt   15     509799.629   ± 2055.510  ops/s
TextFormatUtilBenchmark.openMetricsWriteToNull      thrpt   15     523457.396   ± 3493.898  ops/s
TextFormatUtilBenchmark.prometheusWriteToByteArray  thrpt   15     528223.160   ± 6526.458  ops/s
TextFormatUtilBenchmark.prometheusWriteToNull       thrpt   15     540359.214   ± 3129.144  ops/s
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
