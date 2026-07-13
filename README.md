# Prometheus Java Client Benchmarks

## Run Information

- **Date:** 2026-07-13T06:48:53Z
- **Commit:** [`4b69f40`](https://github.com/psantamaria/client_java/commit/4b69f40bd4e616d69468ce99dc4323162287a577)
- **JDK:** 25.0.2 (OpenJDK 64-Bit Server VM)
- **Benchmark config:** 3 fork(s), 3 warmup, 5 measurement, 4 threads
- **Hardware:** AMD EPYC 7763 64-Core Processor, 4 cores, 16 GB RAM
- **OS:** Linux 6.17.0-1018-azure

## Results

### CounterBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusInc | 66.15K | ± 360.37 | ops/s | **fastest** |
| prometheusNoLabelsInc | 56.85K | ± 180.38 | ops/s | 1.2x slower |
| prometheusAdd | 50.61K | ± 406.01 | ops/s | 1.3x slower |
| codahaleIncNoLabels | 48.11K | ± 1.54K | ops/s | 1.4x slower |
| simpleclientNoLabelsInc | 6.61K | ± 17.86 | ops/s | 10x slower |
| simpleclientInc | 6.40K | ± 254.49 | ops/s | 10x slower |
| simpleclientAdd | 6.31K | ± 222.20 | ops/s | 10x slower |
| openTelemetryInc | 1.28K | ± 50.46 | ops/s | 52x slower |
| openTelemetryIncNoLabels | 1.26K | ± 138.24 | ops/s | 52x slower |
| openTelemetryAdd | 1.25K | ± 30.46 | ops/s | 53x slower |

### HistogramBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusClassic | 5.27K | ± 1.49K | ops/s | **fastest** |
| simpleclient | 4.45K | ± 47.08 | ops/s | 1.2x slower |
| prometheusNative | 2.57K | ± 97.92 | ops/s | 2.0x slower |
| openTelemetryClassic | 683.21 | ± 28.70 | ops/s | 7.7x slower |
| openTelemetryExponential | 558.11 | ± 18.90 | ops/s | 9.4x slower |

### TextFormatUtilBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusWriteToByteArray | 477.00K | ± 2.14K | ops/s | **fastest** |
| prometheusWriteToNull | 476.26K | ± 3.81K | ops/s | 1.0x slower |
| openMetricsWriteToNull | 474.84K | ± 3.16K | ops/s | 1.0x slower |
| openMetricsWriteToByteArray | 462.46K | ± 7.54K | ops/s | 1.0x slower |

### Raw Results

```
Benchmark                                            Mode  Cnt          Score        Error  Units
CounterBenchmark.codahaleIncNoLabels                thrpt   15      48114.871   ± 1537.050  ops/s
CounterBenchmark.openTelemetryAdd                   thrpt   15       1249.530     ± 30.463  ops/s
CounterBenchmark.openTelemetryInc                   thrpt   15       1275.117     ± 50.457  ops/s
CounterBenchmark.openTelemetryIncNoLabels           thrpt   15       1262.597    ± 138.245  ops/s
CounterBenchmark.prometheusAdd                      thrpt   15      50611.178    ± 406.014  ops/s
CounterBenchmark.prometheusInc                      thrpt   15      66146.265    ± 360.373  ops/s
CounterBenchmark.prometheusNoLabelsInc              thrpt   15      56850.673    ± 180.382  ops/s
CounterBenchmark.simpleclientAdd                    thrpt   15       6310.504    ± 222.196  ops/s
CounterBenchmark.simpleclientInc                    thrpt   15       6403.875    ± 254.488  ops/s
CounterBenchmark.simpleclientNoLabelsInc            thrpt   15       6614.626     ± 17.859  ops/s
HistogramBenchmark.openTelemetryClassic             thrpt   15        683.212     ± 28.703  ops/s
HistogramBenchmark.openTelemetryExponential         thrpt   15        558.107     ± 18.899  ops/s
HistogramBenchmark.prometheusClassic                thrpt   15       5268.980   ± 1488.123  ops/s
HistogramBenchmark.prometheusNative                 thrpt   15       2574.192     ± 97.921  ops/s
HistogramBenchmark.simpleclient                     thrpt   15       4452.059     ± 47.085  ops/s
TextFormatUtilBenchmark.openMetricsWriteToByteArray  thrpt   15     462456.188   ± 7539.024  ops/s
TextFormatUtilBenchmark.openMetricsWriteToNull      thrpt   15     474841.191   ± 3164.766  ops/s
TextFormatUtilBenchmark.prometheusWriteToByteArray  thrpt   15     476998.646   ± 2143.253  ops/s
TextFormatUtilBenchmark.prometheusWriteToNull       thrpt   15     476257.159   ± 3805.050  ops/s
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
