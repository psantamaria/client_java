# Prometheus Java Client Benchmarks

## Run Information

- **Date:** 2026-06-22T08:33:38Z
- **Commit:** [`4b69f40`](https://github.com/psantamaria/client_java/commit/4b69f40bd4e616d69468ce99dc4323162287a577)
- **JDK:** 25.0.2 (OpenJDK 64-Bit Server VM)
- **Benchmark config:** 3 fork(s), 3 warmup, 5 measurement, 4 threads
- **Hardware:** AMD EPYC 7763 64-Core Processor, 4 cores, 16 GB RAM
- **OS:** Linux 6.17.0-1018-azure

## Results

### CounterBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusInc | 63.84K | ± 4.11K | ops/s | **fastest** |
| prometheusNoLabelsInc | 56.65K | ± 375.53 | ops/s | 1.1x slower |
| prometheusAdd | 51.58K | ± 83.74 | ops/s | 1.2x slower |
| codahaleIncNoLabels | 49.35K | ± 1.72K | ops/s | 1.3x slower |
| simpleclientNoLabelsInc | 6.62K | ± 16.41 | ops/s | 9.6x slower |
| simpleclientInc | 6.61K | ± 172.71 | ops/s | 9.7x slower |
| simpleclientAdd | 6.32K | ± 242.12 | ops/s | 10x slower |
| openTelemetryInc | 1.27K | ± 23.67 | ops/s | 50x slower |
| openTelemetryAdd | 1.24K | ± 46.48 | ops/s | 51x slower |
| openTelemetryIncNoLabels | 1.23K | ± 58.61 | ops/s | 52x slower |

### HistogramBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusClassic | 6.76K | ± 528.47 | ops/s | **fastest** |
| simpleclient | 4.46K | ± 49.21 | ops/s | 1.5x slower |
| prometheusNative | 2.59K | ± 62.72 | ops/s | 2.6x slower |
| openTelemetryClassic | 695.85 | ± 24.25 | ops/s | 9.7x slower |
| openTelemetryExponential | 550.65 | ± 19.09 | ops/s | 12x slower |

### TextFormatUtilBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusWriteToByteArray | 461.86K | ± 8.10K | ops/s | **fastest** |
| openMetricsWriteToNull | 451.13K | ± 22.40K | ops/s | 1.0x slower |
| prometheusWriteToNull | 450.37K | ± 31.19K | ops/s | 1.0x slower |
| openMetricsWriteToByteArray | 437.90K | ± 35.62K | ops/s | 1.1x slower |

### Raw Results

```
Benchmark                                            Mode  Cnt          Score        Error  Units
CounterBenchmark.codahaleIncNoLabels                thrpt   15      49345.516   ± 1718.372  ops/s
CounterBenchmark.openTelemetryAdd                   thrpt   15       1244.355     ± 46.475  ops/s
CounterBenchmark.openTelemetryInc                   thrpt   15       1266.976     ± 23.671  ops/s
CounterBenchmark.openTelemetryIncNoLabels           thrpt   15       1226.948     ± 58.611  ops/s
CounterBenchmark.prometheusAdd                      thrpt   15      51578.858     ± 83.738  ops/s
CounterBenchmark.prometheusInc                      thrpt   15      63842.093   ± 4110.681  ops/s
CounterBenchmark.prometheusNoLabelsInc              thrpt   15      56647.719    ± 375.529  ops/s
CounterBenchmark.simpleclientAdd                    thrpt   15       6319.673    ± 242.120  ops/s
CounterBenchmark.simpleclientInc                    thrpt   15       6607.064    ± 172.705  ops/s
CounterBenchmark.simpleclientNoLabelsInc            thrpt   15       6616.640     ± 16.405  ops/s
HistogramBenchmark.openTelemetryClassic             thrpt   15        695.847     ± 24.250  ops/s
HistogramBenchmark.openTelemetryExponential         thrpt   15        550.655     ± 19.094  ops/s
HistogramBenchmark.prometheusClassic                thrpt   15       6757.605    ± 528.468  ops/s
HistogramBenchmark.prometheusNative                 thrpt   15       2594.251     ± 62.715  ops/s
HistogramBenchmark.simpleclient                     thrpt   15       4458.448     ± 49.209  ops/s
TextFormatUtilBenchmark.openMetricsWriteToByteArray  thrpt   15     437904.372  ± 35617.950  ops/s
TextFormatUtilBenchmark.openMetricsWriteToNull      thrpt   15     451132.544  ± 22396.088  ops/s
TextFormatUtilBenchmark.prometheusWriteToByteArray  thrpt   15     461860.637   ± 8097.627  ops/s
TextFormatUtilBenchmark.prometheusWriteToNull       thrpt   15     450365.751  ± 31193.781  ops/s
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
