# Prometheus Java Client Benchmarks

## Run Information

- **Date:** 2026-05-17T07:01:00Z
- **Commit:** [`4b69f40`](https://github.com/psantamaria/client_java/commit/4b69f40bd4e616d69468ce99dc4323162287a577)
- **JDK:** 25.0.2 (OpenJDK 64-Bit Server VM)
- **Benchmark config:** 3 fork(s), 3 warmup, 5 measurement, 4 threads
- **Hardware:** AMD EPYC 9V74 80-Core Processor, 4 cores, 16 GB RAM
- **OS:** Linux 6.17.0-1013-azure

## Results

### CounterBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusInc | 60.85K | ± 857.28 | ops/s | **fastest** |
| prometheusNoLabelsInc | 51.86K | ± 831.11 | ops/s | 1.2x slower |
| prometheusAdd | 48.25K | ± 1.20K | ops/s | 1.3x slower |
| codahaleIncNoLabels | 44.12K | ± 307.16 | ops/s | 1.4x slower |
| simpleclientInc | 6.23K | ± 108.68 | ops/s | 9.8x slower |
| simpleclientNoLabelsInc | 6.01K | ± 210.39 | ops/s | 10x slower |
| simpleclientAdd | 5.79K | ± 322.67 | ops/s | 11x slower |
| openTelemetryInc | 1.28K | ± 17.32 | ops/s | 48x slower |
| openTelemetryIncNoLabels | 1.25K | ± 74.93 | ops/s | 49x slower |
| openTelemetryAdd | 1.25K | ± 4.64 | ops/s | 49x slower |

### HistogramBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusClassic | 6.35K | ± 1.24K | ops/s | **fastest** |
| simpleclient | 4.18K | ± 15.48 | ops/s | 1.5x slower |
| prometheusNative | 2.93K | ± 246.97 | ops/s | 2.2x slower |
| openTelemetryClassic | 620.48 | ± 22.02 | ops/s | 10x slower |
| openTelemetryExponential | 519.84 | ± 19.63 | ops/s | 12x slower |

### TextFormatUtilBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusWriteToNull | 541.29K | ± 5.12K | ops/s | **fastest** |
| prometheusWriteToByteArray | 520.17K | ± 3.23K | ops/s | 1.0x slower |
| openMetricsWriteToNull | 515.71K | ± 7.38K | ops/s | 1.0x slower |
| openMetricsWriteToByteArray | 507.19K | ± 7.13K | ops/s | 1.1x slower |

### Raw Results

```
Benchmark                                            Mode  Cnt          Score        Error  Units
CounterBenchmark.codahaleIncNoLabels                thrpt   15      44117.084    ± 307.163  ops/s
CounterBenchmark.openTelemetryAdd                   thrpt   15       1245.018      ± 4.645  ops/s
CounterBenchmark.openTelemetryInc                   thrpt   15       1278.682     ± 17.318  ops/s
CounterBenchmark.openTelemetryIncNoLabels           thrpt   15       1254.529     ± 74.927  ops/s
CounterBenchmark.prometheusAdd                      thrpt   15      48249.409   ± 1197.121  ops/s
CounterBenchmark.prometheusInc                      thrpt   15      60847.260    ± 857.285  ops/s
CounterBenchmark.prometheusNoLabelsInc              thrpt   15      51858.976    ± 831.113  ops/s
CounterBenchmark.simpleclientAdd                    thrpt   15       5789.044    ± 322.674  ops/s
CounterBenchmark.simpleclientInc                    thrpt   15       6233.870    ± 108.685  ops/s
CounterBenchmark.simpleclientNoLabelsInc            thrpt   15       6007.234    ± 210.389  ops/s
HistogramBenchmark.openTelemetryClassic             thrpt   15        620.482     ± 22.025  ops/s
HistogramBenchmark.openTelemetryExponential         thrpt   15        519.843     ± 19.629  ops/s
HistogramBenchmark.prometheusClassic                thrpt   15       6349.033   ± 1236.481  ops/s
HistogramBenchmark.prometheusNative                 thrpt   15       2925.821    ± 246.974  ops/s
HistogramBenchmark.simpleclient                     thrpt   15       4177.816     ± 15.482  ops/s
TextFormatUtilBenchmark.openMetricsWriteToByteArray  thrpt   15     507193.742   ± 7129.055  ops/s
TextFormatUtilBenchmark.openMetricsWriteToNull      thrpt   15     515710.407   ± 7375.484  ops/s
TextFormatUtilBenchmark.prometheusWriteToByteArray  thrpt   15     520166.770   ± 3230.504  ops/s
TextFormatUtilBenchmark.prometheusWriteToNull       thrpt   15     541285.434   ± 5115.510  ops/s
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
