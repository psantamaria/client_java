# Prometheus Java Client Benchmarks

## Run Information

- **Date:** 2026-07-27T07:00:32Z
- **Commit:** [`4b69f40`](https://github.com/psantamaria/client_java/commit/4b69f40bd4e616d69468ce99dc4323162287a577)
- **JDK:** 25.0.2 (OpenJDK 64-Bit Server VM)
- **Benchmark config:** 3 fork(s), 3 warmup, 5 measurement, 4 threads
- **Hardware:** INTEL(R) XEON(R) PLATINUM 8573C, 4 cores, 16 GB RAM
- **OS:** Linux 6.17.0-1020-azure

## Results

### CounterBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusNoLabelsInc | 29.14K | ± 540.16 | ops/s | **fastest** |
| prometheusInc | 28.49K | ± 529.08 | ops/s | 1.0x slower |
| codahaleIncNoLabels | 28.38K | ± 1.61K | ops/s | 1.0x slower |
| prometheusAdd | 27.90K | ± 370.94 | ops/s | 1.0x slower |
| simpleclientAdd | 7.18K | ± 127.30 | ops/s | 4.1x slower |
| simpleclientInc | 7.17K | ± 128.05 | ops/s | 4.1x slower |
| simpleclientNoLabelsInc | 7.07K | ± 178.05 | ops/s | 4.1x slower |
| openTelemetryAdd | 1.22K | ± 89.02 | ops/s | 24x slower |
| openTelemetryIncNoLabels | 1.18K | ± 39.18 | ops/s | 25x slower |
| openTelemetryInc | 1.05K | ± 73.49 | ops/s | 28x slower |

### HistogramBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| simpleclient | 4.72K | ± 67.25 | ops/s | **fastest** |
| prometheusClassic | 2.88K | ± 722.73 | ops/s | 1.6x slower |
| prometheusNative | 2.30K | ± 231.15 | ops/s | 2.0x slower |
| openTelemetryClassic | 393.44 | ± 18.99 | ops/s | 12x slower |
| openTelemetryExponential | 335.53 | ± 35.14 | ops/s | 14x slower |

### TextFormatUtilBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusWriteToNull | 301.23K | ± 4.55K | ops/s | **fastest** |
| prometheusWriteToByteArray | 298.56K | ± 2.66K | ops/s | 1.0x slower |
| openMetricsWriteToNull | 283.54K | ± 1.72K | ops/s | 1.1x slower |
| openMetricsWriteToByteArray | 281.11K | ± 3.41K | ops/s | 1.1x slower |

### Raw Results

```
Benchmark                                            Mode  Cnt          Score        Error  Units
CounterBenchmark.codahaleIncNoLabels                thrpt   15      28381.215   ± 1610.807  ops/s
CounterBenchmark.openTelemetryAdd                   thrpt   15       1223.797     ± 89.018  ops/s
CounterBenchmark.openTelemetryInc                   thrpt   15       1046.291     ± 73.490  ops/s
CounterBenchmark.openTelemetryIncNoLabels           thrpt   15       1184.803     ± 39.178  ops/s
CounterBenchmark.prometheusAdd                      thrpt   15      27900.718    ± 370.936  ops/s
CounterBenchmark.prometheusInc                      thrpt   15      28493.781    ± 529.076  ops/s
CounterBenchmark.prometheusNoLabelsInc              thrpt   15      29144.593    ± 540.155  ops/s
CounterBenchmark.simpleclientAdd                    thrpt   15       7181.878    ± 127.298  ops/s
CounterBenchmark.simpleclientInc                    thrpt   15       7173.875    ± 128.047  ops/s
CounterBenchmark.simpleclientNoLabelsInc            thrpt   15       7074.357    ± 178.045  ops/s
HistogramBenchmark.openTelemetryClassic             thrpt   15        393.444     ± 18.994  ops/s
HistogramBenchmark.openTelemetryExponential         thrpt   15        335.529     ± 35.140  ops/s
HistogramBenchmark.prometheusClassic                thrpt   15       2884.449    ± 722.727  ops/s
HistogramBenchmark.prometheusNative                 thrpt   15       2302.637    ± 231.152  ops/s
HistogramBenchmark.simpleclient                     thrpt   15       4717.600     ± 67.254  ops/s
TextFormatUtilBenchmark.openMetricsWriteToByteArray  thrpt   15     281110.948   ± 3414.462  ops/s
TextFormatUtilBenchmark.openMetricsWriteToNull      thrpt   15     283537.155   ± 1715.272  ops/s
TextFormatUtilBenchmark.prometheusWriteToByteArray  thrpt   15     298558.267   ± 2659.387  ops/s
TextFormatUtilBenchmark.prometheusWriteToNull       thrpt   15     301228.074   ± 4545.340  ops/s
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
