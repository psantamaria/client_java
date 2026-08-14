# Prometheus Java Client Benchmarks

## Run Information

- **Date:** 2026-08-14T05:18:02Z
- **Commit:** [`4b69f40`](https://github.com/psantamaria/client_java/commit/4b69f40bd4e616d69468ce99dc4323162287a577)
- **JDK:** 25.0.2 (OpenJDK 64-Bit Server VM)
- **Benchmark config:** 3 fork(s), 3 warmup, 5 measurement, 4 threads
- **Hardware:** AMD EPYC 7763 64-Core Processor, 4 cores, 16 GB RAM
- **OS:** Linux 6.17.0-1020-azure

## Results

### CounterBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusInc | 66.00K | ± 362.33 | ops/s | **fastest** |
| prometheusAdd | 51.20K | ± 296.73 | ops/s | 1.3x slower |
| prometheusNoLabelsInc | 50.63K | ± 4.60K | ops/s | 1.3x slower |
| codahaleIncNoLabels | 47.92K | ± 1.03K | ops/s | 1.4x slower |
| simpleclientInc | 6.70K | ± 8.81 | ops/s | 9.9x slower |
| simpleclientAdd | 6.36K | ± 206.16 | ops/s | 10x slower |
| simpleclientNoLabelsInc | 6.25K | ± 66.74 | ops/s | 11x slower |
| openTelemetryAdd | 1.27K | ± 36.03 | ops/s | 52x slower |
| openTelemetryIncNoLabels | 1.23K | ± 42.31 | ops/s | 54x slower |
| openTelemetryInc | 1.22K | ± 23.79 | ops/s | 54x slower |

### HistogramBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusClassic | 6.19K | ± 1.45K | ops/s | **fastest** |
| simpleclient | 4.46K | ± 55.72 | ops/s | 1.4x slower |
| prometheusNative | 3.01K | ± 292.51 | ops/s | 2.1x slower |
| openTelemetryClassic | 688.70 | ± 37.53 | ops/s | 9.0x slower |
| openTelemetryExponential | 573.80 | ± 24.27 | ops/s | 11x slower |

### TextFormatUtilBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusWriteToByteArray | 476.07K | ± 5.87K | ops/s | **fastest** |
| prometheusWriteToNull | 475.95K | ± 3.97K | ops/s | 1.0x slower |
| openMetricsWriteToNull | 471.30K | ± 2.62K | ops/s | 1.0x slower |
| openMetricsWriteToByteArray | 459.09K | ± 6.57K | ops/s | 1.0x slower |

### Raw Results

```
Benchmark                                            Mode  Cnt          Score        Error  Units
CounterBenchmark.codahaleIncNoLabels                thrpt   15      47920.213   ± 1030.451  ops/s
CounterBenchmark.openTelemetryAdd                   thrpt   15       1266.008     ± 36.032  ops/s
CounterBenchmark.openTelemetryInc                   thrpt   15       1219.774     ± 23.785  ops/s
CounterBenchmark.openTelemetryIncNoLabels           thrpt   15       1229.321     ± 42.309  ops/s
CounterBenchmark.prometheusAdd                      thrpt   15      51199.409    ± 296.726  ops/s
CounterBenchmark.prometheusInc                      thrpt   15      65995.256    ± 362.334  ops/s
CounterBenchmark.prometheusNoLabelsInc              thrpt   15      50633.502   ± 4599.462  ops/s
CounterBenchmark.simpleclientAdd                    thrpt   15       6362.878    ± 206.157  ops/s
CounterBenchmark.simpleclientInc                    thrpt   15       6696.090      ± 8.813  ops/s
CounterBenchmark.simpleclientNoLabelsInc            thrpt   15       6254.491     ± 66.744  ops/s
HistogramBenchmark.openTelemetryClassic             thrpt   15        688.701     ± 37.532  ops/s
HistogramBenchmark.openTelemetryExponential         thrpt   15        573.802     ± 24.268  ops/s
HistogramBenchmark.prometheusClassic                thrpt   15       6189.665   ± 1445.369  ops/s
HistogramBenchmark.prometheusNative                 thrpt   15       3014.725    ± 292.505  ops/s
HistogramBenchmark.simpleclient                     thrpt   15       4461.019     ± 55.717  ops/s
TextFormatUtilBenchmark.openMetricsWriteToByteArray  thrpt   15     459087.805   ± 6569.339  ops/s
TextFormatUtilBenchmark.openMetricsWriteToNull      thrpt   15     471304.315   ± 2617.231  ops/s
TextFormatUtilBenchmark.prometheusWriteToByteArray  thrpt   15     476071.301   ± 5867.890  ops/s
TextFormatUtilBenchmark.prometheusWriteToNull       thrpt   15     475953.075   ± 3974.850  ops/s
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
