# Prometheus Java Client Benchmarks

## Run Information

- **Date:** 2026-06-27T07:06:20Z
- **Commit:** [`4b69f40`](https://github.com/psantamaria/client_java/commit/4b69f40bd4e616d69468ce99dc4323162287a577)
- **JDK:** 25.0.2 (OpenJDK 64-Bit Server VM)
- **Benchmark config:** 3 fork(s), 3 warmup, 5 measurement, 4 threads
- **Hardware:** AMD EPYC 7763 64-Core Processor, 4 cores, 16 GB RAM
- **OS:** Linux 6.17.0-1018-azure

## Results

### CounterBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusInc | 65.31K | ± 1.64K | ops/s | **fastest** |
| prometheusNoLabelsInc | 55.92K | ± 1.16K | ops/s | 1.2x slower |
| prometheusAdd | 51.06K | ± 520.51 | ops/s | 1.3x slower |
| codahaleIncNoLabels | 48.47K | ± 1.35K | ops/s | 1.3x slower |
| simpleclientNoLabelsInc | 6.48K | ± 188.39 | ops/s | 10x slower |
| simpleclientAdd | 6.46K | ± 46.25 | ops/s | 10x slower |
| simpleclientInc | 6.43K | ± 219.54 | ops/s | 10x slower |
| openTelemetryInc | 1.43K | ± 178.80 | ops/s | 46x slower |
| openTelemetryAdd | 1.42K | ± 192.74 | ops/s | 46x slower |
| openTelemetryIncNoLabels | 1.13K | ± 71.08 | ops/s | 58x slower |

### HistogramBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusClassic | 5.67K | ± 1.41K | ops/s | **fastest** |
| simpleclient | 4.47K | ± 20.56 | ops/s | 1.3x slower |
| prometheusNative | 2.72K | ± 234.98 | ops/s | 2.1x slower |
| openTelemetryClassic | 689.36 | ± 61.44 | ops/s | 8.2x slower |
| openTelemetryExponential | 551.09 | ± 4.87 | ops/s | 10x slower |

### TextFormatUtilBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusWriteToNull | 485.12K | ± 4.44K | ops/s | **fastest** |
| prometheusWriteToByteArray | 480.22K | ± 4.89K | ops/s | 1.0x slower |
| openMetricsWriteToNull | 475.51K | ± 5.73K | ops/s | 1.0x slower |
| openMetricsWriteToByteArray | 449.29K | ± 19.56K | ops/s | 1.1x slower |

### Raw Results

```
Benchmark                                            Mode  Cnt          Score        Error  Units
CounterBenchmark.codahaleIncNoLabels                thrpt   15      48470.886   ± 1353.083  ops/s
CounterBenchmark.openTelemetryAdd                   thrpt   15       1422.734    ± 192.739  ops/s
CounterBenchmark.openTelemetryInc                   thrpt   15       1431.395    ± 178.804  ops/s
CounterBenchmark.openTelemetryIncNoLabels           thrpt   15       1134.424     ± 71.076  ops/s
CounterBenchmark.prometheusAdd                      thrpt   15      51064.848    ± 520.510  ops/s
CounterBenchmark.prometheusInc                      thrpt   15      65311.688   ± 1641.905  ops/s
CounterBenchmark.prometheusNoLabelsInc              thrpt   15      55921.056   ± 1155.698  ops/s
CounterBenchmark.simpleclientAdd                    thrpt   15       6456.915     ± 46.254  ops/s
CounterBenchmark.simpleclientInc                    thrpt   15       6434.782    ± 219.538  ops/s
CounterBenchmark.simpleclientNoLabelsInc            thrpt   15       6484.409    ± 188.391  ops/s
HistogramBenchmark.openTelemetryClassic             thrpt   15        689.356     ± 61.440  ops/s
HistogramBenchmark.openTelemetryExponential         thrpt   15        551.095      ± 4.869  ops/s
HistogramBenchmark.prometheusClassic                thrpt   15       5674.176   ± 1405.905  ops/s
HistogramBenchmark.prometheusNative                 thrpt   15       2721.063    ± 234.981  ops/s
HistogramBenchmark.simpleclient                     thrpt   15       4466.579     ± 20.555  ops/s
TextFormatUtilBenchmark.openMetricsWriteToByteArray  thrpt   15     449294.423  ± 19559.632  ops/s
TextFormatUtilBenchmark.openMetricsWriteToNull      thrpt   15     475507.250   ± 5725.391  ops/s
TextFormatUtilBenchmark.prometheusWriteToByteArray  thrpt   15     480220.747   ± 4892.984  ops/s
TextFormatUtilBenchmark.prometheusWriteToNull       thrpt   15     485121.774   ± 4441.257  ops/s
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
