# Prometheus Java Client Benchmarks

## Run Information

- **Date:** 2026-06-20T07:32:49Z
- **Commit:** [`4b69f40`](https://github.com/psantamaria/client_java/commit/4b69f40bd4e616d69468ce99dc4323162287a577)
- **JDK:** 25.0.2 (OpenJDK 64-Bit Server VM)
- **Benchmark config:** 3 fork(s), 3 warmup, 5 measurement, 4 threads
- **Hardware:** AMD EPYC 7763 64-Core Processor, 4 cores, 16 GB RAM
- **OS:** Linux 6.17.0-1018-azure

## Results

### CounterBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusInc | 64.87K | ± 1.86K | ops/s | **fastest** |
| prometheusNoLabelsInc | 57.08K | ± 98.32 | ops/s | 1.1x slower |
| prometheusAdd | 51.46K | ± 216.42 | ops/s | 1.3x slower |
| codahaleIncNoLabels | 48.35K | ± 1.59K | ops/s | 1.3x slower |
| simpleclientInc | 6.70K | ± 10.56 | ops/s | 9.7x slower |
| simpleclientNoLabelsInc | 6.62K | ± 17.70 | ops/s | 9.8x slower |
| simpleclientAdd | 6.01K | ± 83.31 | ops/s | 11x slower |
| openTelemetryAdd | 1.37K | ± 187.69 | ops/s | 47x slower |
| openTelemetryIncNoLabels | 1.29K | ± 151.76 | ops/s | 50x slower |
| openTelemetryInc | 1.23K | ± 17.33 | ops/s | 53x slower |

### HistogramBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusClassic | 4.96K | ± 602.79 | ops/s | **fastest** |
| simpleclient | 4.48K | ± 70.46 | ops/s | 1.1x slower |
| prometheusNative | 2.70K | ± 59.58 | ops/s | 1.8x slower |
| openTelemetryClassic | 711.58 | ± 20.59 | ops/s | 7.0x slower |
| openTelemetryExponential | 550.62 | ± 25.38 | ops/s | 9.0x slower |

### TextFormatUtilBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| openMetricsWriteToNull | 484.63K | ± 2.23K | ops/s | **fastest** |
| prometheusWriteToNull | 477.15K | ± 15.12K | ops/s | 1.0x slower |
| prometheusWriteToByteArray | 476.68K | ± 9.08K | ops/s | 1.0x slower |
| openMetricsWriteToByteArray | 475.52K | ± 5.09K | ops/s | 1.0x slower |

### Raw Results

```
Benchmark                                            Mode  Cnt          Score        Error  Units
CounterBenchmark.codahaleIncNoLabels                thrpt   15      48349.009   ± 1586.455  ops/s
CounterBenchmark.openTelemetryAdd                   thrpt   15       1366.246    ± 187.687  ops/s
CounterBenchmark.openTelemetryInc                   thrpt   15       1230.143     ± 17.326  ops/s
CounterBenchmark.openTelemetryIncNoLabels           thrpt   15       1287.870    ± 151.758  ops/s
CounterBenchmark.prometheusAdd                      thrpt   15      51457.472    ± 216.418  ops/s
CounterBenchmark.prometheusInc                      thrpt   15      64865.725   ± 1858.013  ops/s
CounterBenchmark.prometheusNoLabelsInc              thrpt   15      57080.260     ± 98.317  ops/s
CounterBenchmark.simpleclientAdd                    thrpt   15       6008.803     ± 83.312  ops/s
CounterBenchmark.simpleclientInc                    thrpt   15       6701.558     ± 10.560  ops/s
CounterBenchmark.simpleclientNoLabelsInc            thrpt   15       6617.966     ± 17.697  ops/s
HistogramBenchmark.openTelemetryClassic             thrpt   15        711.580     ± 20.590  ops/s
HistogramBenchmark.openTelemetryExponential         thrpt   15        550.623     ± 25.379  ops/s
HistogramBenchmark.prometheusClassic                thrpt   15       4960.515    ± 602.794  ops/s
HistogramBenchmark.prometheusNative                 thrpt   15       2700.521     ± 59.581  ops/s
HistogramBenchmark.simpleclient                     thrpt   15       4479.011     ± 70.456  ops/s
TextFormatUtilBenchmark.openMetricsWriteToByteArray  thrpt   15     475521.671   ± 5085.122  ops/s
TextFormatUtilBenchmark.openMetricsWriteToNull      thrpt   15     484632.943   ± 2231.315  ops/s
TextFormatUtilBenchmark.prometheusWriteToByteArray  thrpt   15     476675.217   ± 9083.805  ops/s
TextFormatUtilBenchmark.prometheusWriteToNull       thrpt   15     477152.264  ± 15116.659  ops/s
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
