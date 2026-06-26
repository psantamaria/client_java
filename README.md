# Prometheus Java Client Benchmarks

## Run Information

- **Date:** 2026-06-26T07:21:59Z
- **Commit:** [`4b69f40`](https://github.com/psantamaria/client_java/commit/4b69f40bd4e616d69468ce99dc4323162287a577)
- **JDK:** 25.0.2 (OpenJDK 64-Bit Server VM)
- **Benchmark config:** 3 fork(s), 3 warmup, 5 measurement, 4 threads
- **Hardware:** AMD EPYC 9V74 80-Core Processor, 4 cores, 16 GB RAM
- **OS:** Linux 6.17.0-1018-azure

## Results

### CounterBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusInc | 59.88K | ± 1.20K | ops/s | **fastest** |
| prometheusNoLabelsInc | 51.71K | ± 907.90 | ops/s | 1.2x slower |
| prometheusAdd | 47.33K | ± 140.46 | ops/s | 1.3x slower |
| codahaleIncNoLabels | 44.23K | ± 278.21 | ops/s | 1.4x slower |
| simpleclientInc | 6.31K | ± 53.53 | ops/s | 9.5x slower |
| simpleclientNoLabelsInc | 6.26K | ± 30.90 | ops/s | 9.6x slower |
| simpleclientAdd | 5.60K | ± 156.76 | ops/s | 11x slower |
| openTelemetryIncNoLabels | 1.46K | ± 96.05 | ops/s | 41x slower |
| openTelemetryInc | 1.42K | ± 149.07 | ops/s | 42x slower |
| openTelemetryAdd | 1.29K | ± 19.66 | ops/s | 46x slower |

### HistogramBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusClassic | 5.09K | ± 1.91K | ops/s | **fastest** |
| simpleclient | 4.51K | ± 128.47 | ops/s | 1.1x slower |
| prometheusNative | 2.78K | ± 118.86 | ops/s | 1.8x slower |
| openTelemetryClassic | 624.61 | ± 45.11 | ops/s | 8.1x slower |
| openTelemetryExponential | 504.58 | ± 21.70 | ops/s | 10x slower |

### TextFormatUtilBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusWriteToNull | 537.45K | ± 2.99K | ops/s | **fastest** |
| prometheusWriteToByteArray | 525.89K | ± 8.18K | ops/s | 1.0x slower |
| openMetricsWriteToNull | 516.02K | ± 7.99K | ops/s | 1.0x slower |
| openMetricsWriteToByteArray | 511.92K | ± 4.70K | ops/s | 1.0x slower |

### Raw Results

```
Benchmark                                            Mode  Cnt          Score        Error  Units
CounterBenchmark.codahaleIncNoLabels                thrpt   15      44232.731    ± 278.213  ops/s
CounterBenchmark.openTelemetryAdd                   thrpt   15       1290.169     ± 19.658  ops/s
CounterBenchmark.openTelemetryInc                   thrpt   15       1417.237    ± 149.074  ops/s
CounterBenchmark.openTelemetryIncNoLabels           thrpt   15       1459.144     ± 96.055  ops/s
CounterBenchmark.prometheusAdd                      thrpt   15      47334.209    ± 140.461  ops/s
CounterBenchmark.prometheusInc                      thrpt   15      59878.466   ± 1203.107  ops/s
CounterBenchmark.prometheusNoLabelsInc              thrpt   15      51713.033    ± 907.904  ops/s
CounterBenchmark.simpleclientAdd                    thrpt   15       5596.310    ± 156.756  ops/s
CounterBenchmark.simpleclientInc                    thrpt   15       6312.162     ± 53.531  ops/s
CounterBenchmark.simpleclientNoLabelsInc            thrpt   15       6260.540     ± 30.902  ops/s
HistogramBenchmark.openTelemetryClassic             thrpt   15        624.605     ± 45.108  ops/s
HistogramBenchmark.openTelemetryExponential         thrpt   15        504.585     ± 21.703  ops/s
HistogramBenchmark.prometheusClassic                thrpt   15       5089.399   ± 1914.983  ops/s
HistogramBenchmark.prometheusNative                 thrpt   15       2781.931    ± 118.863  ops/s
HistogramBenchmark.simpleclient                     thrpt   15       4509.048    ± 128.471  ops/s
TextFormatUtilBenchmark.openMetricsWriteToByteArray  thrpt   15     511916.632   ± 4697.184  ops/s
TextFormatUtilBenchmark.openMetricsWriteToNull      thrpt   15     516024.781   ± 7987.523  ops/s
TextFormatUtilBenchmark.prometheusWriteToByteArray  thrpt   15     525891.091   ± 8177.574  ops/s
TextFormatUtilBenchmark.prometheusWriteToNull       thrpt   15     537454.284   ± 2992.122  ops/s
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
