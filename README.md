# Prometheus Java Client Benchmarks

## Run Information

- **Date:** 2026-08-22T04:05:32Z
- **Commit:** [`4b69f40`](https://github.com/psantamaria/client_java/commit/4b69f40bd4e616d69468ce99dc4323162287a577)
- **JDK:** 25.0.2 (OpenJDK 64-Bit Server VM)
- **Benchmark config:** 3 fork(s), 3 warmup, 5 measurement, 4 threads
- **Hardware:** AMD EPYC 7763 64-Core Processor, 4 cores, 16 GB RAM
- **OS:** Linux 6.17.0-1022-azure

## Results

### CounterBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusInc | 66.08K | ± 380.23 | ops/s | **fastest** |
| prometheusNoLabelsInc | 57.09K | ± 121.33 | ops/s | 1.2x slower |
| prometheusAdd | 51.44K | ± 154.18 | ops/s | 1.3x slower |
| codahaleIncNoLabels | 48.64K | ± 1.32K | ops/s | 1.4x slower |
| simpleclientInc | 6.55K | ± 246.44 | ops/s | 10x slower |
| simpleclientAdd | 6.46K | ± 19.67 | ops/s | 10x slower |
| simpleclientNoLabelsInc | 6.23K | ± 8.98 | ops/s | 11x slower |
| openTelemetryInc | 1.40K | ± 161.76 | ops/s | 47x slower |
| openTelemetryIncNoLabels | 1.33K | ± 140.21 | ops/s | 50x slower |
| openTelemetryAdd | 1.26K | ± 73.61 | ops/s | 53x slower |

### HistogramBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusClassic | 6.01K | ± 2.02K | ops/s | **fastest** |
| simpleclient | 4.42K | ± 33.15 | ops/s | 1.4x slower |
| prometheusNative | 3.07K | ± 214.45 | ops/s | 2.0x slower |
| openTelemetryClassic | 691.96 | ± 16.66 | ops/s | 8.7x slower |
| openTelemetryExponential | 574.43 | ± 29.64 | ops/s | 10x slower |

### TextFormatUtilBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusWriteToNull | 499.46K | ± 7.93K | ops/s | **fastest** |
| prometheusWriteToByteArray | 490.84K | ± 11.30K | ops/s | 1.0x slower |
| openMetricsWriteToByteArray | 482.64K | ± 4.35K | ops/s | 1.0x slower |
| openMetricsWriteToNull | 476.03K | ± 19.61K | ops/s | 1.0x slower |

### Raw Results

```
Benchmark                                            Mode  Cnt          Score        Error  Units
CounterBenchmark.codahaleIncNoLabels                thrpt   15      48641.158   ± 1318.205  ops/s
CounterBenchmark.openTelemetryAdd                   thrpt   15       1256.725     ± 73.610  ops/s
CounterBenchmark.openTelemetryInc                   thrpt   15       1395.031    ± 161.757  ops/s
CounterBenchmark.openTelemetryIncNoLabels           thrpt   15       1334.956    ± 140.215  ops/s
CounterBenchmark.prometheusAdd                      thrpt   15      51440.854    ± 154.181  ops/s
CounterBenchmark.prometheusInc                      thrpt   15      66084.257    ± 380.230  ops/s
CounterBenchmark.prometheusNoLabelsInc              thrpt   15      57089.115    ± 121.326  ops/s
CounterBenchmark.simpleclientAdd                    thrpt   15       6460.630     ± 19.670  ops/s
CounterBenchmark.simpleclientInc                    thrpt   15       6550.053    ± 246.436  ops/s
CounterBenchmark.simpleclientNoLabelsInc            thrpt   15       6227.324      ± 8.983  ops/s
HistogramBenchmark.openTelemetryClassic             thrpt   15        691.965     ± 16.657  ops/s
HistogramBenchmark.openTelemetryExponential         thrpt   15        574.432     ± 29.639  ops/s
HistogramBenchmark.prometheusClassic                thrpt   15       6008.296   ± 2016.831  ops/s
HistogramBenchmark.prometheusNative                 thrpt   15       3073.734    ± 214.450  ops/s
HistogramBenchmark.simpleclient                     thrpt   15       4424.196     ± 33.147  ops/s
TextFormatUtilBenchmark.openMetricsWriteToByteArray  thrpt   15     482644.026   ± 4353.203  ops/s
TextFormatUtilBenchmark.openMetricsWriteToNull      thrpt   15     476030.618  ± 19607.476  ops/s
TextFormatUtilBenchmark.prometheusWriteToByteArray  thrpt   15     490839.299  ± 11303.122  ops/s
TextFormatUtilBenchmark.prometheusWriteToNull       thrpt   15     499458.225   ± 7929.448  ops/s
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
