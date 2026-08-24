# Prometheus Java Client Benchmarks

## Run Information

- **Date:** 2026-08-24T04:13:42Z
- **Commit:** [`4b69f40`](https://github.com/psantamaria/client_java/commit/4b69f40bd4e616d69468ce99dc4323162287a577)
- **JDK:** 25.0.2 (OpenJDK 64-Bit Server VM)
- **Benchmark config:** 3 fork(s), 3 warmup, 5 measurement, 4 threads
- **Hardware:** AMD EPYC 9V74 80-Core Processor, 4 cores, 16 GB RAM
- **OS:** Linux 6.17.0-1022-azure

## Results

### CounterBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusInc | 58.50K | ± 2.90K | ops/s | **fastest** |
| prometheusNoLabelsInc | 52.67K | ± 68.35 | ops/s | 1.1x slower |
| prometheusAdd | 48.31K | ± 342.22 | ops/s | 1.2x slower |
| codahaleIncNoLabels | 43.74K | ± 356.14 | ops/s | 1.3x slower |
| simpleclientInc | 6.15K | ± 145.47 | ops/s | 9.5x slower |
| simpleclientAdd | 6.06K | ± 221.26 | ops/s | 9.7x slower |
| simpleclientNoLabelsInc | 5.82K | ± 94.71 | ops/s | 10x slower |
| openTelemetryAdd | 1.42K | ± 94.11 | ops/s | 41x slower |
| openTelemetryIncNoLabels | 1.40K | ± 91.52 | ops/s | 42x slower |
| openTelemetryInc | 1.36K | ± 84.54 | ops/s | 43x slower |

### HistogramBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusClassic | 5.04K | ± 1.21K | ops/s | **fastest** |
| simpleclient | 4.22K | ± 24.01 | ops/s | 1.2x slower |
| prometheusNative | 2.95K | ± 246.41 | ops/s | 1.7x slower |
| openTelemetryClassic | 632.84 | ± 10.45 | ops/s | 8.0x slower |
| openTelemetryExponential | 527.02 | ± 33.81 | ops/s | 9.6x slower |

### TextFormatUtilBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusWriteToNull | 559.36K | ± 2.71K | ops/s | **fastest** |
| prometheusWriteToByteArray | 543.95K | ± 5.86K | ops/s | 1.0x slower |
| openMetricsWriteToNull | 536.72K | ± 2.76K | ops/s | 1.0x slower |
| openMetricsWriteToByteArray | 522.41K | ± 6.50K | ops/s | 1.1x slower |

### Raw Results

```
Benchmark                                            Mode  Cnt          Score        Error  Units
CounterBenchmark.codahaleIncNoLabels                thrpt   15      43739.688    ± 356.138  ops/s
CounterBenchmark.openTelemetryAdd                   thrpt   15       1422.074     ± 94.111  ops/s
CounterBenchmark.openTelemetryInc                   thrpt   15       1355.547     ± 84.544  ops/s
CounterBenchmark.openTelemetryIncNoLabels           thrpt   15       1395.193     ± 91.523  ops/s
CounterBenchmark.prometheusAdd                      thrpt   15      48305.606    ± 342.215  ops/s
CounterBenchmark.prometheusInc                      thrpt   15      58498.134   ± 2898.447  ops/s
CounterBenchmark.prometheusNoLabelsInc              thrpt   15      52667.775     ± 68.353  ops/s
CounterBenchmark.simpleclientAdd                    thrpt   15       6055.781    ± 221.257  ops/s
CounterBenchmark.simpleclientInc                    thrpt   15       6148.370    ± 145.470  ops/s
CounterBenchmark.simpleclientNoLabelsInc            thrpt   15       5820.741     ± 94.710  ops/s
HistogramBenchmark.openTelemetryClassic             thrpt   15        632.841     ± 10.446  ops/s
HistogramBenchmark.openTelemetryExponential         thrpt   15        527.020     ± 33.815  ops/s
HistogramBenchmark.prometheusClassic                thrpt   15       5044.916   ± 1208.460  ops/s
HistogramBenchmark.prometheusNative                 thrpt   15       2951.609    ± 246.408  ops/s
HistogramBenchmark.simpleclient                     thrpt   15       4221.898     ± 24.005  ops/s
TextFormatUtilBenchmark.openMetricsWriteToByteArray  thrpt   15     522406.211   ± 6500.674  ops/s
TextFormatUtilBenchmark.openMetricsWriteToNull      thrpt   15     536724.769   ± 2764.163  ops/s
TextFormatUtilBenchmark.prometheusWriteToByteArray  thrpt   15     543948.414   ± 5862.549  ops/s
TextFormatUtilBenchmark.prometheusWriteToNull       thrpt   15     559362.519   ± 2708.950  ops/s
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
