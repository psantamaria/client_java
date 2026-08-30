# Prometheus Java Client Benchmarks

## Run Information

- **Date:** 2026-08-30T09:01:38Z
- **Commit:** [`4b69f40`](https://github.com/psantamaria/client_java/commit/4b69f40bd4e616d69468ce99dc4323162287a577)
- **JDK:** 25.0.2 (OpenJDK 64-Bit Server VM)
- **Benchmark config:** 3 fork(s), 3 warmup, 5 measurement, 4 threads
- **Hardware:** AMD EPYC 7763 64-Core Processor, 4 cores, 16 GB RAM
- **OS:** Linux 6.17.0-1022-azure

## Results

### CounterBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusInc | 64.70K | ± 1.38K | ops/s | **fastest** |
| prometheusNoLabelsInc | 56.92K | ± 356.63 | ops/s | 1.1x slower |
| prometheusAdd | 51.43K | ± 212.33 | ops/s | 1.3x slower |
| codahaleIncNoLabels | 48.59K | ± 1.28K | ops/s | 1.3x slower |
| simpleclientInc | 6.55K | ± 153.71 | ops/s | 9.9x slower |
| simpleclientNoLabelsInc | 6.48K | ± 127.96 | ops/s | 10.0x slower |
| simpleclientAdd | 6.29K | ± 263.19 | ops/s | 10x slower |
| openTelemetryAdd | 1.60K | ± 290.85 | ops/s | 40x slower |
| openTelemetryInc | 1.38K | ± 217.10 | ops/s | 47x slower |
| openTelemetryIncNoLabels | 1.29K | ± 88.68 | ops/s | 50x slower |

### HistogramBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusClassic | 4.94K | ± 1.06K | ops/s | **fastest** |
| simpleclient | 4.46K | ± 51.43 | ops/s | 1.1x slower |
| prometheusNative | 2.67K | ± 84.19 | ops/s | 1.9x slower |
| openTelemetryClassic | 671.56 | ± 27.47 | ops/s | 7.4x slower |
| openTelemetryExponential | 573.22 | ± 18.53 | ops/s | 8.6x slower |

### TextFormatUtilBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| openMetricsWriteToNull | 485.70K | ± 2.63K | ops/s | **fastest** |
| prometheusWriteToNull | 482.70K | ± 6.56K | ops/s | 1.0x slower |
| prometheusWriteToByteArray | 481.97K | ± 4.11K | ops/s | 1.0x slower |
| openMetricsWriteToByteArray | 473.22K | ± 2.45K | ops/s | 1.0x slower |

### Raw Results

```
Benchmark                                            Mode  Cnt          Score        Error  Units
CounterBenchmark.codahaleIncNoLabels                thrpt   15      48588.457   ± 1275.851  ops/s
CounterBenchmark.openTelemetryAdd                   thrpt   15       1597.689    ± 290.848  ops/s
CounterBenchmark.openTelemetryInc                   thrpt   15       1375.091    ± 217.104  ops/s
CounterBenchmark.openTelemetryIncNoLabels           thrpt   15       1286.451     ± 88.680  ops/s
CounterBenchmark.prometheusAdd                      thrpt   15      51429.831    ± 212.330  ops/s
CounterBenchmark.prometheusInc                      thrpt   15      64696.038   ± 1384.227  ops/s
CounterBenchmark.prometheusNoLabelsInc              thrpt   15      56921.481    ± 356.627  ops/s
CounterBenchmark.simpleclientAdd                    thrpt   15       6288.010    ± 263.186  ops/s
CounterBenchmark.simpleclientInc                    thrpt   15       6552.567    ± 153.714  ops/s
CounterBenchmark.simpleclientNoLabelsInc            thrpt   15       6484.039    ± 127.963  ops/s
HistogramBenchmark.openTelemetryClassic             thrpt   15        671.558     ± 27.467  ops/s
HistogramBenchmark.openTelemetryExponential         thrpt   15        573.216     ± 18.525  ops/s
HistogramBenchmark.prometheusClassic                thrpt   15       4944.266   ± 1063.794  ops/s
HistogramBenchmark.prometheusNative                 thrpt   15       2670.943     ± 84.191  ops/s
HistogramBenchmark.simpleclient                     thrpt   15       4462.725     ± 51.432  ops/s
TextFormatUtilBenchmark.openMetricsWriteToByteArray  thrpt   15     473220.660   ± 2445.704  ops/s
TextFormatUtilBenchmark.openMetricsWriteToNull      thrpt   15     485702.409   ± 2627.479  ops/s
TextFormatUtilBenchmark.prometheusWriteToByteArray  thrpt   15     481974.859   ± 4105.416  ops/s
TextFormatUtilBenchmark.prometheusWriteToNull       thrpt   15     482699.170   ± 6563.196  ops/s
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
