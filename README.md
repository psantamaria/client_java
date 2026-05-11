# Prometheus Java Client Benchmarks

## Run Information

- **Date:** 2026-05-11T07:11:10Z
- **Commit:** [`4b69f40`](https://github.com/psantamaria/client_java/commit/4b69f40bd4e616d69468ce99dc4323162287a577)
- **JDK:** 25.0.2 (OpenJDK 64-Bit Server VM)
- **Benchmark config:** 3 fork(s), 3 warmup, 5 measurement, 4 threads
- **Hardware:** AMD EPYC 7763 64-Core Processor, 4 cores, 16 GB RAM
- **OS:** Linux 6.17.0-1010-azure

## Results

### CounterBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusInc | 65.97K | ± 313.39 | ops/s | **fastest** |
| prometheusNoLabelsInc | 55.86K | ± 687.49 | ops/s | 1.2x slower |
| prometheusAdd | 50.77K | ± 426.70 | ops/s | 1.3x slower |
| codahaleIncNoLabels | 47.61K | ± 355.78 | ops/s | 1.4x slower |
| simpleclientInc | 6.56K | ± 222.19 | ops/s | 10x slower |
| simpleclientAdd | 6.48K | ± 12.77 | ops/s | 10x slower |
| simpleclientNoLabelsInc | 6.35K | ± 198.48 | ops/s | 10x slower |
| openTelemetryAdd | 1.39K | ± 197.39 | ops/s | 47x slower |
| openTelemetryInc | 1.39K | ± 146.16 | ops/s | 48x slower |
| openTelemetryIncNoLabels | 1.31K | ± 185.29 | ops/s | 50x slower |

### HistogramBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusClassic | 5.68K | ± 2.03K | ops/s | **fastest** |
| simpleclient | 4.39K | ± 70.02 | ops/s | 1.3x slower |
| prometheusNative | 2.94K | ± 215.87 | ops/s | 1.9x slower |
| openTelemetryClassic | 690.37 | ± 19.96 | ops/s | 8.2x slower |
| openTelemetryExponential | 565.77 | ± 14.23 | ops/s | 10x slower |

### TextFormatUtilBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusWriteToNull | 488.41K | ± 3.63K | ops/s | **fastest** |
| prometheusWriteToByteArray | 482.67K | ± 4.92K | ops/s | 1.0x slower |
| openMetricsWriteToNull | 480.87K | ± 4.54K | ops/s | 1.0x slower |
| openMetricsWriteToByteArray | 476.05K | ± 2.37K | ops/s | 1.0x slower |

### Raw Results

```
Benchmark                                            Mode  Cnt          Score        Error  Units
CounterBenchmark.codahaleIncNoLabels                thrpt   15      47611.968    ± 355.777  ops/s
CounterBenchmark.openTelemetryAdd                   thrpt   15       1390.577    ± 197.395  ops/s
CounterBenchmark.openTelemetryInc                   thrpt   15       1385.531    ± 146.158  ops/s
CounterBenchmark.openTelemetryIncNoLabels           thrpt   15       1306.497    ± 185.286  ops/s
CounterBenchmark.prometheusAdd                      thrpt   15      50771.522    ± 426.702  ops/s
CounterBenchmark.prometheusInc                      thrpt   15      65973.232    ± 313.393  ops/s
CounterBenchmark.prometheusNoLabelsInc              thrpt   15      55858.319    ± 687.494  ops/s
CounterBenchmark.simpleclientAdd                    thrpt   15       6481.480     ± 12.773  ops/s
CounterBenchmark.simpleclientInc                    thrpt   15       6559.120    ± 222.192  ops/s
CounterBenchmark.simpleclientNoLabelsInc            thrpt   15       6345.645    ± 198.482  ops/s
HistogramBenchmark.openTelemetryClassic             thrpt   15        690.369     ± 19.963  ops/s
HistogramBenchmark.openTelemetryExponential         thrpt   15        565.769     ± 14.233  ops/s
HistogramBenchmark.prometheusClassic                thrpt   15       5676.178   ± 2030.872  ops/s
HistogramBenchmark.prometheusNative                 thrpt   15       2940.026    ± 215.868  ops/s
HistogramBenchmark.simpleclient                     thrpt   15       4392.876     ± 70.023  ops/s
TextFormatUtilBenchmark.openMetricsWriteToByteArray  thrpt   15     476054.523   ± 2371.043  ops/s
TextFormatUtilBenchmark.openMetricsWriteToNull      thrpt   15     480866.738   ± 4536.337  ops/s
TextFormatUtilBenchmark.prometheusWriteToByteArray  thrpt   15     482674.132   ± 4919.179  ops/s
TextFormatUtilBenchmark.prometheusWriteToNull       thrpt   15     488409.185   ± 3632.070  ops/s
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
