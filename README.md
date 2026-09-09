# Prometheus Java Client Benchmarks

## Run Information

- **Date:** 2026-09-09T08:15:11Z
- **Commit:** [`4b69f40`](https://github.com/psantamaria/client_java/commit/4b69f40bd4e616d69468ce99dc4323162287a577)
- **JDK:** 25.0.2 (OpenJDK 64-Bit Server VM)
- **Benchmark config:** 3 fork(s), 3 warmup, 5 measurement, 4 threads
- **Hardware:** AMD EPYC 9V74 80-Core Processor, 4 cores, 16 GB RAM
- **OS:** Linux 6.17.0-1022-azure

## Results

### CounterBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusInc | 59.83K | ± 42.26 | ops/s | **fastest** |
| prometheusNoLabelsInc | 52.71K | ± 81.47 | ops/s | 1.1x slower |
| prometheusAdd | 48.83K | ± 693.57 | ops/s | 1.2x slower |
| codahaleIncNoLabels | 43.37K | ± 1.78K | ops/s | 1.4x slower |
| simpleclientInc | 6.29K | ± 123.90 | ops/s | 9.5x slower |
| simpleclientNoLabelsInc | 6.09K | ± 234.86 | ops/s | 9.8x slower |
| simpleclientAdd | 5.86K | ± 247.46 | ops/s | 10x slower |
| openTelemetryInc | 1.36K | ± 181.89 | ops/s | 44x slower |
| openTelemetryIncNoLabels | 1.36K | ± 39.93 | ops/s | 44x slower |
| openTelemetryAdd | 1.32K | ± 79.58 | ops/s | 45x slower |

### HistogramBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusClassic | 4.58K | ± 447.42 | ops/s | **fastest** |
| simpleclient | 4.36K | ± 59.71 | ops/s | 1.1x slower |
| prometheusNative | 2.86K | ± 270.81 | ops/s | 1.6x slower |
| openTelemetryClassic | 615.79 | ± 27.56 | ops/s | 7.4x slower |
| openTelemetryExponential | 521.05 | ± 24.39 | ops/s | 8.8x slower |

### TextFormatUtilBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusWriteToNull | 556.64K | ± 5.46K | ops/s | **fastest** |
| prometheusWriteToByteArray | 543.28K | ± 5.90K | ops/s | 1.0x slower |
| openMetricsWriteToNull | 535.45K | ± 3.95K | ops/s | 1.0x slower |
| openMetricsWriteToByteArray | 522.22K | ± 5.91K | ops/s | 1.1x slower |

### Raw Results

```
Benchmark                                            Mode  Cnt          Score        Error  Units
CounterBenchmark.codahaleIncNoLabels                thrpt   15      43367.768   ± 1776.044  ops/s
CounterBenchmark.openTelemetryAdd                   thrpt   15       1316.647     ± 79.577  ops/s
CounterBenchmark.openTelemetryInc                   thrpt   15       1360.283    ± 181.892  ops/s
CounterBenchmark.openTelemetryIncNoLabels           thrpt   15       1359.522     ± 39.932  ops/s
CounterBenchmark.prometheusAdd                      thrpt   15      48834.376    ± 693.568  ops/s
CounterBenchmark.prometheusInc                      thrpt   15      59826.062     ± 42.259  ops/s
CounterBenchmark.prometheusNoLabelsInc              thrpt   15      52712.357     ± 81.466  ops/s
CounterBenchmark.simpleclientAdd                    thrpt   15       5858.672    ± 247.457  ops/s
CounterBenchmark.simpleclientInc                    thrpt   15       6290.169    ± 123.900  ops/s
CounterBenchmark.simpleclientNoLabelsInc            thrpt   15       6092.657    ± 234.860  ops/s
HistogramBenchmark.openTelemetryClassic             thrpt   15        615.786     ± 27.561  ops/s
HistogramBenchmark.openTelemetryExponential         thrpt   15        521.051     ± 24.395  ops/s
HistogramBenchmark.prometheusClassic                thrpt   15       4583.793    ± 447.424  ops/s
HistogramBenchmark.prometheusNative                 thrpt   15       2858.307    ± 270.808  ops/s
HistogramBenchmark.simpleclient                     thrpt   15       4356.623     ± 59.714  ops/s
TextFormatUtilBenchmark.openMetricsWriteToByteArray  thrpt   15     522222.698   ± 5912.369  ops/s
TextFormatUtilBenchmark.openMetricsWriteToNull      thrpt   15     535451.008   ± 3949.824  ops/s
TextFormatUtilBenchmark.prometheusWriteToByteArray  thrpt   15     543278.032   ± 5897.213  ops/s
TextFormatUtilBenchmark.prometheusWriteToNull       thrpt   15     556641.772   ± 5456.820  ops/s
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
