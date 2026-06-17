# Prometheus Java Client Benchmarks

## Run Information

- **Date:** 2026-06-17T08:20:36Z
- **Commit:** [`4b69f40`](https://github.com/psantamaria/client_java/commit/4b69f40bd4e616d69468ce99dc4323162287a577)
- **JDK:** 25.0.2 (OpenJDK 64-Bit Server VM)
- **Benchmark config:** 3 fork(s), 3 warmup, 5 measurement, 4 threads
- **Hardware:** AMD EPYC 7763 64-Core Processor, 4 cores, 16 GB RAM
- **OS:** Linux 6.17.0-1018-azure

## Results

### CounterBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusInc | 64.90K | ± 1.83K | ops/s | **fastest** |
| prometheusNoLabelsInc | 56.52K | ± 559.33 | ops/s | 1.1x slower |
| prometheusAdd | 50.91K | ± 751.70 | ops/s | 1.3x slower |
| codahaleIncNoLabels | 48.59K | ± 1.95K | ops/s | 1.3x slower |
| simpleclientNoLabelsInc | 6.52K | ± 145.81 | ops/s | 10.0x slower |
| simpleclientInc | 6.47K | ± 156.55 | ops/s | 10x slower |
| simpleclientAdd | 6.18K | ± 211.45 | ops/s | 10x slower |
| openTelemetryInc | 1.39K | ± 84.20 | ops/s | 47x slower |
| openTelemetryIncNoLabels | 1.39K | ± 188.87 | ops/s | 47x slower |
| openTelemetryAdd | 1.23K | ± 51.59 | ops/s | 53x slower |

### HistogramBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusClassic | 5.45K | ± 1.43K | ops/s | **fastest** |
| simpleclient | 4.41K | ± 100.25 | ops/s | 1.2x slower |
| prometheusNative | 3.05K | ± 327.79 | ops/s | 1.8x slower |
| openTelemetryClassic | 689.45 | ± 18.91 | ops/s | 7.9x slower |
| openTelemetryExponential | 564.64 | ± 5.84 | ops/s | 9.7x slower |

### TextFormatUtilBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusWriteToNull | 424.91K | ± 32.57K | ops/s | **fastest** |
| openMetricsWriteToByteArray | 411.48K | ± 6.12K | ops/s | 1.0x slower |
| openMetricsWriteToNull | 407.99K | ± 6.99K | ops/s | 1.0x slower |
| prometheusWriteToByteArray | 403.03K | ± 7.99K | ops/s | 1.1x slower |

### Raw Results

```
Benchmark                                            Mode  Cnt          Score        Error  Units
CounterBenchmark.codahaleIncNoLabels                thrpt   15      48590.074   ± 1948.432  ops/s
CounterBenchmark.openTelemetryAdd                   thrpt   15       1232.847     ± 51.586  ops/s
CounterBenchmark.openTelemetryInc                   thrpt   15       1390.770     ± 84.201  ops/s
CounterBenchmark.openTelemetryIncNoLabels           thrpt   15       1385.928    ± 188.874  ops/s
CounterBenchmark.prometheusAdd                      thrpt   15      50912.184    ± 751.704  ops/s
CounterBenchmark.prometheusInc                      thrpt   15      64902.001   ± 1831.273  ops/s
CounterBenchmark.prometheusNoLabelsInc              thrpt   15      56521.519    ± 559.328  ops/s
CounterBenchmark.simpleclientAdd                    thrpt   15       6183.388    ± 211.448  ops/s
CounterBenchmark.simpleclientInc                    thrpt   15       6471.093    ± 156.554  ops/s
CounterBenchmark.simpleclientNoLabelsInc            thrpt   15       6521.315    ± 145.810  ops/s
HistogramBenchmark.openTelemetryClassic             thrpt   15        689.448     ± 18.906  ops/s
HistogramBenchmark.openTelemetryExponential         thrpt   15        564.645      ± 5.842  ops/s
HistogramBenchmark.prometheusClassic                thrpt   15       5453.647   ± 1433.882  ops/s
HistogramBenchmark.prometheusNative                 thrpt   15       3054.114    ± 327.787  ops/s
HistogramBenchmark.simpleclient                     thrpt   15       4412.979    ± 100.246  ops/s
TextFormatUtilBenchmark.openMetricsWriteToByteArray  thrpt   15     411477.156   ± 6115.970  ops/s
TextFormatUtilBenchmark.openMetricsWriteToNull      thrpt   15     407985.496   ± 6989.304  ops/s
TextFormatUtilBenchmark.prometheusWriteToByteArray  thrpt   15     403027.086   ± 7989.868  ops/s
TextFormatUtilBenchmark.prometheusWriteToNull       thrpt   15     424907.763  ± 32572.391  ops/s
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
