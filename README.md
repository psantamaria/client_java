# Prometheus Java Client Benchmarks

## Run Information

- **Date:** 2026-09-04T08:07:01Z
- **Commit:** [`4b69f40`](https://github.com/psantamaria/client_java/commit/4b69f40bd4e616d69468ce99dc4323162287a577)
- **JDK:** 25.0.2 (OpenJDK 64-Bit Server VM)
- **Benchmark config:** 3 fork(s), 3 warmup, 5 measurement, 4 threads
- **Hardware:** INTEL(R) XEON(R) PLATINUM 8573C, 4 cores, 16 GB RAM
- **OS:** Linux 6.17.0-1022-azure

## Results

### CounterBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusAdd | 28.31K | ± 771.17 | ops/s | **fastest** |
| prometheusNoLabelsInc | 27.85K | ± 420.38 | ops/s | 1.0x slower |
| prometheusInc | 27.64K | ± 847.32 | ops/s | 1.0x slower |
| codahaleIncNoLabels | 27.17K | ± 1.32K | ops/s | 1.0x slower |
| simpleclientInc | 6.98K | ± 148.50 | ops/s | 4.1x slower |
| simpleclientNoLabelsInc | 6.91K | ± 87.05 | ops/s | 4.1x slower |
| simpleclientAdd | 6.69K | ± 253.42 | ops/s | 4.2x slower |
| openTelemetryIncNoLabels | 1.19K | ± 50.79 | ops/s | 24x slower |
| openTelemetryAdd | 1.13K | ± 113.41 | ops/s | 25x slower |
| openTelemetryInc | 1.10K | ± 148.61 | ops/s | 26x slower |

### HistogramBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| simpleclient | 4.47K | ± 107.66 | ops/s | **fastest** |
| prometheusClassic | 2.62K | ± 408.25 | ops/s | 1.7x slower |
| prometheusNative | 2.08K | ± 243.61 | ops/s | 2.1x slower |
| openTelemetryClassic | 386.04 | ± 18.45 | ops/s | 12x slower |
| openTelemetryExponential | 326.98 | ± 13.86 | ops/s | 14x slower |

### TextFormatUtilBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusWriteToNull | 291.01K | ± 4.36K | ops/s | **fastest** |
| prometheusWriteToByteArray | 286.96K | ± 2.58K | ops/s | 1.0x slower |
| openMetricsWriteToByteArray | 276.47K | ± 2.72K | ops/s | 1.1x slower |
| openMetricsWriteToNull | 273.41K | ± 3.31K | ops/s | 1.1x slower |

### Raw Results

```
Benchmark                                            Mode  Cnt          Score        Error  Units
CounterBenchmark.codahaleIncNoLabels                thrpt   15      27172.544   ± 1316.576  ops/s
CounterBenchmark.openTelemetryAdd                   thrpt   15       1129.884    ± 113.414  ops/s
CounterBenchmark.openTelemetryInc                   thrpt   15       1101.065    ± 148.608  ops/s
CounterBenchmark.openTelemetryIncNoLabels           thrpt   15       1192.433     ± 50.786  ops/s
CounterBenchmark.prometheusAdd                      thrpt   15      28313.746    ± 771.169  ops/s
CounterBenchmark.prometheusInc                      thrpt   15      27641.355    ± 847.318  ops/s
CounterBenchmark.prometheusNoLabelsInc              thrpt   15      27851.790    ± 420.381  ops/s
CounterBenchmark.simpleclientAdd                    thrpt   15       6689.544    ± 253.418  ops/s
CounterBenchmark.simpleclientInc                    thrpt   15       6978.221    ± 148.498  ops/s
CounterBenchmark.simpleclientNoLabelsInc            thrpt   15       6912.650     ± 87.049  ops/s
HistogramBenchmark.openTelemetryClassic             thrpt   15        386.040     ± 18.450  ops/s
HistogramBenchmark.openTelemetryExponential         thrpt   15        326.979     ± 13.862  ops/s
HistogramBenchmark.prometheusClassic                thrpt   15       2624.659    ± 408.249  ops/s
HistogramBenchmark.prometheusNative                 thrpt   15       2083.820    ± 243.610  ops/s
HistogramBenchmark.simpleclient                     thrpt   15       4468.345    ± 107.661  ops/s
TextFormatUtilBenchmark.openMetricsWriteToByteArray  thrpt   15     276468.133   ± 2724.362  ops/s
TextFormatUtilBenchmark.openMetricsWriteToNull      thrpt   15     273407.549   ± 3308.607  ops/s
TextFormatUtilBenchmark.prometheusWriteToByteArray  thrpt   15     286959.152   ± 2579.691  ops/s
TextFormatUtilBenchmark.prometheusWriteToNull       thrpt   15     291013.292   ± 4363.074  ops/s
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
