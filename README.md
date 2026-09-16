# Prometheus Java Client Benchmarks

## Run Information

- **Date:** 2026-09-16T08:21:35Z
- **Commit:** [`4b69f40`](https://github.com/psantamaria/client_java/commit/4b69f40bd4e616d69468ce99dc4323162287a577)
- **JDK:** 25.0.2 (OpenJDK 64-Bit Server VM)
- **Benchmark config:** 3 fork(s), 3 warmup, 5 measurement, 4 threads
- **Hardware:** AMD EPYC 9V45 96-Core Processor, 4 cores, 16 GB RAM
- **OS:** Linux 6.17.0-1022-azure

## Results

### CounterBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusNoLabelsInc | 66.50K | ± 1.06K | ops/s | **fastest** |
| prometheusInc | 65.38K | ± 2.71K | ops/s | 1.0x slower |
| codahaleIncNoLabels | 60.88K | ± 1.05K | ops/s | 1.1x slower |
| prometheusAdd | 58.01K | ± 1.68K | ops/s | 1.1x slower |
| simpleclientAdd | 10.72K | ± 357.02 | ops/s | 6.2x slower |
| simpleclientInc | 10.64K | ± 228.53 | ops/s | 6.3x slower |
| simpleclientNoLabelsInc | 10.58K | ± 292.77 | ops/s | 6.3x slower |
| openTelemetryIncNoLabels | 1.90K | ± 213.29 | ops/s | 35x slower |
| openTelemetryInc | 1.85K | ± 298.76 | ops/s | 36x slower |
| openTelemetryAdd | 1.72K | ± 95.20 | ops/s | 39x slower |

### HistogramBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusClassic | 7.54K | ± 2.49K | ops/s | **fastest** |
| simpleclient | 7.04K | ± 74.20 | ops/s | 1.1x slower |
| prometheusNative | 5.17K | ± 491.76 | ops/s | 1.5x slower |
| openTelemetryClassic | 912.92 | ± 68.93 | ops/s | 8.3x slower |
| openTelemetryExponential | 736.34 | ± 23.82 | ops/s | 10x slower |

### TextFormatUtilBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusWriteToNull | 758.05K | ± 46.76K | ops/s | **fastest** |
| prometheusWriteToByteArray | 739.06K | ± 31.80K | ops/s | 1.0x slower |
| openMetricsWriteToByteArray | 677.82K | ± 28.00K | ops/s | 1.1x slower |
| openMetricsWriteToNull | 647.31K | ± 18.45K | ops/s | 1.2x slower |

### Raw Results

```
Benchmark                                            Mode  Cnt          Score        Error  Units
CounterBenchmark.codahaleIncNoLabels                thrpt   15      60877.857   ± 1049.903  ops/s
CounterBenchmark.openTelemetryAdd                   thrpt   15       1724.376     ± 95.201  ops/s
CounterBenchmark.openTelemetryInc                   thrpt   15       1849.569    ± 298.764  ops/s
CounterBenchmark.openTelemetryIncNoLabels           thrpt   15       1896.751    ± 213.294  ops/s
CounterBenchmark.prometheusAdd                      thrpt   15      58007.467   ± 1679.806  ops/s
CounterBenchmark.prometheusInc                      thrpt   15      65380.297   ± 2711.589  ops/s
CounterBenchmark.prometheusNoLabelsInc              thrpt   15      66500.103   ± 1060.779  ops/s
CounterBenchmark.simpleclientAdd                    thrpt   15      10716.168    ± 357.021  ops/s
CounterBenchmark.simpleclientInc                    thrpt   15      10637.061    ± 228.533  ops/s
CounterBenchmark.simpleclientNoLabelsInc            thrpt   15      10578.559    ± 292.768  ops/s
HistogramBenchmark.openTelemetryClassic             thrpt   15        912.922     ± 68.930  ops/s
HistogramBenchmark.openTelemetryExponential         thrpt   15        736.342     ± 23.820  ops/s
HistogramBenchmark.prometheusClassic                thrpt   15       7543.114   ± 2490.352  ops/s
HistogramBenchmark.prometheusNative                 thrpt   15       5170.360    ± 491.762  ops/s
HistogramBenchmark.simpleclient                     thrpt   15       7040.944     ± 74.200  ops/s
TextFormatUtilBenchmark.openMetricsWriteToByteArray  thrpt   15     677816.556  ± 27995.066  ops/s
TextFormatUtilBenchmark.openMetricsWriteToNull      thrpt   15     647313.606  ± 18446.119  ops/s
TextFormatUtilBenchmark.prometheusWriteToByteArray  thrpt   15     739063.647  ± 31797.212  ops/s
TextFormatUtilBenchmark.prometheusWriteToNull       thrpt   15     758053.773  ± 46756.105  ops/s
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
