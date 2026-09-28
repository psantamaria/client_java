# Prometheus Java Client Benchmarks

## Run Information

- **Date:** 2026-09-28T09:22:26Z
- **Commit:** [`4b69f40`](https://github.com/psantamaria/client_java/commit/4b69f40bd4e616d69468ce99dc4323162287a577)
- **JDK:** 25.0.2 (OpenJDK 64-Bit Server VM)
- **Benchmark config:** 3 fork(s), 3 warmup, 5 measurement, 4 threads
- **Hardware:** AMD EPYC 7763 64-Core Processor, 4 cores, 16 GB RAM
- **OS:** Linux 6.17.0-1022-azure

## Results

### CounterBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusInc | 65.90K | ± 408.19 | ops/s | **fastest** |
| prometheusNoLabelsInc | 56.47K | ± 386.28 | ops/s | 1.2x slower |
| prometheusAdd | 50.79K | ± 326.12 | ops/s | 1.3x slower |
| codahaleIncNoLabels | 50.20K | ± 77.73 | ops/s | 1.3x slower |
| simpleclientInc | 6.55K | ± 217.04 | ops/s | 10x slower |
| simpleclientNoLabelsInc | 6.53K | ± 143.84 | ops/s | 10x slower |
| simpleclientAdd | 6.03K | ± 342.60 | ops/s | 11x slower |
| openTelemetryAdd | 1.35K | ± 156.85 | ops/s | 49x slower |
| openTelemetryInc | 1.32K | ± 177.21 | ops/s | 50x slower |
| openTelemetryIncNoLabels | 1.26K | ± 179.00 | ops/s | 53x slower |

### HistogramBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusClassic | 5.34K | ± 695.48 | ops/s | **fastest** |
| simpleclient | 4.44K | ± 55.24 | ops/s | 1.2x slower |
| prometheusNative | 2.83K | ± 351.32 | ops/s | 1.9x slower |
| openTelemetryClassic | 715.40 | ± 23.36 | ops/s | 7.5x slower |
| openTelemetryExponential | 527.56 | ± 5.56 | ops/s | 10x slower |

### TextFormatUtilBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusWriteToNull | 484.40K | ± 5.56K | ops/s | **fastest** |
| prometheusWriteToByteArray | 480.25K | ± 5.01K | ops/s | 1.0x slower |
| openMetricsWriteToNull | 473.06K | ± 9.05K | ops/s | 1.0x slower |
| openMetricsWriteToByteArray | 471.07K | ± 3.15K | ops/s | 1.0x slower |

### Raw Results

```
Benchmark                                            Mode  Cnt          Score        Error  Units
CounterBenchmark.codahaleIncNoLabels                thrpt   15      50204.256     ± 77.731  ops/s
CounterBenchmark.openTelemetryAdd                   thrpt   15       1354.035    ± 156.852  ops/s
CounterBenchmark.openTelemetryInc                   thrpt   15       1318.947    ± 177.214  ops/s
CounterBenchmark.openTelemetryIncNoLabels           thrpt   15       1255.010    ± 178.999  ops/s
CounterBenchmark.prometheusAdd                      thrpt   15      50794.321    ± 326.125  ops/s
CounterBenchmark.prometheusInc                      thrpt   15      65902.594    ± 408.186  ops/s
CounterBenchmark.prometheusNoLabelsInc              thrpt   15      56470.225    ± 386.281  ops/s
CounterBenchmark.simpleclientAdd                    thrpt   15       6026.159    ± 342.603  ops/s
CounterBenchmark.simpleclientInc                    thrpt   15       6550.113    ± 217.042  ops/s
CounterBenchmark.simpleclientNoLabelsInc            thrpt   15       6534.105    ± 143.837  ops/s
HistogramBenchmark.openTelemetryClassic             thrpt   15        715.399     ± 23.358  ops/s
HistogramBenchmark.openTelemetryExponential         thrpt   15        527.564      ± 5.561  ops/s
HistogramBenchmark.prometheusClassic                thrpt   15       5343.873    ± 695.476  ops/s
HistogramBenchmark.prometheusNative                 thrpt   15       2827.041    ± 351.317  ops/s
HistogramBenchmark.simpleclient                     thrpt   15       4435.967     ± 55.238  ops/s
TextFormatUtilBenchmark.openMetricsWriteToByteArray  thrpt   15     471065.913   ± 3145.470  ops/s
TextFormatUtilBenchmark.openMetricsWriteToNull      thrpt   15     473061.704   ± 9053.352  ops/s
TextFormatUtilBenchmark.prometheusWriteToByteArray  thrpt   15     480253.562   ± 5008.635  ops/s
TextFormatUtilBenchmark.prometheusWriteToNull       thrpt   15     484399.059   ± 5560.074  ops/s
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
