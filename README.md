# Prometheus Java Client Benchmarks

## Run Information

- **Date:** 2026-08-06T06:28:31Z
- **Commit:** [`4b69f40`](https://github.com/psantamaria/client_java/commit/4b69f40bd4e616d69468ce99dc4323162287a577)
- **JDK:** 25.0.2 (OpenJDK 64-Bit Server VM)
- **Benchmark config:** 3 fork(s), 3 warmup, 5 measurement, 4 threads
- **Hardware:** AMD EPYC 7763 64-Core Processor, 4 cores, 16 GB RAM
- **OS:** Linux 6.17.0-1020-azure

## Results

### CounterBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusInc | 64.86K | ± 918.84 | ops/s | **fastest** |
| prometheusNoLabelsInc | 55.15K | ± 2.78K | ops/s | 1.2x slower |
| prometheusAdd | 51.47K | ± 212.42 | ops/s | 1.3x slower |
| codahaleIncNoLabels | 45.07K | ± 8.82K | ops/s | 1.4x slower |
| simpleclientNoLabelsInc | 6.60K | ± 10.64 | ops/s | 9.8x slower |
| simpleclientInc | 6.56K | ± 217.87 | ops/s | 9.9x slower |
| simpleclientAdd | 6.20K | ± 222.08 | ops/s | 10x slower |
| openTelemetryAdd | 1.44K | ± 265.93 | ops/s | 45x slower |
| openTelemetryInc | 1.41K | ± 205.89 | ops/s | 46x slower |
| openTelemetryIncNoLabels | 1.25K | ± 16.88 | ops/s | 52x slower |

### HistogramBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusClassic | 5.62K | ± 1.16K | ops/s | **fastest** |
| simpleclient | 4.41K | ± 26.88 | ops/s | 1.3x slower |
| prometheusNative | 2.97K | ± 306.80 | ops/s | 1.9x slower |
| openTelemetryClassic | 693.28 | ± 28.66 | ops/s | 8.1x slower |
| openTelemetryExponential | 545.26 | ± 26.51 | ops/s | 10x slower |

### TextFormatUtilBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusWriteToNull | 483.97K | ± 2.54K | ops/s | **fastest** |
| prometheusWriteToByteArray | 477.89K | ± 4.50K | ops/s | 1.0x slower |
| openMetricsWriteToNull | 474.78K | ± 7.39K | ops/s | 1.0x slower |
| openMetricsWriteToByteArray | 467.43K | ± 8.72K | ops/s | 1.0x slower |

### Raw Results

```
Benchmark                                            Mode  Cnt          Score        Error  Units
CounterBenchmark.codahaleIncNoLabels                thrpt   15      45072.967   ± 8817.721  ops/s
CounterBenchmark.openTelemetryAdd                   thrpt   15       1436.487    ± 265.932  ops/s
CounterBenchmark.openTelemetryInc                   thrpt   15       1405.673    ± 205.888  ops/s
CounterBenchmark.openTelemetryIncNoLabels           thrpt   15       1246.892     ± 16.878  ops/s
CounterBenchmark.prometheusAdd                      thrpt   15      51466.912    ± 212.421  ops/s
CounterBenchmark.prometheusInc                      thrpt   15      64859.818    ± 918.843  ops/s
CounterBenchmark.prometheusNoLabelsInc              thrpt   15      55151.510   ± 2778.847  ops/s
CounterBenchmark.simpleclientAdd                    thrpt   15       6199.053    ± 222.080  ops/s
CounterBenchmark.simpleclientInc                    thrpt   15       6559.167    ± 217.869  ops/s
CounterBenchmark.simpleclientNoLabelsInc            thrpt   15       6598.016     ± 10.636  ops/s
HistogramBenchmark.openTelemetryClassic             thrpt   15        693.281     ± 28.662  ops/s
HistogramBenchmark.openTelemetryExponential         thrpt   15        545.259     ± 26.514  ops/s
HistogramBenchmark.prometheusClassic                thrpt   15       5624.632   ± 1155.895  ops/s
HistogramBenchmark.prometheusNative                 thrpt   15       2969.280    ± 306.799  ops/s
HistogramBenchmark.simpleclient                     thrpt   15       4405.084     ± 26.882  ops/s
TextFormatUtilBenchmark.openMetricsWriteToByteArray  thrpt   15     467432.874   ± 8715.281  ops/s
TextFormatUtilBenchmark.openMetricsWriteToNull      thrpt   15     474779.999   ± 7392.867  ops/s
TextFormatUtilBenchmark.prometheusWriteToByteArray  thrpt   15     477886.340   ± 4496.657  ops/s
TextFormatUtilBenchmark.prometheusWriteToNull       thrpt   15     483972.891   ± 2537.774  ops/s
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
