# Prometheus Java Client Benchmarks

## Run Information

- **Date:** 2026-07-17T06:15:33Z
- **Commit:** [`4b69f40`](https://github.com/psantamaria/client_java/commit/4b69f40bd4e616d69468ce99dc4323162287a577)
- **JDK:** 25.0.2 (OpenJDK 64-Bit Server VM)
- **Benchmark config:** 3 fork(s), 3 warmup, 5 measurement, 4 threads
- **Hardware:** INTEL(R) XEON(R) PLATINUM 8573C, 4 cores, 16 GB RAM
- **OS:** Linux 6.17.0-1020-azure

## Results

### CounterBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| codahaleIncNoLabels | 27.61K | ± 213.09 | ops/s | **fastest** |
| prometheusInc | 26.64K | ± 11.31 | ops/s | 1.0x slower |
| prometheusNoLabelsInc | 26.52K | ± 268.81 | ops/s | 1.0x slower |
| prometheusAdd | 26.01K | ± 101.25 | ops/s | 1.1x slower |
| simpleclientInc | 6.67K | ± 22.54 | ops/s | 4.1x slower |
| simpleclientNoLabelsInc | 6.63K | ± 36.73 | ops/s | 4.2x slower |
| simpleclientAdd | 6.61K | ± 120.24 | ops/s | 4.2x slower |
| openTelemetryAdd | 1.05K | ± 37.99 | ops/s | 26x slower |
| openTelemetryIncNoLabels | 1.03K | ± 69.64 | ops/s | 27x slower |
| openTelemetryInc | 990.72 | ± 28.88 | ops/s | 28x slower |

### HistogramBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| simpleclient | 4.36K | ± 45.38 | ops/s | **fastest** |
| prometheusClassic | 3.24K | ± 269.54 | ops/s | 1.3x slower |
| prometheusNative | 1.98K | ± 287.99 | ops/s | 2.2x slower |
| openTelemetryClassic | 375.70 | ± 12.07 | ops/s | 12x slower |
| openTelemetryExponential | 317.07 | ± 5.43 | ops/s | 14x slower |

### TextFormatUtilBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusWriteToByteArray | 302.87K | ± 1.82K | ops/s | **fastest** |
| prometheusWriteToNull | 302.45K | ± 1.55K | ops/s | 1.0x slower |
| openMetricsWriteToNull | 287.16K | ± 1.18K | ops/s | 1.1x slower |
| openMetricsWriteToByteArray | 284.23K | ± 1.27K | ops/s | 1.1x slower |

### Raw Results

```
Benchmark                                            Mode  Cnt          Score        Error  Units
CounterBenchmark.codahaleIncNoLabels                thrpt   15      27612.264    ± 213.088  ops/s
CounterBenchmark.openTelemetryAdd                   thrpt   15       1049.328     ± 37.986  ops/s
CounterBenchmark.openTelemetryInc                   thrpt   15        990.724     ± 28.882  ops/s
CounterBenchmark.openTelemetryIncNoLabels           thrpt   15       1025.777     ± 69.643  ops/s
CounterBenchmark.prometheusAdd                      thrpt   15      26010.103    ± 101.247  ops/s
CounterBenchmark.prometheusInc                      thrpt   15      26639.973     ± 11.314  ops/s
CounterBenchmark.prometheusNoLabelsInc              thrpt   15      26515.892    ± 268.811  ops/s
CounterBenchmark.simpleclientAdd                    thrpt   15       6614.662    ± 120.240  ops/s
CounterBenchmark.simpleclientInc                    thrpt   15       6666.606     ± 22.543  ops/s
CounterBenchmark.simpleclientNoLabelsInc            thrpt   15       6626.891     ± 36.728  ops/s
HistogramBenchmark.openTelemetryClassic             thrpt   15        375.699     ± 12.068  ops/s
HistogramBenchmark.openTelemetryExponential         thrpt   15        317.073      ± 5.432  ops/s
HistogramBenchmark.prometheusClassic                thrpt   15       3242.071    ± 269.542  ops/s
HistogramBenchmark.prometheusNative                 thrpt   15       1983.098    ± 287.992  ops/s
HistogramBenchmark.simpleclient                     thrpt   15       4360.975     ± 45.375  ops/s
TextFormatUtilBenchmark.openMetricsWriteToByteArray  thrpt   15     284231.050   ± 1272.759  ops/s
TextFormatUtilBenchmark.openMetricsWriteToNull      thrpt   15     287160.188   ± 1178.560  ops/s
TextFormatUtilBenchmark.prometheusWriteToByteArray  thrpt   15     302866.579   ± 1824.379  ops/s
TextFormatUtilBenchmark.prometheusWriteToNull       thrpt   15     302445.835   ± 1550.950  ops/s
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
