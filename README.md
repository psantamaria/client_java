# Prometheus Java Client Benchmarks

## Run Information

- **Date:** 2026-08-29T09:48:23Z
- **Commit:** [`4b69f40`](https://github.com/psantamaria/client_java/commit/4b69f40bd4e616d69468ce99dc4323162287a577)
- **JDK:** 25.0.2 (OpenJDK 64-Bit Server VM)
- **Benchmark config:** 3 fork(s), 3 warmup, 5 measurement, 4 threads
- **Hardware:** AMD EPYC 7763 64-Core Processor, 4 cores, 16 GB RAM
- **OS:** Linux 6.17.0-1022-azure

## Results

### CounterBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusInc | 65.68K | ± 777.00 | ops/s | **fastest** |
| prometheusNoLabelsInc | 52.79K | ± 5.66K | ops/s | 1.2x slower |
| prometheusAdd | 51.16K | ± 555.07 | ops/s | 1.3x slower |
| codahaleIncNoLabels | 47.56K | ± 456.95 | ops/s | 1.4x slower |
| simpleclientInc | 6.60K | ± 171.05 | ops/s | 10.0x slower |
| simpleclientNoLabelsInc | 6.49K | ± 203.14 | ops/s | 10x slower |
| simpleclientAdd | 6.23K | ± 189.14 | ops/s | 11x slower |
| openTelemetryAdd | 1.53K | ± 252.32 | ops/s | 43x slower |
| openTelemetryIncNoLabels | 1.35K | ± 165.95 | ops/s | 49x slower |
| openTelemetryInc | 1.22K | ± 21.41 | ops/s | 54x slower |

### HistogramBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusClassic | 5.25K | ± 1.03K | ops/s | **fastest** |
| simpleclient | 4.45K | ± 61.65 | ops/s | 1.2x slower |
| prometheusNative | 2.96K | ± 237.69 | ops/s | 1.8x slower |
| openTelemetryClassic | 702.25 | ± 38.16 | ops/s | 7.5x slower |
| openTelemetryExponential | 577.98 | ± 21.91 | ops/s | 9.1x slower |

### TextFormatUtilBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusWriteToNull | 488.72K | ± 2.75K | ops/s | **fastest** |
| prometheusWriteToByteArray | 474.03K | ± 9.47K | ops/s | 1.0x slower |
| openMetricsWriteToNull | 468.83K | ± 6.08K | ops/s | 1.0x slower |
| openMetricsWriteToByteArray | 464.28K | ± 6.95K | ops/s | 1.1x slower |

### Raw Results

```
Benchmark                                            Mode  Cnt          Score        Error  Units
CounterBenchmark.codahaleIncNoLabels                thrpt   15      47563.600    ± 456.954  ops/s
CounterBenchmark.openTelemetryAdd                   thrpt   15       1534.659    ± 252.317  ops/s
CounterBenchmark.openTelemetryInc                   thrpt   15       1220.157     ± 21.406  ops/s
CounterBenchmark.openTelemetryIncNoLabels           thrpt   15       1347.029    ± 165.950  ops/s
CounterBenchmark.prometheusAdd                      thrpt   15      51162.583    ± 555.070  ops/s
CounterBenchmark.prometheusInc                      thrpt   15      65681.760    ± 777.004  ops/s
CounterBenchmark.prometheusNoLabelsInc              thrpt   15      52789.407   ± 5657.136  ops/s
CounterBenchmark.simpleclientAdd                    thrpt   15       6226.370    ± 189.144  ops/s
CounterBenchmark.simpleclientInc                    thrpt   15       6595.062    ± 171.046  ops/s
CounterBenchmark.simpleclientNoLabelsInc            thrpt   15       6494.487    ± 203.140  ops/s
HistogramBenchmark.openTelemetryClassic             thrpt   15        702.252     ± 38.159  ops/s
HistogramBenchmark.openTelemetryExponential         thrpt   15        577.981     ± 21.915  ops/s
HistogramBenchmark.prometheusClassic                thrpt   15       5250.494   ± 1025.718  ops/s
HistogramBenchmark.prometheusNative                 thrpt   15       2955.866    ± 237.692  ops/s
HistogramBenchmark.simpleclient                     thrpt   15       4451.332     ± 61.649  ops/s
TextFormatUtilBenchmark.openMetricsWriteToByteArray  thrpt   15     464281.980   ± 6949.979  ops/s
TextFormatUtilBenchmark.openMetricsWriteToNull      thrpt   15     468828.923   ± 6082.220  ops/s
TextFormatUtilBenchmark.prometheusWriteToByteArray  thrpt   15     474032.941   ± 9467.780  ops/s
TextFormatUtilBenchmark.prometheusWriteToNull       thrpt   15     488720.797   ± 2749.153  ops/s
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
