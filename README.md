# Prometheus Java Client Benchmarks

## Run Information

- **Date:** 2026-07-12T06:39:01Z
- **Commit:** [`4b69f40`](https://github.com/psantamaria/client_java/commit/4b69f40bd4e616d69468ce99dc4323162287a577)
- **JDK:** 25.0.2 (OpenJDK 64-Bit Server VM)
- **Benchmark config:** 3 fork(s), 3 warmup, 5 measurement, 4 threads
- **Hardware:** AMD EPYC 7763 64-Core Processor, 4 cores, 16 GB RAM
- **OS:** Linux 6.17.0-1018-azure

## Results

### CounterBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusInc | 64.96K | ± 1.87K | ops/s | **fastest** |
| prometheusNoLabelsInc | 57.15K | ± 127.42 | ops/s | 1.1x slower |
| prometheusAdd | 51.16K | ± 507.68 | ops/s | 1.3x slower |
| codahaleIncNoLabels | 49.49K | ± 1.79K | ops/s | 1.3x slower |
| simpleclientNoLabelsInc | 6.45K | ± 157.90 | ops/s | 10x slower |
| simpleclientInc | 6.41K | ± 127.27 | ops/s | 10x slower |
| simpleclientAdd | 6.17K | ± 253.35 | ops/s | 11x slower |
| openTelemetryAdd | 1.41K | ± 210.06 | ops/s | 46x slower |
| openTelemetryIncNoLabels | 1.41K | ± 167.36 | ops/s | 46x slower |
| openTelemetryInc | 1.27K | ± 11.41 | ops/s | 51x slower |

### HistogramBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusClassic | 5.83K | ± 2.08K | ops/s | **fastest** |
| simpleclient | 4.39K | ± 18.03 | ops/s | 1.3x slower |
| prometheusNative | 3.01K | ± 296.59 | ops/s | 1.9x slower |
| openTelemetryClassic | 679.77 | ± 18.46 | ops/s | 8.6x slower |
| openTelemetryExponential | 543.81 | ± 16.84 | ops/s | 11x slower |

### TextFormatUtilBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusWriteToNull | 484.65K | ± 2.51K | ops/s | **fastest** |
| prometheusWriteToByteArray | 472.55K | ± 4.12K | ops/s | 1.0x slower |
| openMetricsWriteToNull | 470.62K | ± 5.48K | ops/s | 1.0x slower |
| openMetricsWriteToByteArray | 462.24K | ± 4.18K | ops/s | 1.0x slower |

### Raw Results

```
Benchmark                                            Mode  Cnt          Score        Error  Units
CounterBenchmark.codahaleIncNoLabels                thrpt   15      49486.451   ± 1787.985  ops/s
CounterBenchmark.openTelemetryAdd                   thrpt   15       1407.174    ± 210.057  ops/s
CounterBenchmark.openTelemetryInc                   thrpt   15       1267.490     ± 11.411  ops/s
CounterBenchmark.openTelemetryIncNoLabels           thrpt   15       1406.984    ± 167.362  ops/s
CounterBenchmark.prometheusAdd                      thrpt   15      51158.585    ± 507.680  ops/s
CounterBenchmark.prometheusInc                      thrpt   15      64958.339   ± 1865.457  ops/s
CounterBenchmark.prometheusNoLabelsInc              thrpt   15      57150.404    ± 127.419  ops/s
CounterBenchmark.simpleclientAdd                    thrpt   15       6171.186    ± 253.352  ops/s
CounterBenchmark.simpleclientInc                    thrpt   15       6407.915    ± 127.269  ops/s
CounterBenchmark.simpleclientNoLabelsInc            thrpt   15       6445.128    ± 157.897  ops/s
HistogramBenchmark.openTelemetryClassic             thrpt   15        679.765     ± 18.456  ops/s
HistogramBenchmark.openTelemetryExponential         thrpt   15        543.810     ± 16.840  ops/s
HistogramBenchmark.prometheusClassic                thrpt   15       5826.780   ± 2077.584  ops/s
HistogramBenchmark.prometheusNative                 thrpt   15       3013.433    ± 296.595  ops/s
HistogramBenchmark.simpleclient                     thrpt   15       4394.199     ± 18.031  ops/s
TextFormatUtilBenchmark.openMetricsWriteToByteArray  thrpt   15     462241.780   ± 4183.506  ops/s
TextFormatUtilBenchmark.openMetricsWriteToNull      thrpt   15     470621.847   ± 5480.115  ops/s
TextFormatUtilBenchmark.prometheusWriteToByteArray  thrpt   15     472551.272   ± 4118.111  ops/s
TextFormatUtilBenchmark.prometheusWriteToNull       thrpt   15     484646.139   ± 2512.719  ops/s
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
