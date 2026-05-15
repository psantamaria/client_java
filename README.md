# Prometheus Java Client Benchmarks

## Run Information

- **Date:** 2026-05-15T07:07:45Z
- **Commit:** [`4b69f40`](https://github.com/psantamaria/client_java/commit/4b69f40bd4e616d69468ce99dc4323162287a577)
- **JDK:** 25.0.2 (OpenJDK 64-Bit Server VM)
- **Benchmark config:** 3 fork(s), 3 warmup, 5 measurement, 4 threads
- **Hardware:** AMD EPYC 7763 64-Core Processor, 4 cores, 16 GB RAM
- **OS:** Linux 6.17.0-1013-azure

## Results

### CounterBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusInc | 64.53K | ± 2.21K | ops/s | **fastest** |
| prometheusNoLabelsInc | 56.89K | ± 304.08 | ops/s | 1.1x slower |
| prometheusAdd | 51.30K | ± 177.38 | ops/s | 1.3x slower |
| codahaleIncNoLabels | 50.14K | ± 61.91 | ops/s | 1.3x slower |
| simpleclientInc | 6.69K | ± 13.13 | ops/s | 9.6x slower |
| simpleclientNoLabelsInc | 6.51K | ± 137.60 | ops/s | 9.9x slower |
| simpleclientAdd | 6.06K | ± 73.92 | ops/s | 11x slower |
| openTelemetryIncNoLabels | 1.35K | ± 133.80 | ops/s | 48x slower |
| openTelemetryInc | 1.35K | ± 148.72 | ops/s | 48x slower |
| openTelemetryAdd | 1.21K | ± 59.93 | ops/s | 53x slower |

### HistogramBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusClassic | 7.12K | ± 211.23 | ops/s | **fastest** |
| simpleclient | 4.46K | ± 47.16 | ops/s | 1.6x slower |
| prometheusNative | 2.72K | ± 318.03 | ops/s | 2.6x slower |
| openTelemetryClassic | 686.45 | ± 20.59 | ops/s | 10x slower |
| openTelemetryExponential | 565.64 | ± 18.60 | ops/s | 13x slower |

### TextFormatUtilBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusWriteToNull | 473.81K | ± 3.22K | ops/s | **fastest** |
| openMetricsWriteToNull | 470.15K | ± 3.66K | ops/s | 1.0x slower |
| prometheusWriteToByteArray | 468.55K | ± 6.79K | ops/s | 1.0x slower |
| openMetricsWriteToByteArray | 450.87K | ± 7.92K | ops/s | 1.1x slower |

### Raw Results

```
Benchmark                                            Mode  Cnt          Score        Error  Units
CounterBenchmark.codahaleIncNoLabels                thrpt   15      50140.347     ± 61.910  ops/s
CounterBenchmark.openTelemetryAdd                   thrpt   15       1213.318     ± 59.931  ops/s
CounterBenchmark.openTelemetryInc                   thrpt   15       1347.859    ± 148.718  ops/s
CounterBenchmark.openTelemetryIncNoLabels           thrpt   15       1353.163    ± 133.802  ops/s
CounterBenchmark.prometheusAdd                      thrpt   15      51304.369    ± 177.376  ops/s
CounterBenchmark.prometheusInc                      thrpt   15      64526.254   ± 2213.445  ops/s
CounterBenchmark.prometheusNoLabelsInc              thrpt   15      56894.884    ± 304.083  ops/s
CounterBenchmark.simpleclientAdd                    thrpt   15       6063.782     ± 73.922  ops/s
CounterBenchmark.simpleclientInc                    thrpt   15       6692.660     ± 13.131  ops/s
CounterBenchmark.simpleclientNoLabelsInc            thrpt   15       6512.566    ± 137.598  ops/s
HistogramBenchmark.openTelemetryClassic             thrpt   15        686.453     ± 20.590  ops/s
HistogramBenchmark.openTelemetryExponential         thrpt   15        565.643     ± 18.600  ops/s
HistogramBenchmark.prometheusClassic                thrpt   15       7123.867    ± 211.225  ops/s
HistogramBenchmark.prometheusNative                 thrpt   15       2724.054    ± 318.033  ops/s
HistogramBenchmark.simpleclient                     thrpt   15       4455.417     ± 47.163  ops/s
TextFormatUtilBenchmark.openMetricsWriteToByteArray  thrpt   15     450865.567   ± 7920.260  ops/s
TextFormatUtilBenchmark.openMetricsWriteToNull      thrpt   15     470149.840   ± 3661.900  ops/s
TextFormatUtilBenchmark.prometheusWriteToByteArray  thrpt   15     468548.278   ± 6794.403  ops/s
TextFormatUtilBenchmark.prometheusWriteToNull       thrpt   15     473808.322   ± 3221.203  ops/s
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
