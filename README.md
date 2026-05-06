# Prometheus Java Client Benchmarks

## Run Information

- **Date:** 2026-05-06T06:41:48Z
- **Commit:** [`4b69f40`](https://github.com/psantamaria/client_java/commit/4b69f40bd4e616d69468ce99dc4323162287a577)
- **JDK:** 25.0.2 (OpenJDK 64-Bit Server VM)
- **Benchmark config:** 3 fork(s), 3 warmup, 5 measurement, 4 threads
- **Hardware:** AMD EPYC 9V74 80-Core Processor, 4 cores, 16 GB RAM
- **OS:** Linux 6.17.0-1010-azure

## Results

### CounterBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusInc | 59.57K | ± 1.45K | ops/s | **fastest** |
| prometheusNoLabelsInc | 51.39K | ± 575.83 | ops/s | 1.2x slower |
| prometheusAdd | 47.72K | ± 217.06 | ops/s | 1.2x slower |
| codahaleIncNoLabels | 44.33K | ± 167.20 | ops/s | 1.3x slower |
| simpleclientInc | 6.16K | ± 76.12 | ops/s | 9.7x slower |
| simpleclientNoLabelsInc | 6.11K | ± 254.19 | ops/s | 9.7x slower |
| simpleclientAdd | 5.82K | ± 6.92 | ops/s | 10x slower |
| openTelemetryAdd | 1.34K | ± 40.39 | ops/s | 44x slower |
| openTelemetryIncNoLabels | 1.27K | ± 53.16 | ops/s | 47x slower |
| openTelemetryInc | 1.27K | ± 43.54 | ops/s | 47x slower |

### HistogramBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusClassic | 5.67K | ± 1.36K | ops/s | **fastest** |
| simpleclient | 4.38K | ± 52.95 | ops/s | 1.3x slower |
| prometheusNative | 3.11K | ± 132.86 | ops/s | 1.8x slower |
| openTelemetryClassic | 610.37 | ± 13.85 | ops/s | 9.3x slower |
| openTelemetryExponential | 488.78 | ± 6.99 | ops/s | 12x slower |

### TextFormatUtilBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusWriteToNull | 555.11K | ± 4.06K | ops/s | **fastest** |
| prometheusWriteToByteArray | 539.69K | ± 6.08K | ops/s | 1.0x slower |
| openMetricsWriteToNull | 534.91K | ± 3.36K | ops/s | 1.0x slower |
| openMetricsWriteToByteArray | 524.90K | ± 2.66K | ops/s | 1.1x slower |

### Raw Results

```
Benchmark                                            Mode  Cnt          Score        Error  Units
CounterBenchmark.codahaleIncNoLabels                thrpt   15      44325.293    ± 167.203  ops/s
CounterBenchmark.openTelemetryAdd                   thrpt   15       1343.593     ± 40.386  ops/s
CounterBenchmark.openTelemetryInc                   thrpt   15       1270.821     ± 43.542  ops/s
CounterBenchmark.openTelemetryIncNoLabels           thrpt   15       1273.033     ± 53.157  ops/s
CounterBenchmark.prometheusAdd                      thrpt   15      47721.213    ± 217.064  ops/s
CounterBenchmark.prometheusInc                      thrpt   15      59574.143   ± 1454.339  ops/s
CounterBenchmark.prometheusNoLabelsInc              thrpt   15      51393.972    ± 575.832  ops/s
CounterBenchmark.simpleclientAdd                    thrpt   15       5822.402      ± 6.917  ops/s
CounterBenchmark.simpleclientInc                    thrpt   15       6157.705     ± 76.117  ops/s
CounterBenchmark.simpleclientNoLabelsInc            thrpt   15       6113.139    ± 254.190  ops/s
HistogramBenchmark.openTelemetryClassic             thrpt   15        610.367     ± 13.846  ops/s
HistogramBenchmark.openTelemetryExponential         thrpt   15        488.781      ± 6.986  ops/s
HistogramBenchmark.prometheusClassic                thrpt   15       5666.515   ± 1363.065  ops/s
HistogramBenchmark.prometheusNative                 thrpt   15       3110.352    ± 132.858  ops/s
HistogramBenchmark.simpleclient                     thrpt   15       4375.139     ± 52.945  ops/s
TextFormatUtilBenchmark.openMetricsWriteToByteArray  thrpt   15     524897.855   ± 2659.324  ops/s
TextFormatUtilBenchmark.openMetricsWriteToNull      thrpt   15     534912.561   ± 3362.339  ops/s
TextFormatUtilBenchmark.prometheusWriteToByteArray  thrpt   15     539693.269   ± 6077.112  ops/s
TextFormatUtilBenchmark.prometheusWriteToNull       thrpt   15     555107.454   ± 4055.620  ops/s
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
