# Prometheus Java Client Benchmarks

## Run Information

- **Date:** 2026-06-05T07:33:49Z
- **Commit:** [`4b69f40`](https://github.com/psantamaria/client_java/commit/4b69f40bd4e616d69468ce99dc4323162287a577)
- **JDK:** 25.0.2 (OpenJDK 64-Bit Server VM)
- **Benchmark config:** 3 fork(s), 3 warmup, 5 measurement, 4 threads
- **Hardware:** AMD EPYC 9V74 80-Core Processor, 4 cores, 16 GB RAM
- **OS:** Linux 6.17.0-1015-azure

## Results

### CounterBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusInc | 59.69K | ± 252.14 | ops/s | **fastest** |
| prometheusNoLabelsInc | 50.94K | ± 78.40 | ops/s | 1.2x slower |
| prometheusAdd | 47.60K | ± 832.79 | ops/s | 1.3x slower |
| codahaleIncNoLabels | 44.38K | ± 857.91 | ops/s | 1.3x slower |
| simpleclientInc | 6.33K | ± 42.54 | ops/s | 9.4x slower |
| simpleclientNoLabelsInc | 6.12K | ± 233.97 | ops/s | 9.8x slower |
| simpleclientAdd | 5.87K | ± 270.63 | ops/s | 10x slower |
| openTelemetryAdd | 1.49K | ± 105.68 | ops/s | 40x slower |
| openTelemetryInc | 1.37K | ± 14.61 | ops/s | 44x slower |
| openTelemetryIncNoLabels | 1.35K | ± 53.16 | ops/s | 44x slower |

### HistogramBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusClassic | 4.80K | ± 1.05K | ops/s | **fastest** |
| simpleclient | 4.56K | ± 74.80 | ops/s | 1.1x slower |
| prometheusNative | 2.94K | ± 205.77 | ops/s | 1.6x slower |
| openTelemetryClassic | 621.71 | ± 27.10 | ops/s | 7.7x slower |
| openTelemetryExponential | 517.43 | ± 30.88 | ops/s | 9.3x slower |

### TextFormatUtilBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusWriteToNull | 556.20K | ± 5.32K | ops/s | **fastest** |
| prometheusWriteToByteArray | 545.89K | ± 4.94K | ops/s | 1.0x slower |
| openMetricsWriteToNull | 534.69K | ± 2.80K | ops/s | 1.0x slower |
| openMetricsWriteToByteArray | 528.30K | ± 4.69K | ops/s | 1.1x slower |

### Raw Results

```
Benchmark                                            Mode  Cnt          Score        Error  Units
CounterBenchmark.codahaleIncNoLabels                thrpt   15      44377.165    ± 857.913  ops/s
CounterBenchmark.openTelemetryAdd                   thrpt   15       1493.701    ± 105.676  ops/s
CounterBenchmark.openTelemetryInc                   thrpt   15       1366.899     ± 14.608  ops/s
CounterBenchmark.openTelemetryIncNoLabels           thrpt   15       1351.110     ± 53.157  ops/s
CounterBenchmark.prometheusAdd                      thrpt   15      47599.328    ± 832.793  ops/s
CounterBenchmark.prometheusInc                      thrpt   15      59692.212    ± 252.137  ops/s
CounterBenchmark.prometheusNoLabelsInc              thrpt   15      50935.230     ± 78.401  ops/s
CounterBenchmark.simpleclientAdd                    thrpt   15       5869.284    ± 270.626  ops/s
CounterBenchmark.simpleclientInc                    thrpt   15       6325.614     ± 42.536  ops/s
CounterBenchmark.simpleclientNoLabelsInc            thrpt   15       6115.350    ± 233.967  ops/s
HistogramBenchmark.openTelemetryClassic             thrpt   15        621.713     ± 27.102  ops/s
HistogramBenchmark.openTelemetryExponential         thrpt   15        517.434     ± 30.883  ops/s
HistogramBenchmark.prometheusClassic                thrpt   15       4795.200   ± 1048.451  ops/s
HistogramBenchmark.prometheusNative                 thrpt   15       2942.823    ± 205.766  ops/s
HistogramBenchmark.simpleclient                     thrpt   15       4558.415     ± 74.800  ops/s
TextFormatUtilBenchmark.openMetricsWriteToByteArray  thrpt   15     528299.534   ± 4692.261  ops/s
TextFormatUtilBenchmark.openMetricsWriteToNull      thrpt   15     534692.983   ± 2796.390  ops/s
TextFormatUtilBenchmark.prometheusWriteToByteArray  thrpt   15     545894.094   ± 4936.562  ops/s
TextFormatUtilBenchmark.prometheusWriteToNull       thrpt   15     556201.404   ± 5320.500  ops/s
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
