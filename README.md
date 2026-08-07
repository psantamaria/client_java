# Prometheus Java Client Benchmarks

## Run Information

- **Date:** 2026-08-07T05:38:26Z
- **Commit:** [`4b69f40`](https://github.com/psantamaria/client_java/commit/4b69f40bd4e616d69468ce99dc4323162287a577)
- **JDK:** 25.0.2 (OpenJDK 64-Bit Server VM)
- **Benchmark config:** 3 fork(s), 3 warmup, 5 measurement, 4 threads
- **Hardware:** AMD EPYC 9V74 80-Core Processor, 4 cores, 16 GB RAM
- **OS:** Linux 6.17.0-1021-azure

## Results

### CounterBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusInc | 76.31K | ± 2.14K | ops/s | **fastest** |
| prometheusNoLabelsInc | 67.27K | ± 649.88 | ops/s | 1.1x slower |
| prometheusAdd | 62.84K | ± 1.13K | ops/s | 1.2x slower |
| codahaleIncNoLabels | 56.80K | ± 154.36 | ops/s | 1.3x slower |
| simpleclientAdd | 7.96K | ± 43.25 | ops/s | 9.6x slower |
| simpleclientNoLabelsInc | 7.87K | ± 278.60 | ops/s | 9.7x slower |
| simpleclientInc | 7.84K | ± 213.61 | ops/s | 9.7x slower |
| openTelemetryAdd | 1.86K | ± 67.03 | ops/s | 41x slower |
| openTelemetryIncNoLabels | 1.84K | ± 98.15 | ops/s | 42x slower |
| openTelemetryInc | 1.74K | ± 187.54 | ops/s | 44x slower |

### HistogramBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusClassic | 7.98K | ± 2.23K | ops/s | **fastest** |
| simpleclient | 5.42K | ± 10.67 | ops/s | 1.5x slower |
| prometheusNative | 3.90K | ± 183.28 | ops/s | 2.0x slower |
| openTelemetryClassic | 803.65 | ± 2.10 | ops/s | 9.9x slower |
| openTelemetryExponential | 695.16 | ± 12.12 | ops/s | 11x slower |

### TextFormatUtilBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusWriteToNull | 681.13K | ± 8.89K | ops/s | **fastest** |
| prometheusWriteToByteArray | 667.62K | ± 8.70K | ops/s | 1.0x slower |
| openMetricsWriteToNull | 649.38K | ± 13.61K | ops/s | 1.0x slower |
| openMetricsWriteToByteArray | 646.50K | ± 4.86K | ops/s | 1.1x slower |

### Raw Results

```
Benchmark                                            Mode  Cnt          Score        Error  Units
CounterBenchmark.codahaleIncNoLabels                thrpt   15      56802.270    ± 154.358  ops/s
CounterBenchmark.openTelemetryAdd                   thrpt   15       1861.346     ± 67.027  ops/s
CounterBenchmark.openTelemetryInc                   thrpt   15       1735.699    ± 187.535  ops/s
CounterBenchmark.openTelemetryIncNoLabels           thrpt   15       1837.377     ± 98.154  ops/s
CounterBenchmark.prometheusAdd                      thrpt   15      62840.981   ± 1129.410  ops/s
CounterBenchmark.prometheusInc                      thrpt   15      76305.158   ± 2135.715  ops/s
CounterBenchmark.prometheusNoLabelsInc              thrpt   15      67270.547    ± 649.876  ops/s
CounterBenchmark.simpleclientAdd                    thrpt   15       7962.180     ± 43.250  ops/s
CounterBenchmark.simpleclientInc                    thrpt   15       7836.888    ± 213.612  ops/s
CounterBenchmark.simpleclientNoLabelsInc            thrpt   15       7865.144    ± 278.596  ops/s
HistogramBenchmark.openTelemetryClassic             thrpt   15        803.646      ± 2.100  ops/s
HistogramBenchmark.openTelemetryExponential         thrpt   15        695.162     ± 12.119  ops/s
HistogramBenchmark.prometheusClassic                thrpt   15       7984.743   ± 2233.442  ops/s
HistogramBenchmark.prometheusNative                 thrpt   15       3896.039    ± 183.279  ops/s
HistogramBenchmark.simpleclient                     thrpt   15       5422.226     ± 10.665  ops/s
TextFormatUtilBenchmark.openMetricsWriteToByteArray  thrpt   15     646502.935   ± 4855.696  ops/s
TextFormatUtilBenchmark.openMetricsWriteToNull      thrpt   15     649381.320  ± 13613.017  ops/s
TextFormatUtilBenchmark.prometheusWriteToByteArray  thrpt   15     667622.913   ± 8701.269  ops/s
TextFormatUtilBenchmark.prometheusWriteToNull       thrpt   15     681128.339   ± 8886.408  ops/s
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
