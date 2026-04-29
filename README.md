# Prometheus Java Client Benchmarks

## Run Information

- **Date:** 2026-04-29T06:39:42Z
- **Commit:** [`4b69f40`](https://github.com/psantamaria/client_java/commit/4b69f40bd4e616d69468ce99dc4323162287a577)
- **JDK:** 25.0.2 (OpenJDK 64-Bit Server VM)
- **Benchmark config:** 3 fork(s), 3 warmup, 5 measurement, 4 threads
- **Hardware:** AMD EPYC 7763 64-Core Processor, 4 cores, 16 GB RAM
- **OS:** Linux 6.17.0-1010-azure

## Results

### CounterBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusInc | 66.95K | ± 331.01 | ops/s | **fastest** |
| prometheusNoLabelsInc | 57.00K | ± 76.73 | ops/s | 1.2x slower |
| prometheusAdd | 51.54K | ± 160.08 | ops/s | 1.3x slower |
| codahaleIncNoLabels | 46.71K | ± 685.28 | ops/s | 1.4x slower |
| simpleclientInc | 6.70K | ± 17.41 | ops/s | 10.0x slower |
| simpleclientNoLabelsInc | 6.52K | ± 147.14 | ops/s | 10x slower |
| simpleclientAdd | 6.15K | ± 280.93 | ops/s | 11x slower |
| openTelemetryAdd | 1.31K | ± 40.83 | ops/s | 51x slower |
| openTelemetryIncNoLabels | 1.30K | ± 180.52 | ops/s | 52x slower |
| openTelemetryInc | 1.26K | ± 21.51 | ops/s | 53x slower |

### HistogramBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusClassic | 5.06K | ± 1.71K | ops/s | **fastest** |
| simpleclient | 4.43K | ± 57.41 | ops/s | 1.1x slower |
| prometheusNative | 2.64K | ± 98.01 | ops/s | 1.9x slower |
| openTelemetryClassic | 712.99 | ± 23.95 | ops/s | 7.1x slower |
| openTelemetryExponential | 557.26 | ± 26.04 | ops/s | 9.1x slower |

### TextFormatUtilBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusWriteToNull | 475.70K | ± 2.84K | ops/s | **fastest** |
| prometheusWriteToByteArray | 472.46K | ± 4.30K | ops/s | 1.0x slower |
| openMetricsWriteToNull | 463.68K | ± 2.18K | ops/s | 1.0x slower |
| openMetricsWriteToByteArray | 459.26K | ± 2.30K | ops/s | 1.0x slower |

### Raw Results

```
Benchmark                                            Mode  Cnt          Score        Error  Units
CounterBenchmark.codahaleIncNoLabels                thrpt   15      46707.967    ± 685.276  ops/s
CounterBenchmark.openTelemetryAdd                   thrpt   15       1311.818     ± 40.834  ops/s
CounterBenchmark.openTelemetryInc                   thrpt   15       1259.638     ± 21.508  ops/s
CounterBenchmark.openTelemetryIncNoLabels           thrpt   15       1296.891    ± 180.525  ops/s
CounterBenchmark.prometheusAdd                      thrpt   15      51540.497    ± 160.075  ops/s
CounterBenchmark.prometheusInc                      thrpt   15      66945.009    ± 331.008  ops/s
CounterBenchmark.prometheusNoLabelsInc              thrpt   15      57002.665     ± 76.733  ops/s
CounterBenchmark.simpleclientAdd                    thrpt   15       6154.386    ± 280.928  ops/s
CounterBenchmark.simpleclientInc                    thrpt   15       6695.953     ± 17.410  ops/s
CounterBenchmark.simpleclientNoLabelsInc            thrpt   15       6523.083    ± 147.140  ops/s
HistogramBenchmark.openTelemetryClassic             thrpt   15        712.985     ± 23.946  ops/s
HistogramBenchmark.openTelemetryExponential         thrpt   15        557.259     ± 26.035  ops/s
HistogramBenchmark.prometheusClassic                thrpt   15       5058.138   ± 1710.305  ops/s
HistogramBenchmark.prometheusNative                 thrpt   15       2644.898     ± 98.007  ops/s
HistogramBenchmark.simpleclient                     thrpt   15       4433.808     ± 57.409  ops/s
TextFormatUtilBenchmark.openMetricsWriteToByteArray  thrpt   15     459256.108   ± 2297.121  ops/s
TextFormatUtilBenchmark.openMetricsWriteToNull      thrpt   15     463677.528   ± 2183.120  ops/s
TextFormatUtilBenchmark.prometheusWriteToByteArray  thrpt   15     472459.213   ± 4304.044  ops/s
TextFormatUtilBenchmark.prometheusWriteToNull       thrpt   15     475704.327   ± 2838.340  ops/s
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
