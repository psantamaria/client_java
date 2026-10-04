# Prometheus Java Client Benchmarks

## Run Information

- **Date:** 2026-10-04T08:57:20Z
- **Commit:** [`4b69f40`](https://github.com/psantamaria/client_java/commit/4b69f40bd4e616d69468ce99dc4323162287a577)
- **JDK:** 25.0.2 (OpenJDK 64-Bit Server VM)
- **Benchmark config:** 3 fork(s), 3 warmup, 5 measurement, 4 threads
- **Hardware:** AMD EPYC 9V45 96-Core Processor, 4 cores, 16 GB RAM
- **OS:** Linux 6.17.0-1022-azure

## Results

### CounterBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusInc | 66.18K | ± 787.49 | ops/s | **fastest** |
| prometheusNoLabelsInc | 64.86K | ± 538.06 | ops/s | 1.0x slower |
| prometheusAdd | 59.65K | ± 3.39K | ops/s | 1.1x slower |
| codahaleIncNoLabels | 59.55K | ± 118.90 | ops/s | 1.1x slower |
| simpleclientAdd | 10.53K | ± 285.15 | ops/s | 6.3x slower |
| simpleclientInc | 10.25K | ± 464.52 | ops/s | 6.5x slower |
| simpleclientNoLabelsInc | 10.21K | ± 181.72 | ops/s | 6.5x slower |
| openTelemetryIncNoLabels | 2.16K | ± 267.04 | ops/s | 31x slower |
| openTelemetryAdd | 2.07K | ± 392.78 | ops/s | 32x slower |
| openTelemetryInc | 1.98K | ± 131.62 | ops/s | 33x slower |

### HistogramBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| simpleclient | 6.71K | ± 47.91 | ops/s | **fastest** |
| prometheusClassic | 6.63K | ± 860.81 | ops/s | 1.0x slower |
| prometheusNative | 4.93K | ± 339.01 | ops/s | 1.4x slower |
| openTelemetryClassic | 873.28 | ± 21.51 | ops/s | 7.7x slower |
| openTelemetryExponential | 700.25 | ± 23.84 | ops/s | 9.6x slower |

### TextFormatUtilBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusWriteToByteArray | 714.50K | ± 27.70K | ops/s | **fastest** |
| prometheusWriteToNull | 701.14K | ± 30.16K | ops/s | 1.0x slower |
| openMetricsWriteToNull | 655.96K | ± 17.06K | ops/s | 1.1x slower |
| openMetricsWriteToByteArray | 653.88K | ± 12.13K | ops/s | 1.1x slower |

### Raw Results

```
Benchmark                                            Mode  Cnt          Score        Error  Units
CounterBenchmark.codahaleIncNoLabels                thrpt   15      59551.943    ± 118.900  ops/s
CounterBenchmark.openTelemetryAdd                   thrpt   15       2073.000    ± 392.775  ops/s
CounterBenchmark.openTelemetryInc                   thrpt   15       1984.010    ± 131.624  ops/s
CounterBenchmark.openTelemetryIncNoLabels           thrpt   15       2156.557    ± 267.042  ops/s
CounterBenchmark.prometheusAdd                      thrpt   15      59651.794   ± 3392.744  ops/s
CounterBenchmark.prometheusInc                      thrpt   15      66179.491    ± 787.493  ops/s
CounterBenchmark.prometheusNoLabelsInc              thrpt   15      64858.918    ± 538.057  ops/s
CounterBenchmark.simpleclientAdd                    thrpt   15      10530.925    ± 285.155  ops/s
CounterBenchmark.simpleclientInc                    thrpt   15      10247.253    ± 464.520  ops/s
CounterBenchmark.simpleclientNoLabelsInc            thrpt   15      10210.247    ± 181.724  ops/s
HistogramBenchmark.openTelemetryClassic             thrpt   15        873.282     ± 21.507  ops/s
HistogramBenchmark.openTelemetryExponential         thrpt   15        700.255     ± 23.841  ops/s
HistogramBenchmark.prometheusClassic                thrpt   15       6626.549    ± 860.812  ops/s
HistogramBenchmark.prometheusNative                 thrpt   15       4934.001    ± 339.006  ops/s
HistogramBenchmark.simpleclient                     thrpt   15       6706.410     ± 47.913  ops/s
TextFormatUtilBenchmark.openMetricsWriteToByteArray  thrpt   15     653883.261  ± 12128.292  ops/s
TextFormatUtilBenchmark.openMetricsWriteToNull      thrpt   15     655963.977  ± 17064.160  ops/s
TextFormatUtilBenchmark.prometheusWriteToByteArray  thrpt   15     714504.310  ± 27704.790  ops/s
TextFormatUtilBenchmark.prometheusWriteToNull       thrpt   15     701144.239  ± 30162.238  ops/s
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
