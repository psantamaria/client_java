# Prometheus Java Client Benchmarks

## Run Information

- **Date:** 2026-09-18T08:13:35Z
- **Commit:** [`4b69f40`](https://github.com/psantamaria/client_java/commit/4b69f40bd4e616d69468ce99dc4323162287a577)
- **JDK:** 25.0.2 (OpenJDK 64-Bit Server VM)
- **Benchmark config:** 3 fork(s), 3 warmup, 5 measurement, 4 threads
- **Hardware:** AMD EPYC 9V74 80-Core Processor, 4 cores, 16 GB RAM
- **OS:** Linux 6.17.0-1022-azure

## Results

### CounterBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusInc | 74.79K | ± 3.88K | ops/s | **fastest** |
| prometheusNoLabelsInc | 67.35K | ± 491.68 | ops/s | 1.1x slower |
| prometheusAdd | 62.28K | ± 382.66 | ops/s | 1.2x slower |
| codahaleIncNoLabels | 56.59K | ± 576.14 | ops/s | 1.3x slower |
| simpleclientInc | 7.82K | ± 25.71 | ops/s | 9.6x slower |
| simpleclientAdd | 7.75K | ± 185.43 | ops/s | 9.7x slower |
| simpleclientNoLabelsInc | 7.61K | ± 217.62 | ops/s | 9.8x slower |
| openTelemetryAdd | 1.76K | ± 80.61 | ops/s | 43x slower |
| openTelemetryIncNoLabels | 1.73K | ± 127.82 | ops/s | 43x slower |
| openTelemetryInc | 1.71K | ± 118.42 | ops/s | 44x slower |

### HistogramBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| simpleclient | 5.65K | ± 31.83 | ops/s | **fastest** |
| prometheusClassic | 5.31K | ± 576.90 | ops/s | 1.1x slower |
| prometheusNative | 4.09K | ± 36.85 | ops/s | 1.4x slower |
| openTelemetryClassic | 753.07 | ± 12.80 | ops/s | 7.5x slower |
| openTelemetryExponential | 660.59 | ± 21.63 | ops/s | 8.6x slower |

### TextFormatUtilBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusWriteToNull | 676.31K | ± 4.25K | ops/s | **fastest** |
| prometheusWriteToByteArray | 661.65K | ± 4.91K | ops/s | 1.0x slower |
| openMetricsWriteToNull | 645.63K | ± 3.39K | ops/s | 1.0x slower |
| openMetricsWriteToByteArray | 637.44K | ± 5.16K | ops/s | 1.1x slower |

### Raw Results

```
Benchmark                                            Mode  Cnt          Score        Error  Units
CounterBenchmark.codahaleIncNoLabels                thrpt   15      56589.623    ± 576.138  ops/s
CounterBenchmark.openTelemetryAdd                   thrpt   15       1759.829     ± 80.608  ops/s
CounterBenchmark.openTelemetryInc                   thrpt   15       1709.515    ± 118.420  ops/s
CounterBenchmark.openTelemetryIncNoLabels           thrpt   15       1728.898    ± 127.819  ops/s
CounterBenchmark.prometheusAdd                      thrpt   15      62284.579    ± 382.657  ops/s
CounterBenchmark.prometheusInc                      thrpt   15      74794.362   ± 3876.640  ops/s
CounterBenchmark.prometheusNoLabelsInc              thrpt   15      67346.129    ± 491.684  ops/s
CounterBenchmark.simpleclientAdd                    thrpt   15       7750.335    ± 185.426  ops/s
CounterBenchmark.simpleclientInc                    thrpt   15       7816.035     ± 25.706  ops/s
CounterBenchmark.simpleclientNoLabelsInc            thrpt   15       7611.556    ± 217.625  ops/s
HistogramBenchmark.openTelemetryClassic             thrpt   15        753.071     ± 12.802  ops/s
HistogramBenchmark.openTelemetryExponential         thrpt   15        660.585     ± 21.631  ops/s
HistogramBenchmark.prometheusClassic                thrpt   15       5305.266    ± 576.902  ops/s
HistogramBenchmark.prometheusNative                 thrpt   15       4094.119     ± 36.855  ops/s
HistogramBenchmark.simpleclient                     thrpt   15       5649.074     ± 31.825  ops/s
TextFormatUtilBenchmark.openMetricsWriteToByteArray  thrpt   15     637439.580   ± 5157.913  ops/s
TextFormatUtilBenchmark.openMetricsWriteToNull      thrpt   15     645634.518   ± 3386.787  ops/s
TextFormatUtilBenchmark.prometheusWriteToByteArray  thrpt   15     661653.416   ± 4914.244  ops/s
TextFormatUtilBenchmark.prometheusWriteToNull       thrpt   15     676312.373   ± 4253.773  ops/s
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
