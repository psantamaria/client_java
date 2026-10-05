# Prometheus Java Client Benchmarks

## Run Information

- **Date:** 2026-10-05T09:23:21Z
- **Commit:** [`4b69f40`](https://github.com/psantamaria/client_java/commit/4b69f40bd4e616d69468ce99dc4323162287a577)
- **JDK:** 25.0.2 (OpenJDK 64-Bit Server VM)
- **Benchmark config:** 3 fork(s), 3 warmup, 5 measurement, 4 threads
- **Hardware:** AMD EPYC 7763 64-Core Processor, 4 cores, 16 GB RAM
- **OS:** Linux 6.17.0-1022-azure

## Results

### CounterBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusInc | 65.65K | ± 593.71 | ops/s | **fastest** |
| prometheusNoLabelsInc | 56.43K | ± 548.44 | ops/s | 1.2x slower |
| prometheusAdd | 50.65K | ± 673.30 | ops/s | 1.3x slower |
| codahaleIncNoLabels | 48.91K | ± 1.24K | ops/s | 1.3x slower |
| simpleclientInc | 6.61K | ± 104.29 | ops/s | 9.9x slower |
| simpleclientNoLabelsInc | 6.46K | ± 218.18 | ops/s | 10x slower |
| simpleclientAdd | 5.89K | ± 141.47 | ops/s | 11x slower |
| openTelemetryAdd | 1.42K | ± 254.19 | ops/s | 46x slower |
| openTelemetryIncNoLabels | 1.35K | ± 156.51 | ops/s | 49x slower |
| openTelemetryInc | 1.33K | ± 160.49 | ops/s | 49x slower |

### HistogramBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusClassic | 4.64K | ± 830.21 | ops/s | **fastest** |
| simpleclient | 4.42K | ± 62.88 | ops/s | 1.0x slower |
| prometheusNative | 3.00K | ± 267.32 | ops/s | 1.5x slower |
| openTelemetryClassic | 672.27 | ± 23.28 | ops/s | 6.9x slower |
| openTelemetryExponential | 549.83 | ± 30.42 | ops/s | 8.4x slower |

### TextFormatUtilBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusWriteToNull | 479.82K | ± 3.66K | ops/s | **fastest** |
| prometheusWriteToByteArray | 472.28K | ± 3.59K | ops/s | 1.0x slower |
| openMetricsWriteToNull | 471.68K | ± 2.52K | ops/s | 1.0x slower |
| openMetricsWriteToByteArray | 469.11K | ± 3.98K | ops/s | 1.0x slower |

### Raw Results

```
Benchmark                                            Mode  Cnt          Score        Error  Units
CounterBenchmark.codahaleIncNoLabels                thrpt   15      48907.752   ± 1244.740  ops/s
CounterBenchmark.openTelemetryAdd                   thrpt   15       1418.728    ± 254.188  ops/s
CounterBenchmark.openTelemetryInc                   thrpt   15       1330.652    ± 160.489  ops/s
CounterBenchmark.openTelemetryIncNoLabels           thrpt   15       1353.644    ± 156.508  ops/s
CounterBenchmark.prometheusAdd                      thrpt   15      50654.808    ± 673.303  ops/s
CounterBenchmark.prometheusInc                      thrpt   15      65654.742    ± 593.707  ops/s
CounterBenchmark.prometheusNoLabelsInc              thrpt   15      56434.505    ± 548.435  ops/s
CounterBenchmark.simpleclientAdd                    thrpt   15       5894.378    ± 141.473  ops/s
CounterBenchmark.simpleclientInc                    thrpt   15       6608.059    ± 104.292  ops/s
CounterBenchmark.simpleclientNoLabelsInc            thrpt   15       6461.726    ± 218.182  ops/s
HistogramBenchmark.openTelemetryClassic             thrpt   15        672.272     ± 23.279  ops/s
HistogramBenchmark.openTelemetryExponential         thrpt   15        549.834     ± 30.416  ops/s
HistogramBenchmark.prometheusClassic                thrpt   15       4635.670    ± 830.209  ops/s
HistogramBenchmark.prometheusNative                 thrpt   15       2999.736    ± 267.315  ops/s
HistogramBenchmark.simpleclient                     thrpt   15       4416.337     ± 62.877  ops/s
TextFormatUtilBenchmark.openMetricsWriteToByteArray  thrpt   15     469113.787   ± 3977.405  ops/s
TextFormatUtilBenchmark.openMetricsWriteToNull      thrpt   15     471681.694   ± 2524.792  ops/s
TextFormatUtilBenchmark.prometheusWriteToByteArray  thrpt   15     472280.616   ± 3585.370  ops/s
TextFormatUtilBenchmark.prometheusWriteToNull       thrpt   15     479820.397   ± 3661.782  ops/s
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
