# Prometheus Java Client Benchmarks

## Run Information

- **Date:** 2026-06-13T07:28:39Z
- **Commit:** [`4b69f40`](https://github.com/psantamaria/client_java/commit/4b69f40bd4e616d69468ce99dc4323162287a577)
- **JDK:** 25.0.2 (OpenJDK 64-Bit Server VM)
- **Benchmark config:** 3 fork(s), 3 warmup, 5 measurement, 4 threads
- **Hardware:** AMD EPYC 7763 64-Core Processor, 4 cores, 16 GB RAM
- **OS:** Linux 6.17.0-1018-azure

## Results

### CounterBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusInc | 66.40K | ± 106.01 | ops/s | **fastest** |
| prometheusNoLabelsInc | 56.75K | ± 311.69 | ops/s | 1.2x slower |
| prometheusAdd | 51.41K | ± 251.42 | ops/s | 1.3x slower |
| codahaleIncNoLabels | 41.22K | ± 14.20K | ops/s | 1.6x slower |
| simpleclientInc | 6.59K | ± 182.86 | ops/s | 10x slower |
| simpleclientNoLabelsInc | 6.41K | ± 173.35 | ops/s | 10x slower |
| simpleclientAdd | 6.06K | ± 348.58 | ops/s | 11x slower |
| openTelemetryInc | 1.31K | ± 21.02 | ops/s | 51x slower |
| openTelemetryIncNoLabels | 1.26K | ± 21.79 | ops/s | 53x slower |
| openTelemetryAdd | 1.22K | ± 41.83 | ops/s | 54x slower |

### HistogramBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusClassic | 5.49K | ± 1.69K | ops/s | **fastest** |
| simpleclient | 4.36K | ± 160.86 | ops/s | 1.3x slower |
| prometheusNative | 3.02K | ± 247.18 | ops/s | 1.8x slower |
| openTelemetryClassic | 711.25 | ± 27.74 | ops/s | 7.7x slower |
| openTelemetryExponential | 597.52 | ± 18.74 | ops/s | 9.2x slower |

### TextFormatUtilBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusWriteToNull | 486.54K | ± 4.19K | ops/s | **fastest** |
| openMetricsWriteToNull | 482.95K | ± 3.74K | ops/s | 1.0x slower |
| prometheusWriteToByteArray | 482.09K | ± 3.52K | ops/s | 1.0x slower |
| openMetricsWriteToByteArray | 476.11K | ± 6.02K | ops/s | 1.0x slower |

### Raw Results

```
Benchmark                                            Mode  Cnt          Score        Error  Units
CounterBenchmark.codahaleIncNoLabels                thrpt   15      41223.921  ± 14199.590  ops/s
CounterBenchmark.openTelemetryAdd                   thrpt   15       1221.862     ± 41.827  ops/s
CounterBenchmark.openTelemetryInc                   thrpt   15       1308.123     ± 21.020  ops/s
CounterBenchmark.openTelemetryIncNoLabels           thrpt   15       1256.408     ± 21.791  ops/s
CounterBenchmark.prometheusAdd                      thrpt   15      51406.852    ± 251.421  ops/s
CounterBenchmark.prometheusInc                      thrpt   15      66396.460    ± 106.006  ops/s
CounterBenchmark.prometheusNoLabelsInc              thrpt   15      56753.148    ± 311.691  ops/s
CounterBenchmark.simpleclientAdd                    thrpt   15       6061.104    ± 348.582  ops/s
CounterBenchmark.simpleclientInc                    thrpt   15       6587.496    ± 182.857  ops/s
CounterBenchmark.simpleclientNoLabelsInc            thrpt   15       6407.183    ± 173.350  ops/s
HistogramBenchmark.openTelemetryClassic             thrpt   15        711.253     ± 27.744  ops/s
HistogramBenchmark.openTelemetryExponential         thrpt   15        597.519     ± 18.738  ops/s
HistogramBenchmark.prometheusClassic                thrpt   15       5494.446   ± 1688.157  ops/s
HistogramBenchmark.prometheusNative                 thrpt   15       3023.570    ± 247.184  ops/s
HistogramBenchmark.simpleclient                     thrpt   15       4356.737    ± 160.860  ops/s
TextFormatUtilBenchmark.openMetricsWriteToByteArray  thrpt   15     476113.327   ± 6022.390  ops/s
TextFormatUtilBenchmark.openMetricsWriteToNull      thrpt   15     482950.712   ± 3743.091  ops/s
TextFormatUtilBenchmark.prometheusWriteToByteArray  thrpt   15     482085.342   ± 3515.375  ops/s
TextFormatUtilBenchmark.prometheusWriteToNull       thrpt   15     486544.055   ± 4187.850  ops/s
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
