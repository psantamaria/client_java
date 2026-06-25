# Prometheus Java Client Benchmarks

## Run Information

- **Date:** 2026-06-25T07:18:11Z
- **Commit:** [`4b69f40`](https://github.com/psantamaria/client_java/commit/4b69f40bd4e616d69468ce99dc4323162287a577)
- **JDK:** 25.0.2 (OpenJDK 64-Bit Server VM)
- **Benchmark config:** 3 fork(s), 3 warmup, 5 measurement, 4 threads
- **Hardware:** AMD EPYC 7763 64-Core Processor, 4 cores, 16 GB RAM
- **OS:** Linux 6.17.0-1018-azure

## Results

### CounterBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusInc | 66.08K | ± 301.50 | ops/s | **fastest** |
| prometheusNoLabelsInc | 56.58K | ± 327.41 | ops/s | 1.2x slower |
| prometheusAdd | 50.92K | ± 265.79 | ops/s | 1.3x slower |
| codahaleIncNoLabels | 49.97K | ± 540.33 | ops/s | 1.3x slower |
| simpleclientInc | 6.52K | ± 176.53 | ops/s | 10x slower |
| simpleclientNoLabelsInc | 6.38K | ± 194.21 | ops/s | 10x slower |
| simpleclientAdd | 6.20K | ± 390.17 | ops/s | 11x slower |
| openTelemetryAdd | 1.28K | ± 21.83 | ops/s | 52x slower |
| openTelemetryInc | 1.24K | ± 32.54 | ops/s | 53x slower |
| openTelemetryIncNoLabels | 1.18K | ± 79.96 | ops/s | 56x slower |

### HistogramBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusClassic | 5.27K | ± 1.36K | ops/s | **fastest** |
| simpleclient | 4.28K | ± 246.20 | ops/s | 1.2x slower |
| prometheusNative | 3.02K | ± 398.07 | ops/s | 1.7x slower |
| openTelemetryClassic | 693.94 | ± 14.48 | ops/s | 7.6x slower |
| openTelemetryExponential | 573.73 | ± 12.84 | ops/s | 9.2x slower |

### TextFormatUtilBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusWriteToNull | 496.29K | ± 5.86K | ops/s | **fastest** |
| prometheusWriteToByteArray | 490.51K | ± 842.80 | ops/s | 1.0x slower |
| openMetricsWriteToNull | 487.01K | ± 1.91K | ops/s | 1.0x slower |
| openMetricsWriteToByteArray | 478.04K | ± 5.37K | ops/s | 1.0x slower |

### Raw Results

```
Benchmark                                            Mode  Cnt          Score        Error  Units
CounterBenchmark.codahaleIncNoLabels                thrpt   15      49972.394    ± 540.326  ops/s
CounterBenchmark.openTelemetryAdd                   thrpt   15       1280.211     ± 21.830  ops/s
CounterBenchmark.openTelemetryInc                   thrpt   15       1242.584     ± 32.537  ops/s
CounterBenchmark.openTelemetryIncNoLabels           thrpt   15       1175.864     ± 79.959  ops/s
CounterBenchmark.prometheusAdd                      thrpt   15      50923.305    ± 265.790  ops/s
CounterBenchmark.prometheusInc                      thrpt   15      66079.488    ± 301.497  ops/s
CounterBenchmark.prometheusNoLabelsInc              thrpt   15      56577.633    ± 327.408  ops/s
CounterBenchmark.simpleclientAdd                    thrpt   15       6201.398    ± 390.171  ops/s
CounterBenchmark.simpleclientInc                    thrpt   15       6515.764    ± 176.530  ops/s
CounterBenchmark.simpleclientNoLabelsInc            thrpt   15       6376.185    ± 194.212  ops/s
HistogramBenchmark.openTelemetryClassic             thrpt   15        693.939     ± 14.481  ops/s
HistogramBenchmark.openTelemetryExponential         thrpt   15        573.731     ± 12.843  ops/s
HistogramBenchmark.prometheusClassic                thrpt   15       5271.943   ± 1360.808  ops/s
HistogramBenchmark.prometheusNative                 thrpt   15       3022.304    ± 398.072  ops/s
HistogramBenchmark.simpleclient                     thrpt   15       4278.163    ± 246.204  ops/s
TextFormatUtilBenchmark.openMetricsWriteToByteArray  thrpt   15     478042.457   ± 5368.988  ops/s
TextFormatUtilBenchmark.openMetricsWriteToNull      thrpt   15     487011.497   ± 1909.408  ops/s
TextFormatUtilBenchmark.prometheusWriteToByteArray  thrpt   15     490507.621    ± 842.796  ops/s
TextFormatUtilBenchmark.prometheusWriteToNull       thrpt   15     496290.388   ± 5863.153  ops/s
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
