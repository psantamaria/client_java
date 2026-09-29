# Prometheus Java Client Benchmarks

## Run Information

- **Date:** 2026-09-29T09:02:58Z
- **Commit:** [`4b69f40`](https://github.com/psantamaria/client_java/commit/4b69f40bd4e616d69468ce99dc4323162287a577)
- **JDK:** 25.0.2 (OpenJDK 64-Bit Server VM)
- **Benchmark config:** 3 fork(s), 3 warmup, 5 measurement, 4 threads
- **Hardware:** AMD EPYC 7763 64-Core Processor, 4 cores, 16 GB RAM
- **OS:** Linux 6.17.0-1022-azure

## Results

### CounterBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusInc | 65.24K | ± 1.32K | ops/s | **fastest** |
| prometheusNoLabelsInc | 56.86K | ± 407.31 | ops/s | 1.1x slower |
| prometheusAdd | 51.27K | ± 277.05 | ops/s | 1.3x slower |
| codahaleIncNoLabels | 49.68K | ± 852.15 | ops/s | 1.3x slower |
| simpleclientInc | 6.50K | ± 200.38 | ops/s | 10x slower |
| simpleclientNoLabelsInc | 6.32K | ± 144.91 | ops/s | 10x slower |
| simpleclientAdd | 6.29K | ± 276.29 | ops/s | 10x slower |
| openTelemetryAdd | 1.55K | ± 268.06 | ops/s | 42x slower |
| openTelemetryIncNoLabels | 1.35K | ± 252.77 | ops/s | 48x slower |
| openTelemetryInc | 1.31K | ± 144.96 | ops/s | 50x slower |

### HistogramBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| simpleclient | 4.38K | ± 36.31 | ops/s | **fastest** |
| prometheusClassic | 4.28K | ± 411.45 | ops/s | 1.0x slower |
| prometheusNative | 2.76K | ± 374.85 | ops/s | 1.6x slower |
| openTelemetryClassic | 699.97 | ± 24.18 | ops/s | 6.3x slower |
| openTelemetryExponential | 559.29 | ± 10.39 | ops/s | 7.8x slower |

### TextFormatUtilBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusWriteToNull | 468.15K | ± 5.75K | ops/s | **fastest** |
| prometheusWriteToByteArray | 463.03K | ± 5.29K | ops/s | 1.0x slower |
| openMetricsWriteToNull | 460.32K | ± 10.35K | ops/s | 1.0x slower |
| openMetricsWriteToByteArray | 455.86K | ± 3.84K | ops/s | 1.0x slower |

### Raw Results

```
Benchmark                                            Mode  Cnt          Score        Error  Units
CounterBenchmark.codahaleIncNoLabels                thrpt   15      49684.687    ± 852.152  ops/s
CounterBenchmark.openTelemetryAdd                   thrpt   15       1553.188    ± 268.056  ops/s
CounterBenchmark.openTelemetryInc                   thrpt   15       1305.700    ± 144.956  ops/s
CounterBenchmark.openTelemetryIncNoLabels           thrpt   15       1351.330    ± 252.767  ops/s
CounterBenchmark.prometheusAdd                      thrpt   15      51268.985    ± 277.047  ops/s
CounterBenchmark.prometheusInc                      thrpt   15      65236.868   ± 1324.464  ops/s
CounterBenchmark.prometheusNoLabelsInc              thrpt   15      56855.951    ± 407.312  ops/s
CounterBenchmark.simpleclientAdd                    thrpt   15       6293.175    ± 276.293  ops/s
CounterBenchmark.simpleclientInc                    thrpt   15       6501.365    ± 200.376  ops/s
CounterBenchmark.simpleclientNoLabelsInc            thrpt   15       6315.791    ± 144.913  ops/s
HistogramBenchmark.openTelemetryClassic             thrpt   15        699.966     ± 24.176  ops/s
HistogramBenchmark.openTelemetryExponential         thrpt   15        559.287     ± 10.386  ops/s
HistogramBenchmark.prometheusClassic                thrpt   15       4282.175    ± 411.450  ops/s
HistogramBenchmark.prometheusNative                 thrpt   15       2759.308    ± 374.847  ops/s
HistogramBenchmark.simpleclient                     thrpt   15       4380.964     ± 36.305  ops/s
TextFormatUtilBenchmark.openMetricsWriteToByteArray  thrpt   15     455856.620   ± 3843.992  ops/s
TextFormatUtilBenchmark.openMetricsWriteToNull      thrpt   15     460321.100  ± 10346.636  ops/s
TextFormatUtilBenchmark.prometheusWriteToByteArray  thrpt   15     463026.881   ± 5294.132  ops/s
TextFormatUtilBenchmark.prometheusWriteToNull       thrpt   15     468151.233   ± 5747.338  ops/s
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
