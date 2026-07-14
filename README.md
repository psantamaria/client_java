# Prometheus Java Client Benchmarks

## Run Information

- **Date:** 2026-07-14T06:03:33Z
- **Commit:** [`4b69f40`](https://github.com/psantamaria/client_java/commit/4b69f40bd4e616d69468ce99dc4323162287a577)
- **JDK:** 25.0.2 (OpenJDK 64-Bit Server VM)
- **Benchmark config:** 3 fork(s), 3 warmup, 5 measurement, 4 threads
- **Hardware:** AMD EPYC 9V74 80-Core Processor, 4 cores, 16 GB RAM
- **OS:** Linux 6.17.0-1018-azure

## Results

### CounterBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusInc | 59.93K | ± 48.66 | ops/s | **fastest** |
| prometheusNoLabelsInc | 51.13K | ± 467.34 | ops/s | 1.2x slower |
| prometheusAdd | 48.38K | ± 203.49 | ops/s | 1.2x slower |
| codahaleIncNoLabels | 44.50K | ± 290.70 | ops/s | 1.3x slower |
| simpleclientInc | 6.26K | ± 159.03 | ops/s | 9.6x slower |
| simpleclientNoLabelsInc | 6.22K | ± 30.85 | ops/s | 9.6x slower |
| simpleclientAdd | 5.72K | ± 172.19 | ops/s | 10x slower |
| openTelemetryAdd | 1.27K | ± 19.10 | ops/s | 47x slower |
| openTelemetryInc | 1.26K | ± 62.68 | ops/s | 48x slower |
| openTelemetryIncNoLabels | 1.20K | ± 48.20 | ops/s | 50x slower |

### HistogramBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusClassic | 6.12K | ± 1.08K | ops/s | **fastest** |
| simpleclient | 4.45K | ± 54.01 | ops/s | 1.4x slower |
| prometheusNative | 2.95K | ± 122.74 | ops/s | 2.1x slower |
| openTelemetryClassic | 595.68 | ± 28.11 | ops/s | 10x slower |
| openTelemetryExponential | 522.89 | ± 10.94 | ops/s | 12x slower |

### TextFormatUtilBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusWriteToNull | 536.98K | ± 4.14K | ops/s | **fastest** |
| prometheusWriteToByteArray | 523.47K | ± 4.47K | ops/s | 1.0x slower |
| openMetricsWriteToNull | 518.53K | ± 7.28K | ops/s | 1.0x slower |
| openMetricsWriteToByteArray | 503.43K | ± 4.04K | ops/s | 1.1x slower |

### Raw Results

```
Benchmark                                            Mode  Cnt          Score        Error  Units
CounterBenchmark.codahaleIncNoLabels                thrpt   15      44500.077    ± 290.695  ops/s
CounterBenchmark.openTelemetryAdd                   thrpt   15       1272.482     ± 19.097  ops/s
CounterBenchmark.openTelemetryInc                   thrpt   15       1258.299     ± 62.678  ops/s
CounterBenchmark.openTelemetryIncNoLabels           thrpt   15       1199.014     ± 48.198  ops/s
CounterBenchmark.prometheusAdd                      thrpt   15      48379.168    ± 203.492  ops/s
CounterBenchmark.prometheusInc                      thrpt   15      59932.110     ± 48.656  ops/s
CounterBenchmark.prometheusNoLabelsInc              thrpt   15      51131.198    ± 467.335  ops/s
CounterBenchmark.simpleclientAdd                    thrpt   15       5720.888    ± 172.189  ops/s
CounterBenchmark.simpleclientInc                    thrpt   15       6263.439    ± 159.031  ops/s
CounterBenchmark.simpleclientNoLabelsInc            thrpt   15       6224.895     ± 30.845  ops/s
HistogramBenchmark.openTelemetryClassic             thrpt   15        595.685     ± 28.107  ops/s
HistogramBenchmark.openTelemetryExponential         thrpt   15        522.890     ± 10.936  ops/s
HistogramBenchmark.prometheusClassic                thrpt   15       6119.404   ± 1082.748  ops/s
HistogramBenchmark.prometheusNative                 thrpt   15       2953.951    ± 122.745  ops/s
HistogramBenchmark.simpleclient                     thrpt   15       4451.464     ± 54.011  ops/s
TextFormatUtilBenchmark.openMetricsWriteToByteArray  thrpt   15     503433.207   ± 4043.919  ops/s
TextFormatUtilBenchmark.openMetricsWriteToNull      thrpt   15     518525.516   ± 7280.644  ops/s
TextFormatUtilBenchmark.prometheusWriteToByteArray  thrpt   15     523470.903   ± 4474.561  ops/s
TextFormatUtilBenchmark.prometheusWriteToNull       thrpt   15     536977.882   ± 4141.009  ops/s
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
