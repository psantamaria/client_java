# Prometheus Java Client Benchmarks

## Run Information

- **Date:** 2026-09-07T08:10:29Z
- **Commit:** [`4b69f40`](https://github.com/psantamaria/client_java/commit/4b69f40bd4e616d69468ce99dc4323162287a577)
- **JDK:** 25.0.2 (OpenJDK 64-Bit Server VM)
- **Benchmark config:** 3 fork(s), 3 warmup, 5 measurement, 4 threads
- **Hardware:** INTEL(R) XEON(R) PLATINUM 8573C, 4 cores, 16 GB RAM
- **OS:** Linux 6.17.0-1022-azure

## Results

### CounterBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| codahaleIncNoLabels | 31.22K | ± 1.44K | ops/s | **fastest** |
| prometheusNoLabelsInc | 31.07K | ± 355.55 | ops/s | 1.0x slower |
| prometheusInc | 30.93K | ± 47.27 | ops/s | 1.0x slower |
| prometheusAdd | 30.20K | ± 95.36 | ops/s | 1.0x slower |
| simpleclientInc | 7.75K | ± 57.95 | ops/s | 4.0x slower |
| simpleclientNoLabelsInc | 7.70K | ± 72.33 | ops/s | 4.1x slower |
| simpleclientAdd | 7.58K | ± 122.25 | ops/s | 4.1x slower |
| openTelemetryAdd | 1.17K | ± 105.17 | ops/s | 27x slower |
| openTelemetryIncNoLabels | 1.14K | ± 32.57 | ops/s | 27x slower |
| openTelemetryInc | 1.09K | ± 48.14 | ops/s | 29x slower |

### HistogramBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| simpleclient | 5.05K | ± 22.08 | ops/s | **fastest** |
| prometheusClassic | 2.62K | ± 496.41 | ops/s | 1.9x slower |
| prometheusNative | 2.23K | ± 218.59 | ops/s | 2.3x slower |
| openTelemetryClassic | 409.72 | ± 24.66 | ops/s | 12x slower |
| openTelemetryExponential | 356.06 | ± 18.02 | ops/s | 14x slower |

### TextFormatUtilBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusWriteToNull | 337.21K | ± 4.57K | ops/s | **fastest** |
| prometheusWriteToByteArray | 330.37K | ± 8.28K | ops/s | 1.0x slower |
| openMetricsWriteToNull | 315.34K | ± 6.37K | ops/s | 1.1x slower |
| openMetricsWriteToByteArray | 313.44K | ± 7.59K | ops/s | 1.1x slower |

### Raw Results

```
Benchmark                                            Mode  Cnt          Score        Error  Units
CounterBenchmark.codahaleIncNoLabels                thrpt   15      31221.874   ± 1437.461  ops/s
CounterBenchmark.openTelemetryAdd                   thrpt   15       1172.632    ± 105.170  ops/s
CounterBenchmark.openTelemetryInc                   thrpt   15       1092.503     ± 48.140  ops/s
CounterBenchmark.openTelemetryIncNoLabels           thrpt   15       1141.207     ± 32.567  ops/s
CounterBenchmark.prometheusAdd                      thrpt   15      30198.130     ± 95.363  ops/s
CounterBenchmark.prometheusInc                      thrpt   15      30930.907     ± 47.266  ops/s
CounterBenchmark.prometheusNoLabelsInc              thrpt   15      31075.000    ± 355.553  ops/s
CounterBenchmark.simpleclientAdd                    thrpt   15       7576.554    ± 122.252  ops/s
CounterBenchmark.simpleclientInc                    thrpt   15       7745.564     ± 57.948  ops/s
CounterBenchmark.simpleclientNoLabelsInc            thrpt   15       7697.281     ± 72.333  ops/s
HistogramBenchmark.openTelemetryClassic             thrpt   15        409.716     ± 24.655  ops/s
HistogramBenchmark.openTelemetryExponential         thrpt   15        356.064     ± 18.020  ops/s
HistogramBenchmark.prometheusClassic                thrpt   15       2620.437    ± 496.409  ops/s
HistogramBenchmark.prometheusNative                 thrpt   15       2231.526    ± 218.594  ops/s
HistogramBenchmark.simpleclient                     thrpt   15       5048.868     ± 22.083  ops/s
TextFormatUtilBenchmark.openMetricsWriteToByteArray  thrpt   15     313437.381   ± 7594.624  ops/s
TextFormatUtilBenchmark.openMetricsWriteToNull      thrpt   15     315343.521   ± 6366.423  ops/s
TextFormatUtilBenchmark.prometheusWriteToByteArray  thrpt   15     330369.233   ± 8278.386  ops/s
TextFormatUtilBenchmark.prometheusWriteToNull       thrpt   15     337209.468   ± 4571.461  ops/s
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
