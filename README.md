# Prometheus Java Client Benchmarks

## Run Information

- **Date:** 2026-05-01T06:55:14Z
- **Commit:** [`4b69f40`](https://github.com/psantamaria/client_java/commit/4b69f40bd4e616d69468ce99dc4323162287a577)
- **JDK:** 25.0.2 (OpenJDK 64-Bit Server VM)
- **Benchmark config:** 3 fork(s), 3 warmup, 5 measurement, 4 threads
- **Hardware:** Intel(R) Xeon(R) Platinum 8370C CPU @ 2.80GHz, 4 cores, 16 GB RAM
- **OS:** Linux 6.17.0-1010-azure

## Results

### CounterBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusInc | 31.49K | ± 21.69 | ops/s | **fastest** |
| prometheusNoLabelsInc | 31.05K | ± 134.03 | ops/s | 1.0x slower |
| codahaleIncNoLabels | 29.97K | ± 1.33K | ops/s | 1.1x slower |
| prometheusAdd | 28.41K | ± 33.33 | ops/s | 1.1x slower |
| simpleclientInc | 6.89K | ± 90.87 | ops/s | 4.6x slower |
| simpleclientNoLabelsInc | 6.59K | ± 94.24 | ops/s | 4.8x slower |
| simpleclientAdd | 6.45K | ± 249.84 | ops/s | 4.9x slower |
| openTelemetryIncNoLabels | 1.44K | ± 154.87 | ops/s | 22x slower |
| openTelemetryInc | 1.36K | ± 67.98 | ops/s | 23x slower |
| openTelemetryAdd | 1.28K | ± 122.57 | ops/s | 25x slower |

### HistogramBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| simpleclient | 4.40K | ± 130.56 | ops/s | **fastest** |
| prometheusClassic | 3.68K | ± 1.06K | ops/s | 1.2x slower |
| prometheusNative | 2.06K | ± 212.97 | ops/s | 2.1x slower |
| openTelemetryClassic | 527.65 | ± 11.52 | ops/s | 8.3x slower |
| openTelemetryExponential | 419.38 | ± 11.89 | ops/s | 10x slower |

### TextFormatUtilBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusWriteToNull | 315.83K | ± 2.84K | ops/s | **fastest** |
| prometheusWriteToByteArray | 311.84K | ± 1.81K | ops/s | 1.0x slower |
| openMetricsWriteToNull | 295.20K | ± 2.86K | ops/s | 1.1x slower |
| openMetricsWriteToByteArray | 292.49K | ± 1.55K | ops/s | 1.1x slower |

### Raw Results

```
Benchmark                                            Mode  Cnt          Score        Error  Units
CounterBenchmark.codahaleIncNoLabels                thrpt   15      29972.795   ± 1332.422  ops/s
CounterBenchmark.openTelemetryAdd                   thrpt   15       1277.993    ± 122.565  ops/s
CounterBenchmark.openTelemetryInc                   thrpt   15       1357.271     ± 67.979  ops/s
CounterBenchmark.openTelemetryIncNoLabels           thrpt   15       1439.591    ± 154.869  ops/s
CounterBenchmark.prometheusAdd                      thrpt   15      28414.230     ± 33.335  ops/s
CounterBenchmark.prometheusInc                      thrpt   15      31487.542     ± 21.686  ops/s
CounterBenchmark.prometheusNoLabelsInc              thrpt   15      31054.310    ± 134.029  ops/s
CounterBenchmark.simpleclientAdd                    thrpt   15       6447.931    ± 249.839  ops/s
CounterBenchmark.simpleclientInc                    thrpt   15       6886.897     ± 90.874  ops/s
CounterBenchmark.simpleclientNoLabelsInc            thrpt   15       6591.060     ± 94.241  ops/s
HistogramBenchmark.openTelemetryClassic             thrpt   15        527.654     ± 11.519  ops/s
HistogramBenchmark.openTelemetryExponential         thrpt   15        419.381     ± 11.894  ops/s
HistogramBenchmark.prometheusClassic                thrpt   15       3681.033   ± 1056.306  ops/s
HistogramBenchmark.prometheusNative                 thrpt   15       2061.508    ± 212.966  ops/s
HistogramBenchmark.simpleclient                     thrpt   15       4400.863    ± 130.564  ops/s
TextFormatUtilBenchmark.openMetricsWriteToByteArray  thrpt   15     292492.402   ± 1553.067  ops/s
TextFormatUtilBenchmark.openMetricsWriteToNull      thrpt   15     295204.664   ± 2859.721  ops/s
TextFormatUtilBenchmark.prometheusWriteToByteArray  thrpt   15     311841.315   ± 1809.179  ops/s
TextFormatUtilBenchmark.prometheusWriteToNull       thrpt   15     315833.523   ± 2841.999  ops/s
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
