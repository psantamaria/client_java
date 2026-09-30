# Prometheus Java Client Benchmarks

## Run Information

- **Date:** 2026-09-30T09:06:10Z
- **Commit:** [`4b69f40`](https://github.com/psantamaria/client_java/commit/4b69f40bd4e616d69468ce99dc4323162287a577)
- **JDK:** 25.0.2 (OpenJDK 64-Bit Server VM)
- **Benchmark config:** 3 fork(s), 3 warmup, 5 measurement, 4 threads
- **Hardware:** AMD EPYC 9V74 80-Core Processor, 4 cores, 16 GB RAM
- **OS:** Linux 6.17.0-1022-azure

## Results

### CounterBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusInc | 56.70K | ± 2.09K | ops/s | **fastest** |
| prometheusNoLabelsInc | 50.46K | ± 1.00K | ops/s | 1.1x slower |
| prometheusAdd | 47.10K | ± 536.83 | ops/s | 1.2x slower |
| codahaleIncNoLabels | 43.50K | ± 653.80 | ops/s | 1.3x slower |
| simpleclientInc | 6.22K | ± 59.84 | ops/s | 9.1x slower |
| simpleclientAdd | 5.90K | ± 170.03 | ops/s | 9.6x slower |
| simpleclientNoLabelsInc | 5.86K | ± 170.22 | ops/s | 9.7x slower |
| openTelemetryInc | 1.30K | ± 133.51 | ops/s | 44x slower |
| openTelemetryAdd | 1.30K | ± 56.51 | ops/s | 44x slower |
| openTelemetryIncNoLabels | 1.29K | ± 148.78 | ops/s | 44x slower |

### HistogramBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusClassic | 5.62K | ± 1.28K | ops/s | **fastest** |
| simpleclient | 4.19K | ± 119.98 | ops/s | 1.3x slower |
| prometheusNative | 2.78K | ± 170.33 | ops/s | 2.0x slower |
| openTelemetryClassic | 580.27 | ± 30.24 | ops/s | 9.7x slower |
| openTelemetryExponential | 492.57 | ± 37.21 | ops/s | 11x slower |

### TextFormatUtilBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusWriteToNull | 526.09K | ± 5.92K | ops/s | **fastest** |
| prometheusWriteToByteArray | 515.89K | ± 4.30K | ops/s | 1.0x slower |
| openMetricsWriteToNull | 508.44K | ± 4.39K | ops/s | 1.0x slower |
| openMetricsWriteToByteArray | 489.06K | ± 6.15K | ops/s | 1.1x slower |

### Raw Results

```
Benchmark                                            Mode  Cnt          Score        Error  Units
CounterBenchmark.codahaleIncNoLabels                thrpt   15      43503.648    ± 653.803  ops/s
CounterBenchmark.openTelemetryAdd                   thrpt   15       1299.533     ± 56.508  ops/s
CounterBenchmark.openTelemetryInc                   thrpt   15       1302.189    ± 133.514  ops/s
CounterBenchmark.openTelemetryIncNoLabels           thrpt   15       1288.479    ± 148.783  ops/s
CounterBenchmark.prometheusAdd                      thrpt   15      47100.477    ± 536.828  ops/s
CounterBenchmark.prometheusInc                      thrpt   15      56698.735   ± 2088.644  ops/s
CounterBenchmark.prometheusNoLabelsInc              thrpt   15      50460.670   ± 1002.610  ops/s
CounterBenchmark.simpleclientAdd                    thrpt   15       5901.035    ± 170.030  ops/s
CounterBenchmark.simpleclientInc                    thrpt   15       6223.260     ± 59.845  ops/s
CounterBenchmark.simpleclientNoLabelsInc            thrpt   15       5864.720    ± 170.221  ops/s
HistogramBenchmark.openTelemetryClassic             thrpt   15        580.271     ± 30.238  ops/s
HistogramBenchmark.openTelemetryExponential         thrpt   15        492.566     ± 37.205  ops/s
HistogramBenchmark.prometheusClassic                thrpt   15       5619.270   ± 1279.556  ops/s
HistogramBenchmark.prometheusNative                 thrpt   15       2783.733    ± 170.332  ops/s
HistogramBenchmark.simpleclient                     thrpt   15       4187.872    ± 119.981  ops/s
TextFormatUtilBenchmark.openMetricsWriteToByteArray  thrpt   15     489057.234   ± 6154.531  ops/s
TextFormatUtilBenchmark.openMetricsWriteToNull      thrpt   15     508444.568   ± 4387.369  ops/s
TextFormatUtilBenchmark.prometheusWriteToByteArray  thrpt   15     515894.710   ± 4295.901  ops/s
TextFormatUtilBenchmark.prometheusWriteToNull       thrpt   15     526086.694   ± 5915.292  ops/s
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
