# Prometheus Java Client Benchmarks

## Run Information

- **Date:** 2026-08-23T04:13:07Z
- **Commit:** [`4b69f40`](https://github.com/psantamaria/client_java/commit/4b69f40bd4e616d69468ce99dc4323162287a577)
- **JDK:** 25.0.2 (OpenJDK 64-Bit Server VM)
- **Benchmark config:** 3 fork(s), 3 warmup, 5 measurement, 4 threads
- **Hardware:** AMD EPYC 7763 64-Core Processor, 4 cores, 16 GB RAM
- **OS:** Linux 6.17.0-1022-azure

## Results

### CounterBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusInc | 65.48K | ± 1.49K | ops/s | **fastest** |
| prometheusNoLabelsInc | 56.68K | ± 450.25 | ops/s | 1.2x slower |
| prometheusAdd | 50.99K | ± 298.03 | ops/s | 1.3x slower |
| codahaleIncNoLabels | 50.01K | ± 1.27K | ops/s | 1.3x slower |
| simpleclientInc | 6.69K | ± 16.73 | ops/s | 9.8x slower |
| simpleclientAdd | 6.44K | ± 10.58 | ops/s | 10x slower |
| simpleclientNoLabelsInc | 6.31K | ± 52.43 | ops/s | 10x slower |
| openTelemetryAdd | 1.25K | ± 5.51 | ops/s | 52x slower |
| openTelemetryInc | 1.25K | ± 28.67 | ops/s | 52x slower |
| openTelemetryIncNoLabels | 1.23K | ± 36.05 | ops/s | 53x slower |

### HistogramBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusClassic | 5.45K | ± 1.38K | ops/s | **fastest** |
| simpleclient | 4.41K | ± 52.62 | ops/s | 1.2x slower |
| prometheusNative | 3.20K | ± 52.12 | ops/s | 1.7x slower |
| openTelemetryClassic | 671.40 | ± 35.91 | ops/s | 8.1x slower |
| openTelemetryExponential | 541.24 | ± 4.88 | ops/s | 10x slower |

### TextFormatUtilBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusWriteToNull | 479.21K | ± 2.61K | ops/s | **fastest** |
| openMetricsWriteToNull | 464.94K | ± 5.73K | ops/s | 1.0x slower |
| prometheusWriteToByteArray | 463.67K | ± 5.67K | ops/s | 1.0x slower |
| openMetricsWriteToByteArray | 462.66K | ± 5.59K | ops/s | 1.0x slower |

### Raw Results

```
Benchmark                                            Mode  Cnt          Score        Error  Units
CounterBenchmark.codahaleIncNoLabels                thrpt   15      50011.188   ± 1270.871  ops/s
CounterBenchmark.openTelemetryAdd                   thrpt   15       1254.627      ± 5.511  ops/s
CounterBenchmark.openTelemetryInc                   thrpt   15       1248.138     ± 28.673  ops/s
CounterBenchmark.openTelemetryIncNoLabels           thrpt   15       1225.365     ± 36.052  ops/s
CounterBenchmark.prometheusAdd                      thrpt   15      50994.792    ± 298.032  ops/s
CounterBenchmark.prometheusInc                      thrpt   15      65478.157   ± 1487.798  ops/s
CounterBenchmark.prometheusNoLabelsInc              thrpt   15      56680.465    ± 450.249  ops/s
CounterBenchmark.simpleclientAdd                    thrpt   15       6441.709     ± 10.578  ops/s
CounterBenchmark.simpleclientInc                    thrpt   15       6690.513     ± 16.727  ops/s
CounterBenchmark.simpleclientNoLabelsInc            thrpt   15       6309.682     ± 52.428  ops/s
HistogramBenchmark.openTelemetryClassic             thrpt   15        671.397     ± 35.907  ops/s
HistogramBenchmark.openTelemetryExponential         thrpt   15        541.239      ± 4.882  ops/s
HistogramBenchmark.prometheusClassic                thrpt   15       5446.001   ± 1383.763  ops/s
HistogramBenchmark.prometheusNative                 thrpt   15       3201.983     ± 52.115  ops/s
HistogramBenchmark.simpleclient                     thrpt   15       4406.091     ± 52.621  ops/s
TextFormatUtilBenchmark.openMetricsWriteToByteArray  thrpt   15     462660.995   ± 5593.295  ops/s
TextFormatUtilBenchmark.openMetricsWriteToNull      thrpt   15     464937.508   ± 5725.654  ops/s
TextFormatUtilBenchmark.prometheusWriteToByteArray  thrpt   15     463674.507   ± 5674.930  ops/s
TextFormatUtilBenchmark.prometheusWriteToNull       thrpt   15     479214.641   ± 2609.877  ops/s
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
