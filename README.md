# Prometheus Java Client Benchmarks

## Run Information

- **Date:** 2026-08-15T04:02:39Z
- **Commit:** [`4b69f40`](https://github.com/psantamaria/client_java/commit/4b69f40bd4e616d69468ce99dc4323162287a577)
- **JDK:** 25.0.2 (OpenJDK 64-Bit Server VM)
- **Benchmark config:** 3 fork(s), 3 warmup, 5 measurement, 4 threads
- **Hardware:** AMD EPYC 9V74 80-Core Processor, 4 cores, 16 GB RAM
- **OS:** Linux 6.17.0-1022-azure

## Results

### CounterBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusInc | 78.05K | ± 1.42K | ops/s | **fastest** |
| prometheusNoLabelsInc | 66.87K | ± 1.29K | ops/s | 1.2x slower |
| prometheusAdd | 61.86K | ± 66.38 | ops/s | 1.3x slower |
| codahaleIncNoLabels | 56.78K | ± 662.09 | ops/s | 1.4x slower |
| simpleclientNoLabelsInc | 8.10K | ± 47.61 | ops/s | 9.6x slower |
| simpleclientInc | 8.00K | ± 114.25 | ops/s | 9.8x slower |
| simpleclientAdd | 7.51K | ± 446.49 | ops/s | 10x slower |
| openTelemetryAdd | 1.83K | ± 78.46 | ops/s | 43x slower |
| openTelemetryIncNoLabels | 1.76K | ± 163.83 | ops/s | 44x slower |
| openTelemetryInc | 1.72K | ± 96.78 | ops/s | 45x slower |

### HistogramBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusClassic | 7.20K | ± 2.96K | ops/s | **fastest** |
| simpleclient | 5.83K | ± 111.85 | ops/s | 1.2x slower |
| prometheusNative | 3.88K | ± 402.68 | ops/s | 1.9x slower |
| openTelemetryClassic | 760.67 | ± 41.01 | ops/s | 9.5x slower |
| openTelemetryExponential | 657.09 | ± 35.42 | ops/s | 11x slower |

### TextFormatUtilBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusWriteToNull | 673.49K | ± 7.35K | ops/s | **fastest** |
| prometheusWriteToByteArray | 659.79K | ± 5.22K | ops/s | 1.0x slower |
| openMetricsWriteToNull | 647.77K | ± 12.30K | ops/s | 1.0x slower |
| openMetricsWriteToByteArray | 634.54K | ± 7.25K | ops/s | 1.1x slower |

### Raw Results

```
Benchmark                                            Mode  Cnt          Score        Error  Units
CounterBenchmark.codahaleIncNoLabels                thrpt   15      56784.353    ± 662.090  ops/s
CounterBenchmark.openTelemetryAdd                   thrpt   15       1828.828     ± 78.457  ops/s
CounterBenchmark.openTelemetryInc                   thrpt   15       1719.974     ± 96.777  ops/s
CounterBenchmark.openTelemetryIncNoLabels           thrpt   15       1764.781    ± 163.830  ops/s
CounterBenchmark.prometheusAdd                      thrpt   15      61861.926     ± 66.382  ops/s
CounterBenchmark.prometheusInc                      thrpt   15      78047.408   ± 1420.895  ops/s
CounterBenchmark.prometheusNoLabelsInc              thrpt   15      66871.517   ± 1292.769  ops/s
CounterBenchmark.simpleclientAdd                    thrpt   15       7509.980    ± 446.494  ops/s
CounterBenchmark.simpleclientInc                    thrpt   15       7995.527    ± 114.254  ops/s
CounterBenchmark.simpleclientNoLabelsInc            thrpt   15       8102.137     ± 47.615  ops/s
HistogramBenchmark.openTelemetryClassic             thrpt   15        760.673     ± 41.013  ops/s
HistogramBenchmark.openTelemetryExponential         thrpt   15        657.092     ± 35.418  ops/s
HistogramBenchmark.prometheusClassic                thrpt   15       7199.824   ± 2963.486  ops/s
HistogramBenchmark.prometheusNative                 thrpt   15       3875.697    ± 402.678  ops/s
HistogramBenchmark.simpleclient                     thrpt   15       5826.491    ± 111.853  ops/s
TextFormatUtilBenchmark.openMetricsWriteToByteArray  thrpt   15     634538.783   ± 7249.620  ops/s
TextFormatUtilBenchmark.openMetricsWriteToNull      thrpt   15     647771.146  ± 12304.025  ops/s
TextFormatUtilBenchmark.prometheusWriteToByteArray  thrpt   15     659791.140   ± 5219.416  ops/s
TextFormatUtilBenchmark.prometheusWriteToNull       thrpt   15     673486.698   ± 7352.644  ops/s
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
