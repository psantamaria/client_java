# Prometheus Java Client Benchmarks

## Run Information

- **Date:** 2026-08-27T13:31:44Z
- **Commit:** [`4b69f40`](https://github.com/psantamaria/client_java/commit/4b69f40bd4e616d69468ce99dc4323162287a577)
- **JDK:** 25.0.2 (OpenJDK 64-Bit Server VM)
- **Benchmark config:** 3 fork(s), 3 warmup, 5 measurement, 4 threads
- **Hardware:** AMD EPYC 7763 64-Core Processor, 4 cores, 16 GB RAM
- **OS:** Linux 6.17.0-1022-azure

## Results

### CounterBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusInc | 63.96K | ± 604.37 | ops/s | **fastest** |
| prometheusNoLabelsInc | 56.83K | ± 265.76 | ops/s | 1.1x slower |
| prometheusAdd | 51.34K | ± 111.00 | ops/s | 1.2x slower |
| codahaleIncNoLabels | 49.37K | ± 1.33K | ops/s | 1.3x slower |
| simpleclientInc | 6.46K | ± 385.59 | ops/s | 9.9x slower |
| simpleclientNoLabelsInc | 6.40K | ± 165.05 | ops/s | 10.0x slower |
| simpleclientAdd | 6.35K | ± 208.07 | ops/s | 10x slower |
| openTelemetryIncNoLabels | 1.33K | ± 124.08 | ops/s | 48x slower |
| openTelemetryAdd | 1.25K | ± 30.73 | ops/s | 51x slower |
| openTelemetryInc | 1.24K | ± 20.15 | ops/s | 52x slower |

### HistogramBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusClassic | 5.07K | ± 1.75K | ops/s | **fastest** |
| simpleclient | 4.43K | ± 62.13 | ops/s | 1.1x slower |
| prometheusNative | 2.81K | ± 334.11 | ops/s | 1.8x slower |
| openTelemetryClassic | 682.73 | ± 25.86 | ops/s | 7.4x slower |
| openTelemetryExponential | 560.95 | ± 18.31 | ops/s | 9.0x slower |

### TextFormatUtilBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusWriteToNull | 477.81K | ± 5.67K | ops/s | **fastest** |
| prometheusWriteToByteArray | 472.63K | ± 4.42K | ops/s | 1.0x slower |
| openMetricsWriteToNull | 468.88K | ± 3.55K | ops/s | 1.0x slower |
| openMetricsWriteToByteArray | 449.36K | ± 2.45K | ops/s | 1.1x slower |

### Raw Results

```
Benchmark                                            Mode  Cnt          Score        Error  Units
CounterBenchmark.codahaleIncNoLabels                thrpt   15      49371.134   ± 1329.628  ops/s
CounterBenchmark.openTelemetryAdd                   thrpt   15       1249.927     ± 30.732  ops/s
CounterBenchmark.openTelemetryInc                   thrpt   15       1235.910     ± 20.151  ops/s
CounterBenchmark.openTelemetryIncNoLabels           thrpt   15       1328.495    ± 124.081  ops/s
CounterBenchmark.prometheusAdd                      thrpt   15      51335.208    ± 110.996  ops/s
CounterBenchmark.prometheusInc                      thrpt   15      63960.275    ± 604.367  ops/s
CounterBenchmark.prometheusNoLabelsInc              thrpt   15      56832.605    ± 265.763  ops/s
CounterBenchmark.simpleclientAdd                    thrpt   15       6351.608    ± 208.068  ops/s
CounterBenchmark.simpleclientInc                    thrpt   15       6462.379    ± 385.587  ops/s
CounterBenchmark.simpleclientNoLabelsInc            thrpt   15       6399.061    ± 165.049  ops/s
HistogramBenchmark.openTelemetryClassic             thrpt   15        682.733     ± 25.859  ops/s
HistogramBenchmark.openTelemetryExponential         thrpt   15        560.955     ± 18.307  ops/s
HistogramBenchmark.prometheusClassic                thrpt   15       5073.666   ± 1746.362  ops/s
HistogramBenchmark.prometheusNative                 thrpt   15       2805.818    ± 334.111  ops/s
HistogramBenchmark.simpleclient                     thrpt   15       4431.262     ± 62.127  ops/s
TextFormatUtilBenchmark.openMetricsWriteToByteArray  thrpt   15     449364.898   ± 2445.662  ops/s
TextFormatUtilBenchmark.openMetricsWriteToNull      thrpt   15     468881.623   ± 3548.523  ops/s
TextFormatUtilBenchmark.prometheusWriteToByteArray  thrpt   15     472631.003   ± 4424.654  ops/s
TextFormatUtilBenchmark.prometheusWriteToNull       thrpt   15     477810.649   ± 5673.891  ops/s
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
