# Prometheus Java Client Benchmarks

## Run Information

- **Date:** 2026-07-05T07:15:50Z
- **Commit:** [`4b69f40`](https://github.com/psantamaria/client_java/commit/4b69f40bd4e616d69468ce99dc4323162287a577)
- **JDK:** 25.0.2 (OpenJDK 64-Bit Server VM)
- **Benchmark config:** 3 fork(s), 3 warmup, 5 measurement, 4 threads
- **Hardware:** AMD EPYC 7763 64-Core Processor, 4 cores, 16 GB RAM
- **OS:** Linux 6.17.0-1018-azure

## Results

### CounterBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusInc | 64.98K | ± 2.42K | ops/s | **fastest** |
| prometheusNoLabelsInc | 55.86K | ± 1.52K | ops/s | 1.2x slower |
| codahaleIncNoLabels | 48.93K | ± 1.38K | ops/s | 1.3x slower |
| prometheusAdd | 44.25K | ± 10.97K | ops/s | 1.5x slower |
| simpleclientInc | 6.49K | ± 150.11 | ops/s | 10x slower |
| simpleclientNoLabelsInc | 6.26K | ± 141.98 | ops/s | 10x slower |
| simpleclientAdd | 6.23K | ± 186.91 | ops/s | 10x slower |
| openTelemetryInc | 1.52K | ± 170.26 | ops/s | 43x slower |
| openTelemetryIncNoLabels | 1.33K | ± 98.19 | ops/s | 49x slower |
| openTelemetryAdd | 1.26K | ± 34.40 | ops/s | 52x slower |

### HistogramBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusClassic | 6.02K | ± 1.49K | ops/s | **fastest** |
| simpleclient | 4.40K | ± 32.66 | ops/s | 1.4x slower |
| prometheusNative | 3.13K | ± 159.21 | ops/s | 1.9x slower |
| openTelemetryClassic | 711.13 | ± 27.21 | ops/s | 8.5x slower |
| openTelemetryExponential | 573.52 | ± 30.23 | ops/s | 11x slower |

### TextFormatUtilBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusWriteToNull | 493.73K | ± 2.97K | ops/s | **fastest** |
| prometheusWriteToByteArray | 491.01K | ± 4.14K | ops/s | 1.0x slower |
| openMetricsWriteToNull | 481.65K | ± 11.01K | ops/s | 1.0x slower |
| openMetricsWriteToByteArray | 479.39K | ± 3.50K | ops/s | 1.0x slower |

### Raw Results

```
Benchmark                                            Mode  Cnt          Score        Error  Units
CounterBenchmark.codahaleIncNoLabels                thrpt   15      48934.118   ± 1376.635  ops/s
CounterBenchmark.openTelemetryAdd                   thrpt   15       1257.405     ± 34.396  ops/s
CounterBenchmark.openTelemetryInc                   thrpt   15       1518.875    ± 170.258  ops/s
CounterBenchmark.openTelemetryIncNoLabels           thrpt   15       1332.076     ± 98.189  ops/s
CounterBenchmark.prometheusAdd                      thrpt   15      44253.850  ± 10966.519  ops/s
CounterBenchmark.prometheusInc                      thrpt   15      64984.574   ± 2418.721  ops/s
CounterBenchmark.prometheusNoLabelsInc              thrpt   15      55864.799   ± 1515.902  ops/s
CounterBenchmark.simpleclientAdd                    thrpt   15       6225.488    ± 186.912  ops/s
CounterBenchmark.simpleclientInc                    thrpt   15       6491.726    ± 150.113  ops/s
CounterBenchmark.simpleclientNoLabelsInc            thrpt   15       6257.884    ± 141.979  ops/s
HistogramBenchmark.openTelemetryClassic             thrpt   15        711.129     ± 27.213  ops/s
HistogramBenchmark.openTelemetryExponential         thrpt   15        573.515     ± 30.230  ops/s
HistogramBenchmark.prometheusClassic                thrpt   15       6022.375   ± 1487.877  ops/s
HistogramBenchmark.prometheusNative                 thrpt   15       3128.049    ± 159.214  ops/s
HistogramBenchmark.simpleclient                     thrpt   15       4402.515     ± 32.663  ops/s
TextFormatUtilBenchmark.openMetricsWriteToByteArray  thrpt   15     479386.842   ± 3497.577  ops/s
TextFormatUtilBenchmark.openMetricsWriteToNull      thrpt   15     481650.978  ± 11009.329  ops/s
TextFormatUtilBenchmark.prometheusWriteToByteArray  thrpt   15     491009.129   ± 4144.172  ops/s
TextFormatUtilBenchmark.prometheusWriteToNull       thrpt   15     493729.541   ± 2966.621  ops/s
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
