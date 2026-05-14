# Prometheus Java Client Benchmarks

## Run Information

- **Date:** 2026-05-14T07:00:28Z
- **Commit:** [`4b69f40`](https://github.com/psantamaria/client_java/commit/4b69f40bd4e616d69468ce99dc4323162287a577)
- **JDK:** 25.0.2 (OpenJDK 64-Bit Server VM)
- **Benchmark config:** 3 fork(s), 3 warmup, 5 measurement, 4 threads
- **Hardware:** AMD EPYC 7763 64-Core Processor, 4 cores, 16 GB RAM
- **OS:** Linux 6.17.0-1010-azure

## Results

### CounterBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusInc | 65.27K | ± 1.34K | ops/s | **fastest** |
| prometheusNoLabelsInc | 55.76K | ± 869.48 | ops/s | 1.2x slower |
| prometheusAdd | 50.01K | ± 1.27K | ops/s | 1.3x slower |
| codahaleIncNoLabels | 49.62K | ± 696.68 | ops/s | 1.3x slower |
| simpleclientInc | 6.70K | ± 16.46 | ops/s | 9.7x slower |
| simpleclientNoLabelsInc | 6.51K | ± 137.74 | ops/s | 10x slower |
| simpleclientAdd | 6.22K | ± 217.20 | ops/s | 10x slower |
| openTelemetryAdd | 1.39K | ± 143.68 | ops/s | 47x slower |
| openTelemetryInc | 1.36K | ± 215.97 | ops/s | 48x slower |
| openTelemetryIncNoLabels | 1.18K | ± 61.83 | ops/s | 55x slower |

### HistogramBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusClassic | 7.06K | ± 1.01K | ops/s | **fastest** |
| simpleclient | 4.41K | ± 45.95 | ops/s | 1.6x slower |
| prometheusNative | 2.82K | ± 318.82 | ops/s | 2.5x slower |
| openTelemetryClassic | 691.64 | ± 47.12 | ops/s | 10x slower |
| openTelemetryExponential | 571.46 | ± 36.87 | ops/s | 12x slower |

### TextFormatUtilBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusWriteToNull | 484.63K | ± 3.35K | ops/s | **fastest** |
| prometheusWriteToByteArray | 480.77K | ± 2.24K | ops/s | 1.0x slower |
| openMetricsWriteToByteArray | 469.70K | ± 4.74K | ops/s | 1.0x slower |
| openMetricsWriteToNull | 469.42K | ± 7.31K | ops/s | 1.0x slower |

### Raw Results

```
Benchmark                                            Mode  Cnt          Score        Error  Units
CounterBenchmark.codahaleIncNoLabels                thrpt   15      49620.770    ± 696.677  ops/s
CounterBenchmark.openTelemetryAdd                   thrpt   15       1389.671    ± 143.681  ops/s
CounterBenchmark.openTelemetryInc                   thrpt   15       1356.563    ± 215.970  ops/s
CounterBenchmark.openTelemetryIncNoLabels           thrpt   15       1181.545     ± 61.829  ops/s
CounterBenchmark.prometheusAdd                      thrpt   15      50008.768   ± 1268.487  ops/s
CounterBenchmark.prometheusInc                      thrpt   15      65267.345   ± 1335.941  ops/s
CounterBenchmark.prometheusNoLabelsInc              thrpt   15      55757.147    ± 869.478  ops/s
CounterBenchmark.simpleclientAdd                    thrpt   15       6217.202    ± 217.198  ops/s
CounterBenchmark.simpleclientInc                    thrpt   15       6696.073     ± 16.460  ops/s
CounterBenchmark.simpleclientNoLabelsInc            thrpt   15       6512.150    ± 137.739  ops/s
HistogramBenchmark.openTelemetryClassic             thrpt   15        691.641     ± 47.118  ops/s
HistogramBenchmark.openTelemetryExponential         thrpt   15        571.456     ± 36.871  ops/s
HistogramBenchmark.prometheusClassic                thrpt   15       7061.195   ± 1010.700  ops/s
HistogramBenchmark.prometheusNative                 thrpt   15       2818.480    ± 318.821  ops/s
HistogramBenchmark.simpleclient                     thrpt   15       4409.606     ± 45.949  ops/s
TextFormatUtilBenchmark.openMetricsWriteToByteArray  thrpt   15     469695.986   ± 4742.304  ops/s
TextFormatUtilBenchmark.openMetricsWriteToNull      thrpt   15     469415.590   ± 7313.627  ops/s
TextFormatUtilBenchmark.prometheusWriteToByteArray  thrpt   15     480772.256   ± 2243.155  ops/s
TextFormatUtilBenchmark.prometheusWriteToNull       thrpt   15     484630.565   ± 3349.515  ops/s
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
