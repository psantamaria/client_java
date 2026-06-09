# Prometheus Java Client Benchmarks

## Run Information

- **Date:** 2026-06-09T07:21:27Z
- **Commit:** [`4b69f40`](https://github.com/psantamaria/client_java/commit/4b69f40bd4e616d69468ce99dc4323162287a577)
- **JDK:** 25.0.2 (OpenJDK 64-Bit Server VM)
- **Benchmark config:** 3 fork(s), 3 warmup, 5 measurement, 4 threads
- **Hardware:** AMD EPYC 7763 64-Core Processor, 4 cores, 16 GB RAM
- **OS:** Linux 6.17.0-1015-azure

## Results

### CounterBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusInc | 65.56K | ± 1.65K | ops/s | **fastest** |
| prometheusNoLabelsInc | 56.83K | ± 276.40 | ops/s | 1.2x slower |
| prometheusAdd | 51.45K | ± 254.52 | ops/s | 1.3x slower |
| codahaleIncNoLabels | 48.18K | ± 1.25K | ops/s | 1.4x slower |
| simpleclientInc | 6.58K | ± 153.51 | ops/s | 10.0x slower |
| simpleclientNoLabelsInc | 6.51K | ± 151.38 | ops/s | 10x slower |
| simpleclientAdd | 6.15K | ± 254.53 | ops/s | 11x slower |
| openTelemetryAdd | 1.53K | ± 346.66 | ops/s | 43x slower |
| openTelemetryIncNoLabels | 1.34K | ± 254.78 | ops/s | 49x slower |
| openTelemetryInc | 1.18K | ± 11.81 | ops/s | 55x slower |

### HistogramBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusClassic | 5.07K | ± 1.05K | ops/s | **fastest** |
| simpleclient | 4.45K | ± 48.15 | ops/s | 1.1x slower |
| prometheusNative | 3.00K | ± 235.06 | ops/s | 1.7x slower |
| openTelemetryClassic | 694.83 | ± 43.43 | ops/s | 7.3x slower |
| openTelemetryExponential | 599.77 | ± 8.43 | ops/s | 8.5x slower |

### TextFormatUtilBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusWriteToNull | 485.20K | ± 3.38K | ops/s | **fastest** |
| prometheusWriteToByteArray | 484.96K | ± 3.77K | ops/s | 1.0x slower |
| openMetricsWriteToByteArray | 476.57K | ± 2.87K | ops/s | 1.0x slower |
| openMetricsWriteToNull | 471.78K | ± 5.69K | ops/s | 1.0x slower |

### Raw Results

```
Benchmark                                            Mode  Cnt          Score        Error  Units
CounterBenchmark.codahaleIncNoLabels                thrpt   15      48178.584   ± 1247.194  ops/s
CounterBenchmark.openTelemetryAdd                   thrpt   15       1530.523    ± 346.659  ops/s
CounterBenchmark.openTelemetryInc                   thrpt   15       1182.068     ± 11.810  ops/s
CounterBenchmark.openTelemetryIncNoLabels           thrpt   15       1340.090    ± 254.776  ops/s
CounterBenchmark.prometheusAdd                      thrpt   15      51451.207    ± 254.515  ops/s
CounterBenchmark.prometheusInc                      thrpt   15      65557.091   ± 1649.826  ops/s
CounterBenchmark.prometheusNoLabelsInc              thrpt   15      56825.740    ± 276.398  ops/s
CounterBenchmark.simpleclientAdd                    thrpt   15       6149.544    ± 254.532  ops/s
CounterBenchmark.simpleclientInc                    thrpt   15       6579.897    ± 153.510  ops/s
CounterBenchmark.simpleclientNoLabelsInc            thrpt   15       6509.234    ± 151.376  ops/s
HistogramBenchmark.openTelemetryClassic             thrpt   15        694.832     ± 43.432  ops/s
HistogramBenchmark.openTelemetryExponential         thrpt   15        599.774      ± 8.431  ops/s
HistogramBenchmark.prometheusClassic                thrpt   15       5069.841   ± 1051.993  ops/s
HistogramBenchmark.prometheusNative                 thrpt   15       3004.414    ± 235.063  ops/s
HistogramBenchmark.simpleclient                     thrpt   15       4451.328     ± 48.147  ops/s
TextFormatUtilBenchmark.openMetricsWriteToByteArray  thrpt   15     476573.289   ± 2868.513  ops/s
TextFormatUtilBenchmark.openMetricsWriteToNull      thrpt   15     471783.585   ± 5689.615  ops/s
TextFormatUtilBenchmark.prometheusWriteToByteArray  thrpt   15     484963.019   ± 3768.667  ops/s
TextFormatUtilBenchmark.prometheusWriteToNull       thrpt   15     485199.984   ± 3378.025  ops/s
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
