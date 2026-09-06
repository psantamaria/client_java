# Prometheus Java Client Benchmarks

## Run Information

- **Date:** 2026-09-06T08:01:44Z
- **Commit:** [`4b69f40`](https://github.com/psantamaria/client_java/commit/4b69f40bd4e616d69468ce99dc4323162287a577)
- **JDK:** 25.0.2 (OpenJDK 64-Bit Server VM)
- **Benchmark config:** 3 fork(s), 3 warmup, 5 measurement, 4 threads
- **Hardware:** AMD EPYC 7763 64-Core Processor, 4 cores, 16 GB RAM
- **OS:** Linux 6.17.0-1022-azure

## Results

### CounterBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusInc | 64.03K | ± 631.82 | ops/s | **fastest** |
| prometheusNoLabelsInc | 57.24K | ± 147.66 | ops/s | 1.1x slower |
| prometheusAdd | 50.74K | ± 774.52 | ops/s | 1.3x slower |
| codahaleIncNoLabels | 48.65K | ± 1.90K | ops/s | 1.3x slower |
| simpleclientInc | 6.66K | ± 79.40 | ops/s | 9.6x slower |
| simpleclientNoLabelsInc | 6.59K | ± 34.28 | ops/s | 9.7x slower |
| simpleclientAdd | 6.13K | ± 254.64 | ops/s | 10x slower |
| openTelemetryInc | 1.49K | ± 205.44 | ops/s | 43x slower |
| openTelemetryIncNoLabels | 1.30K | ± 105.17 | ops/s | 49x slower |
| openTelemetryAdd | 1.29K | ± 44.15 | ops/s | 50x slower |

### HistogramBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusClassic | 6.34K | ± 1.23K | ops/s | **fastest** |
| simpleclient | 4.44K | ± 46.36 | ops/s | 1.4x slower |
| prometheusNative | 3.06K | ± 307.92 | ops/s | 2.1x slower |
| openTelemetryClassic | 682.09 | ± 22.41 | ops/s | 9.3x slower |
| openTelemetryExponential | 591.83 | ± 35.44 | ops/s | 11x slower |

### TextFormatUtilBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusWriteToNull | 496.89K | ± 3.52K | ops/s | **fastest** |
| openMetricsWriteToNull | 494.42K | ± 1.46K | ops/s | 1.0x slower |
| prometheusWriteToByteArray | 494.16K | ± 5.99K | ops/s | 1.0x slower |
| openMetricsWriteToByteArray | 485.49K | ± 2.89K | ops/s | 1.0x slower |

### Raw Results

```
Benchmark                                            Mode  Cnt          Score        Error  Units
CounterBenchmark.codahaleIncNoLabels                thrpt   15      48646.901   ± 1904.858  ops/s
CounterBenchmark.openTelemetryAdd                   thrpt   15       1291.161     ± 44.145  ops/s
CounterBenchmark.openTelemetryInc                   thrpt   15       1492.502    ± 205.440  ops/s
CounterBenchmark.openTelemetryIncNoLabels           thrpt   15       1301.546    ± 105.168  ops/s
CounterBenchmark.prometheusAdd                      thrpt   15      50740.520    ± 774.519  ops/s
CounterBenchmark.prometheusInc                      thrpt   15      64028.172    ± 631.818  ops/s
CounterBenchmark.prometheusNoLabelsInc              thrpt   15      57236.684    ± 147.657  ops/s
CounterBenchmark.simpleclientAdd                    thrpt   15       6133.137    ± 254.637  ops/s
CounterBenchmark.simpleclientInc                    thrpt   15       6660.618     ± 79.396  ops/s
CounterBenchmark.simpleclientNoLabelsInc            thrpt   15       6591.315     ± 34.285  ops/s
HistogramBenchmark.openTelemetryClassic             thrpt   15        682.092     ± 22.414  ops/s
HistogramBenchmark.openTelemetryExponential         thrpt   15        591.827     ± 35.438  ops/s
HistogramBenchmark.prometheusClassic                thrpt   15       6339.932   ± 1234.622  ops/s
HistogramBenchmark.prometheusNative                 thrpt   15       3062.821    ± 307.917  ops/s
HistogramBenchmark.simpleclient                     thrpt   15       4439.456     ± 46.361  ops/s
TextFormatUtilBenchmark.openMetricsWriteToByteArray  thrpt   15     485486.022   ± 2893.325  ops/s
TextFormatUtilBenchmark.openMetricsWriteToNull      thrpt   15     494416.372   ± 1457.262  ops/s
TextFormatUtilBenchmark.prometheusWriteToByteArray  thrpt   15     494162.628   ± 5992.966  ops/s
TextFormatUtilBenchmark.prometheusWriteToNull       thrpt   15     496885.826   ± 3522.898  ops/s
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
