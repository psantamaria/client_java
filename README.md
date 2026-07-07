# Prometheus Java Client Benchmarks

## Run Information

- **Date:** 2026-07-07T07:19:31Z
- **Commit:** [`4b69f40`](https://github.com/psantamaria/client_java/commit/4b69f40bd4e616d69468ce99dc4323162287a577)
- **JDK:** 25.0.2 (OpenJDK 64-Bit Server VM)
- **Benchmark config:** 3 fork(s), 3 warmup, 5 measurement, 4 threads
- **Hardware:** AMD EPYC 9V74 80-Core Processor, 4 cores, 16 GB RAM
- **OS:** Linux 6.17.0-1018-azure

## Results

### CounterBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusInc | 59.64K | ± 545.13 | ops/s | **fastest** |
| prometheusNoLabelsInc | 50.71K | ± 332.83 | ops/s | 1.2x slower |
| prometheusAdd | 47.97K | ± 417.61 | ops/s | 1.2x slower |
| codahaleIncNoLabels | 44.46K | ± 167.43 | ops/s | 1.3x slower |
| simpleclientNoLabelsInc | 6.10K | ± 110.66 | ops/s | 9.8x slower |
| simpleclientAdd | 6.03K | ± 134.81 | ops/s | 9.9x slower |
| simpleclientInc | 6.00K | ± 156.01 | ops/s | 9.9x slower |
| openTelemetryIncNoLabels | 1.36K | ± 73.16 | ops/s | 44x slower |
| openTelemetryInc | 1.33K | ± 104.04 | ops/s | 45x slower |
| openTelemetryAdd | 1.32K | ± 84.00 | ops/s | 45x slower |

### HistogramBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusClassic | 6.47K | ± 1.57K | ops/s | **fastest** |
| simpleclient | 4.54K | ± 45.71 | ops/s | 1.4x slower |
| prometheusNative | 3.03K | ± 254.47 | ops/s | 2.1x slower |
| openTelemetryClassic | 583.17 | ± 23.41 | ops/s | 11x slower |
| openTelemetryExponential | 514.49 | ± 26.23 | ops/s | 13x slower |

### TextFormatUtilBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusWriteToNull | 538.41K | ± 3.77K | ops/s | **fastest** |
| prometheusWriteToByteArray | 526.12K | ± 4.39K | ops/s | 1.0x slower |
| openMetricsWriteToNull | 512.43K | ± 6.47K | ops/s | 1.1x slower |
| openMetricsWriteToByteArray | 498.08K | ± 4.25K | ops/s | 1.1x slower |

### Raw Results

```
Benchmark                                            Mode  Cnt          Score        Error  Units
CounterBenchmark.codahaleIncNoLabels                thrpt   15      44461.451    ± 167.426  ops/s
CounterBenchmark.openTelemetryAdd                   thrpt   15       1321.772     ± 83.998  ops/s
CounterBenchmark.openTelemetryInc                   thrpt   15       1331.295    ± 104.035  ops/s
CounterBenchmark.openTelemetryIncNoLabels           thrpt   15       1359.438     ± 73.156  ops/s
CounterBenchmark.prometheusAdd                      thrpt   15      47973.933    ± 417.606  ops/s
CounterBenchmark.prometheusInc                      thrpt   15      59641.743    ± 545.131  ops/s
CounterBenchmark.prometheusNoLabelsInc              thrpt   15      50707.637    ± 332.826  ops/s
CounterBenchmark.simpleclientAdd                    thrpt   15       6025.610    ± 134.813  ops/s
CounterBenchmark.simpleclientInc                    thrpt   15       5997.947    ± 156.006  ops/s
CounterBenchmark.simpleclientNoLabelsInc            thrpt   15       6096.516    ± 110.660  ops/s
HistogramBenchmark.openTelemetryClassic             thrpt   15        583.166     ± 23.409  ops/s
HistogramBenchmark.openTelemetryExponential         thrpt   15        514.494     ± 26.227  ops/s
HistogramBenchmark.prometheusClassic                thrpt   15       6469.214   ± 1568.854  ops/s
HistogramBenchmark.prometheusNative                 thrpt   15       3025.813    ± 254.465  ops/s
HistogramBenchmark.simpleclient                     thrpt   15       4541.961     ± 45.706  ops/s
TextFormatUtilBenchmark.openMetricsWriteToByteArray  thrpt   15     498083.953   ± 4250.510  ops/s
TextFormatUtilBenchmark.openMetricsWriteToNull      thrpt   15     512427.798   ± 6474.341  ops/s
TextFormatUtilBenchmark.prometheusWriteToByteArray  thrpt   15     526120.015   ± 4389.473  ops/s
TextFormatUtilBenchmark.prometheusWriteToNull       thrpt   15     538407.644   ± 3774.339  ops/s
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
