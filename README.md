# Prometheus Java Client Benchmarks

## Run Information

- **Date:** 2026-09-14T08:44:14Z
- **Commit:** [`4b69f40`](https://github.com/psantamaria/client_java/commit/4b69f40bd4e616d69468ce99dc4323162287a577)
- **JDK:** 25.0.2 (OpenJDK 64-Bit Server VM)
- **Benchmark config:** 3 fork(s), 3 warmup, 5 measurement, 4 threads
- **Hardware:** AMD EPYC 9V74 80-Core Processor, 4 cores, 16 GB RAM
- **OS:** Linux 6.17.0-1022-azure

## Results

### CounterBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusInc | 76.61K | ± 553.03 | ops/s | **fastest** |
| prometheusNoLabelsInc | 66.96K | ± 38.74 | ops/s | 1.1x slower |
| prometheusAdd | 62.50K | ± 288.65 | ops/s | 1.2x slower |
| codahaleIncNoLabels | 50.63K | ± 6.30K | ops/s | 1.5x slower |
| simpleclientNoLabelsInc | 8.10K | ± 45.51 | ops/s | 9.5x slower |
| simpleclientInc | 8.05K | ± 98.16 | ops/s | 9.5x slower |
| simpleclientAdd | 7.60K | ± 241.42 | ops/s | 10x slower |
| openTelemetryInc | 1.96K | ± 83.58 | ops/s | 39x slower |
| openTelemetryIncNoLabels | 1.76K | ± 227.29 | ops/s | 43x slower |
| openTelemetryAdd | 1.71K | ± 31.80 | ops/s | 45x slower |

### HistogramBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusClassic | 8.04K | ± 1.56K | ops/s | **fastest** |
| simpleclient | 5.61K | ± 53.10 | ops/s | 1.4x slower |
| prometheusNative | 3.89K | ± 230.26 | ops/s | 2.1x slower |
| openTelemetryClassic | 769.72 | ± 38.23 | ops/s | 10x slower |
| openTelemetryExponential | 689.70 | ± 24.98 | ops/s | 12x slower |

### TextFormatUtilBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusWriteToNull | 670.58K | ± 8.42K | ops/s | **fastest** |
| prometheusWriteToByteArray | 657.87K | ± 10.93K | ops/s | 1.0x slower |
| openMetricsWriteToNull | 643.72K | ± 5.82K | ops/s | 1.0x slower |
| openMetricsWriteToByteArray | 634.77K | ± 5.01K | ops/s | 1.1x slower |

### Raw Results

```
Benchmark                                            Mode  Cnt          Score        Error  Units
CounterBenchmark.codahaleIncNoLabels                thrpt   15      50633.563   ± 6301.873  ops/s
CounterBenchmark.openTelemetryAdd                   thrpt   15       1708.106     ± 31.799  ops/s
CounterBenchmark.openTelemetryInc                   thrpt   15       1962.222     ± 83.575  ops/s
CounterBenchmark.openTelemetryIncNoLabels           thrpt   15       1761.564    ± 227.295  ops/s
CounterBenchmark.prometheusAdd                      thrpt   15      62504.369    ± 288.652  ops/s
CounterBenchmark.prometheusInc                      thrpt   15      76611.890    ± 553.027  ops/s
CounterBenchmark.prometheusNoLabelsInc              thrpt   15      66960.498     ± 38.737  ops/s
CounterBenchmark.simpleclientAdd                    thrpt   15       7601.065    ± 241.415  ops/s
CounterBenchmark.simpleclientInc                    thrpt   15       8052.470     ± 98.160  ops/s
CounterBenchmark.simpleclientNoLabelsInc            thrpt   15       8097.554     ± 45.515  ops/s
HistogramBenchmark.openTelemetryClassic             thrpt   15        769.721     ± 38.225  ops/s
HistogramBenchmark.openTelemetryExponential         thrpt   15        689.703     ± 24.976  ops/s
HistogramBenchmark.prometheusClassic                thrpt   15       8038.360   ± 1558.588  ops/s
HistogramBenchmark.prometheusNative                 thrpt   15       3886.442    ± 230.256  ops/s
HistogramBenchmark.simpleclient                     thrpt   15       5611.501     ± 53.102  ops/s
TextFormatUtilBenchmark.openMetricsWriteToByteArray  thrpt   15     634770.740   ± 5012.011  ops/s
TextFormatUtilBenchmark.openMetricsWriteToNull      thrpt   15     643723.260   ± 5819.990  ops/s
TextFormatUtilBenchmark.prometheusWriteToByteArray  thrpt   15     657874.072  ± 10934.451  ops/s
TextFormatUtilBenchmark.prometheusWriteToNull       thrpt   15     670581.884   ± 8422.404  ops/s
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
