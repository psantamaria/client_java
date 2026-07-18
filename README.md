# Prometheus Java Client Benchmarks

## Run Information

- **Date:** 2026-07-18T06:01:15Z
- **Commit:** [`4b69f40`](https://github.com/psantamaria/client_java/commit/4b69f40bd4e616d69468ce99dc4323162287a577)
- **JDK:** 25.0.2 (OpenJDK 64-Bit Server VM)
- **Benchmark config:** 3 fork(s), 3 warmup, 5 measurement, 4 threads
- **Hardware:** AMD EPYC 7763 64-Core Processor, 4 cores, 16 GB RAM
- **OS:** Linux 6.17.0-1020-azure

## Results

### CounterBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusInc | 61.75K | ± 5.44K | ops/s | **fastest** |
| prometheusNoLabelsInc | 56.14K | ± 1.01K | ops/s | 1.1x slower |
| prometheusAdd | 51.58K | ± 81.77 | ops/s | 1.2x slower |
| codahaleIncNoLabels | 48.32K | ± 1.52K | ops/s | 1.3x slower |
| simpleclientNoLabelsInc | 6.54K | ± 113.17 | ops/s | 9.4x slower |
| simpleclientInc | 6.40K | ± 234.35 | ops/s | 9.6x slower |
| simpleclientAdd | 6.30K | ± 299.71 | ops/s | 9.8x slower |
| openTelemetryInc | 1.27K | ± 17.12 | ops/s | 49x slower |
| openTelemetryIncNoLabels | 1.25K | ± 164.19 | ops/s | 49x slower |
| openTelemetryAdd | 1.23K | ± 23.45 | ops/s | 50x slower |

### HistogramBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusClassic | 4.97K | ± 821.28 | ops/s | **fastest** |
| simpleclient | 4.43K | ± 94.17 | ops/s | 1.1x slower |
| prometheusNative | 2.92K | ± 272.86 | ops/s | 1.7x slower |
| openTelemetryClassic | 672.95 | ± 19.27 | ops/s | 7.4x slower |
| openTelemetryExponential | 557.95 | ± 47.44 | ops/s | 8.9x slower |

### TextFormatUtilBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusWriteToNull | 491.33K | ± 1.34K | ops/s | **fastest** |
| prometheusWriteToByteArray | 486.04K | ± 3.29K | ops/s | 1.0x slower |
| openMetricsWriteToNull | 479.16K | ± 2.77K | ops/s | 1.0x slower |
| openMetricsWriteToByteArray | 470.52K | ± 3.11K | ops/s | 1.0x slower |

### Raw Results

```
Benchmark                                            Mode  Cnt          Score        Error  Units
CounterBenchmark.codahaleIncNoLabels                thrpt   15      48322.369   ± 1516.882  ops/s
CounterBenchmark.openTelemetryAdd                   thrpt   15       1229.021     ± 23.448  ops/s
CounterBenchmark.openTelemetryInc                   thrpt   15       1271.722     ± 17.124  ops/s
CounterBenchmark.openTelemetryIncNoLabels           thrpt   15       1251.142    ± 164.194  ops/s
CounterBenchmark.prometheusAdd                      thrpt   15      51584.211     ± 81.774  ops/s
CounterBenchmark.prometheusInc                      thrpt   15      61749.517   ± 5444.038  ops/s
CounterBenchmark.prometheusNoLabelsInc              thrpt   15      56144.425   ± 1005.035  ops/s
CounterBenchmark.simpleclientAdd                    thrpt   15       6296.606    ± 299.707  ops/s
CounterBenchmark.simpleclientInc                    thrpt   15       6402.729    ± 234.347  ops/s
CounterBenchmark.simpleclientNoLabelsInc            thrpt   15       6543.636    ± 113.174  ops/s
HistogramBenchmark.openTelemetryClassic             thrpt   15        672.947     ± 19.270  ops/s
HistogramBenchmark.openTelemetryExponential         thrpt   15        557.954     ± 47.437  ops/s
HistogramBenchmark.prometheusClassic                thrpt   15       4973.446    ± 821.276  ops/s
HistogramBenchmark.prometheusNative                 thrpt   15       2917.410    ± 272.857  ops/s
HistogramBenchmark.simpleclient                     thrpt   15       4433.575     ± 94.172  ops/s
TextFormatUtilBenchmark.openMetricsWriteToByteArray  thrpt   15     470520.635   ± 3109.411  ops/s
TextFormatUtilBenchmark.openMetricsWriteToNull      thrpt   15     479164.556   ± 2769.805  ops/s
TextFormatUtilBenchmark.prometheusWriteToByteArray  thrpt   15     486043.926   ± 3291.073  ops/s
TextFormatUtilBenchmark.prometheusWriteToNull       thrpt   15     491328.786   ± 1343.694  ops/s
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
