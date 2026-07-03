# Prometheus Java Client Benchmarks

## Run Information

- **Date:** 2026-07-03T07:04:48Z
- **Commit:** [`4b69f40`](https://github.com/psantamaria/client_java/commit/4b69f40bd4e616d69468ce99dc4323162287a577)
- **JDK:** 25.0.2 (OpenJDK 64-Bit Server VM)
- **Benchmark config:** 3 fork(s), 3 warmup, 5 measurement, 4 threads
- **Hardware:** AMD EPYC 7763 64-Core Processor, 4 cores, 16 GB RAM
- **OS:** Linux 6.17.0-1018-azure

## Results

### CounterBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusInc | 65.78K | ± 1.22K | ops/s | **fastest** |
| prometheusNoLabelsInc | 56.76K | ± 360.28 | ops/s | 1.2x slower |
| prometheusAdd | 51.43K | ± 242.29 | ops/s | 1.3x slower |
| codahaleIncNoLabels | 49.90K | ± 2.09K | ops/s | 1.3x slower |
| simpleclientInc | 6.57K | ± 100.89 | ops/s | 10x slower |
| simpleclientNoLabelsInc | 6.52K | ± 132.99 | ops/s | 10x slower |
| simpleclientAdd | 6.04K | ± 69.29 | ops/s | 11x slower |
| openTelemetryInc | 1.30K | ± 32.72 | ops/s | 50x slower |
| openTelemetryIncNoLabels | 1.25K | ± 20.39 | ops/s | 52x slower |
| openTelemetryAdd | 1.24K | ± 83.41 | ops/s | 53x slower |

### HistogramBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusClassic | 5.49K | ± 1.22K | ops/s | **fastest** |
| simpleclient | 4.44K | ± 42.31 | ops/s | 1.2x slower |
| prometheusNative | 2.96K | ± 101.22 | ops/s | 1.9x slower |
| openTelemetryClassic | 689.55 | ± 33.84 | ops/s | 8.0x slower |
| openTelemetryExponential | 580.69 | ± 45.27 | ops/s | 9.5x slower |

### TextFormatUtilBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusWriteToNull | 495.88K | ± 3.05K | ops/s | **fastest** |
| prometheusWriteToByteArray | 486.86K | ± 3.84K | ops/s | 1.0x slower |
| openMetricsWriteToNull | 486.76K | ± 3.26K | ops/s | 1.0x slower |
| openMetricsWriteToByteArray | 475.11K | ± 4.87K | ops/s | 1.0x slower |

### Raw Results

```
Benchmark                                            Mode  Cnt          Score        Error  Units
CounterBenchmark.codahaleIncNoLabels                thrpt   15      49902.126   ± 2094.245  ops/s
CounterBenchmark.openTelemetryAdd                   thrpt   15       1235.899     ± 83.407  ops/s
CounterBenchmark.openTelemetryInc                   thrpt   15       1302.877     ± 32.716  ops/s
CounterBenchmark.openTelemetryIncNoLabels           thrpt   15       1252.957     ± 20.390  ops/s
CounterBenchmark.prometheusAdd                      thrpt   15      51428.354    ± 242.294  ops/s
CounterBenchmark.prometheusInc                      thrpt   15      65777.425   ± 1218.142  ops/s
CounterBenchmark.prometheusNoLabelsInc              thrpt   15      56756.624    ± 360.281  ops/s
CounterBenchmark.simpleclientAdd                    thrpt   15       6042.561     ± 69.294  ops/s
CounterBenchmark.simpleclientInc                    thrpt   15       6573.221    ± 100.887  ops/s
CounterBenchmark.simpleclientNoLabelsInc            thrpt   15       6523.306    ± 132.993  ops/s
HistogramBenchmark.openTelemetryClassic             thrpt   15        689.550     ± 33.836  ops/s
HistogramBenchmark.openTelemetryExponential         thrpt   15        580.687     ± 45.270  ops/s
HistogramBenchmark.prometheusClassic                thrpt   15       5493.269   ± 1218.394  ops/s
HistogramBenchmark.prometheusNative                 thrpt   15       2956.645    ± 101.224  ops/s
HistogramBenchmark.simpleclient                     thrpt   15       4444.261     ± 42.306  ops/s
TextFormatUtilBenchmark.openMetricsWriteToByteArray  thrpt   15     475114.525   ± 4867.538  ops/s
TextFormatUtilBenchmark.openMetricsWriteToNull      thrpt   15     486759.153   ± 3255.893  ops/s
TextFormatUtilBenchmark.prometheusWriteToByteArray  thrpt   15     486860.183   ± 3842.065  ops/s
TextFormatUtilBenchmark.prometheusWriteToNull       thrpt   15     495883.697   ± 3050.271  ops/s
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
