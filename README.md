# Prometheus Java Client Benchmarks

## Run Information

- **Date:** 2026-06-01T08:06:41Z
- **Commit:** [`4b69f40`](https://github.com/psantamaria/client_java/commit/4b69f40bd4e616d69468ce99dc4323162287a577)
- **JDK:** 25.0.2 (OpenJDK 64-Bit Server VM)
- **Benchmark config:** 3 fork(s), 3 warmup, 5 measurement, 4 threads
- **Hardware:** AMD EPYC 9V74 80-Core Processor, 4 cores, 16 GB RAM
- **OS:** Linux 6.17.0-1015-azure

## Results

### CounterBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusInc | 60.06K | ± 1.07K | ops/s | **fastest** |
| prometheusNoLabelsInc | 51.36K | ± 1.03K | ops/s | 1.2x slower |
| prometheusAdd | 48.38K | ± 315.45 | ops/s | 1.2x slower |
| codahaleIncNoLabels | 44.29K | ± 140.76 | ops/s | 1.4x slower |
| simpleclientInc | 6.23K | ± 155.32 | ops/s | 9.6x slower |
| simpleclientNoLabelsInc | 6.00K | ± 178.94 | ops/s | 10x slower |
| simpleclientAdd | 5.93K | ± 197.57 | ops/s | 10x slower |
| openTelemetryIncNoLabels | 1.41K | ± 124.75 | ops/s | 43x slower |
| openTelemetryInc | 1.37K | ± 86.88 | ops/s | 44x slower |
| openTelemetryAdd | 1.34K | ± 9.13 | ops/s | 45x slower |

### HistogramBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusClassic | 6.47K | ± 1.44K | ops/s | **fastest** |
| simpleclient | 4.57K | ± 94.18 | ops/s | 1.4x slower |
| prometheusNative | 3.02K | ± 226.01 | ops/s | 2.1x slower |
| openTelemetryClassic | 604.11 | ± 27.60 | ops/s | 11x slower |
| openTelemetryExponential | 544.99 | ± 20.31 | ops/s | 12x slower |

### TextFormatUtilBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusWriteToNull | 548.97K | ± 3.86K | ops/s | **fastest** |
| prometheusWriteToByteArray | 547.29K | ± 2.23K | ops/s | 1.0x slower |
| openMetricsWriteToNull | 541.83K | ± 2.42K | ops/s | 1.0x slower |
| openMetricsWriteToByteArray | 515.05K | ± 19.43K | ops/s | 1.1x slower |

### Raw Results

```
Benchmark                                            Mode  Cnt          Score        Error  Units
CounterBenchmark.codahaleIncNoLabels                thrpt   15      44287.811    ± 140.755  ops/s
CounterBenchmark.openTelemetryAdd                   thrpt   15       1344.481      ± 9.131  ops/s
CounterBenchmark.openTelemetryInc                   thrpt   15       1366.758     ± 86.881  ops/s
CounterBenchmark.openTelemetryIncNoLabels           thrpt   15       1408.149    ± 124.749  ops/s
CounterBenchmark.prometheusAdd                      thrpt   15      48384.399    ± 315.452  ops/s
CounterBenchmark.prometheusInc                      thrpt   15      60058.768   ± 1074.064  ops/s
CounterBenchmark.prometheusNoLabelsInc              thrpt   15      51360.810   ± 1027.597  ops/s
CounterBenchmark.simpleclientAdd                    thrpt   15       5926.568    ± 197.569  ops/s
CounterBenchmark.simpleclientInc                    thrpt   15       6233.448    ± 155.320  ops/s
CounterBenchmark.simpleclientNoLabelsInc            thrpt   15       6000.659    ± 178.938  ops/s
HistogramBenchmark.openTelemetryClassic             thrpt   15        604.111     ± 27.601  ops/s
HistogramBenchmark.openTelemetryExponential         thrpt   15        544.991     ± 20.308  ops/s
HistogramBenchmark.prometheusClassic                thrpt   15       6473.897   ± 1443.147  ops/s
HistogramBenchmark.prometheusNative                 thrpt   15       3023.541    ± 226.014  ops/s
HistogramBenchmark.simpleclient                     thrpt   15       4567.934     ± 94.184  ops/s
TextFormatUtilBenchmark.openMetricsWriteToByteArray  thrpt   15     515046.074  ± 19426.068  ops/s
TextFormatUtilBenchmark.openMetricsWriteToNull      thrpt   15     541834.789   ± 2422.113  ops/s
TextFormatUtilBenchmark.prometheusWriteToByteArray  thrpt   15     547289.167   ± 2226.671  ops/s
TextFormatUtilBenchmark.prometheusWriteToNull       thrpt   15     548965.717   ± 3860.353  ops/s
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
