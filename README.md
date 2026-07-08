# Prometheus Java Client Benchmarks

## Run Information

- **Date:** 2026-07-08T06:33:25Z
- **Commit:** [`4b69f40`](https://github.com/psantamaria/client_java/commit/4b69f40bd4e616d69468ce99dc4323162287a577)
- **JDK:** 25.0.2 (OpenJDK 64-Bit Server VM)
- **Benchmark config:** 3 fork(s), 3 warmup, 5 measurement, 4 threads
- **Hardware:** AMD EPYC 7763 64-Core Processor, 4 cores, 16 GB RAM
- **OS:** Linux 6.17.0-1018-azure

## Results

### CounterBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusInc | 65.48K | ± 1.34K | ops/s | **fastest** |
| prometheusNoLabelsInc | 56.71K | ± 779.08 | ops/s | 1.2x slower |
| prometheusAdd | 51.22K | ± 583.06 | ops/s | 1.3x slower |
| codahaleIncNoLabels | 50.11K | ± 874.76 | ops/s | 1.3x slower |
| simpleclientInc | 6.66K | ± 60.85 | ops/s | 9.8x slower |
| simpleclientNoLabelsInc | 6.39K | ± 183.31 | ops/s | 10x slower |
| simpleclientAdd | 6.10K | ± 283.71 | ops/s | 11x slower |
| openTelemetryIncNoLabels | 1.43K | ± 198.74 | ops/s | 46x slower |
| openTelemetryAdd | 1.30K | ± 25.07 | ops/s | 51x slower |
| openTelemetryInc | 1.26K | ± 42.47 | ops/s | 52x slower |

### HistogramBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusClassic | 6.21K | ± 1.48K | ops/s | **fastest** |
| simpleclient | 4.44K | ± 24.50 | ops/s | 1.4x slower |
| prometheusNative | 2.72K | ± 298.45 | ops/s | 2.3x slower |
| openTelemetryClassic | 682.78 | ± 11.91 | ops/s | 9.1x slower |
| openTelemetryExponential | 533.28 | ± 15.64 | ops/s | 12x slower |

### TextFormatUtilBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusWriteToNull | 481.36K | ± 3.50K | ops/s | **fastest** |
| prometheusWriteToByteArray | 479.67K | ± 2.17K | ops/s | 1.0x slower |
| openMetricsWriteToNull | 469.48K | ± 6.45K | ops/s | 1.0x slower |
| openMetricsWriteToByteArray | 463.98K | ± 3.73K | ops/s | 1.0x slower |

### Raw Results

```
Benchmark                                            Mode  Cnt          Score        Error  Units
CounterBenchmark.codahaleIncNoLabels                thrpt   15      50106.042    ± 874.755  ops/s
CounterBenchmark.openTelemetryAdd                   thrpt   15       1296.256     ± 25.070  ops/s
CounterBenchmark.openTelemetryInc                   thrpt   15       1263.128     ± 42.467  ops/s
CounterBenchmark.openTelemetryIncNoLabels           thrpt   15       1432.493    ± 198.736  ops/s
CounterBenchmark.prometheusAdd                      thrpt   15      51217.958    ± 583.062  ops/s
CounterBenchmark.prometheusInc                      thrpt   15      65480.765   ± 1340.061  ops/s
CounterBenchmark.prometheusNoLabelsInc              thrpt   15      56708.901    ± 779.082  ops/s
CounterBenchmark.simpleclientAdd                    thrpt   15       6102.160    ± 283.712  ops/s
CounterBenchmark.simpleclientInc                    thrpt   15       6661.923     ± 60.848  ops/s
CounterBenchmark.simpleclientNoLabelsInc            thrpt   15       6390.172    ± 183.314  ops/s
HistogramBenchmark.openTelemetryClassic             thrpt   15        682.775     ± 11.914  ops/s
HistogramBenchmark.openTelemetryExponential         thrpt   15        533.281     ± 15.643  ops/s
HistogramBenchmark.prometheusClassic                thrpt   15       6211.617   ± 1482.712  ops/s
HistogramBenchmark.prometheusNative                 thrpt   15       2717.864    ± 298.449  ops/s
HistogramBenchmark.simpleclient                     thrpt   15       4437.013     ± 24.498  ops/s
TextFormatUtilBenchmark.openMetricsWriteToByteArray  thrpt   15     463982.591   ± 3726.102  ops/s
TextFormatUtilBenchmark.openMetricsWriteToNull      thrpt   15     469479.857   ± 6454.637  ops/s
TextFormatUtilBenchmark.prometheusWriteToByteArray  thrpt   15     479673.785   ± 2174.026  ops/s
TextFormatUtilBenchmark.prometheusWriteToNull       thrpt   15     481363.113   ± 3495.042  ops/s
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
