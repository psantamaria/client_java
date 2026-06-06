# Prometheus Java Client Benchmarks

## Run Information

- **Date:** 2026-06-06T07:07:01Z
- **Commit:** [`4b69f40`](https://github.com/psantamaria/client_java/commit/4b69f40bd4e616d69468ce99dc4323162287a577)
- **JDK:** 25.0.2 (OpenJDK 64-Bit Server VM)
- **Benchmark config:** 3 fork(s), 3 warmup, 5 measurement, 4 threads
- **Hardware:** Intel(R) Xeon(R) Platinum 8370C CPU @ 2.80GHz, 4 cores, 16 GB RAM
- **OS:** Linux 6.17.0-1015-azure

## Results

### CounterBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusInc | 31.51K | ± 22.88 | ops/s | **fastest** |
| prometheusNoLabelsInc | 31.27K | ± 232.81 | ops/s | 1.0x slower |
| codahaleIncNoLabels | 29.03K | ± 305.47 | ops/s | 1.1x slower |
| prometheusAdd | 28.39K | ± 52.94 | ops/s | 1.1x slower |
| simpleclientInc | 6.84K | ± 66.34 | ops/s | 4.6x slower |
| simpleclientNoLabelsInc | 6.60K | ± 222.95 | ops/s | 4.8x slower |
| simpleclientAdd | 6.07K | ± 473.41 | ops/s | 5.2x slower |
| openTelemetryIncNoLabels | 1.47K | ± 27.12 | ops/s | 21x slower |
| openTelemetryInc | 1.41K | ± 36.84 | ops/s | 22x slower |
| openTelemetryAdd | 1.39K | ± 110.92 | ops/s | 23x slower |

### HistogramBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| simpleclient | 4.45K | ± 33.95 | ops/s | **fastest** |
| prometheusClassic | 3.37K | ± 573.26 | ops/s | 1.3x slower |
| prometheusNative | 2.00K | ± 93.32 | ops/s | 2.2x slower |
| openTelemetryClassic | 532.76 | ± 19.14 | ops/s | 8.3x slower |
| openTelemetryExponential | 451.10 | ± 30.43 | ops/s | 9.9x slower |

### TextFormatUtilBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusWriteToNull | 320.80K | ± 1.61K | ops/s | **fastest** |
| prometheusWriteToByteArray | 317.23K | ± 1.54K | ops/s | 1.0x slower |
| openMetricsWriteToNull | 300.82K | ± 1.04K | ops/s | 1.1x slower |
| openMetricsWriteToByteArray | 298.97K | ± 2.05K | ops/s | 1.1x slower |

### Raw Results

```
Benchmark                                            Mode  Cnt          Score        Error  Units
CounterBenchmark.codahaleIncNoLabels                thrpt   15      29028.851    ± 305.471  ops/s
CounterBenchmark.openTelemetryAdd                   thrpt   15       1388.773    ± 110.919  ops/s
CounterBenchmark.openTelemetryInc                   thrpt   15       1410.114     ± 36.842  ops/s
CounterBenchmark.openTelemetryIncNoLabels           thrpt   15       1470.685     ± 27.121  ops/s
CounterBenchmark.prometheusAdd                      thrpt   15      28390.613     ± 52.945  ops/s
CounterBenchmark.prometheusInc                      thrpt   15      31509.954     ± 22.882  ops/s
CounterBenchmark.prometheusNoLabelsInc              thrpt   15      31273.928    ± 232.810  ops/s
CounterBenchmark.simpleclientAdd                    thrpt   15       6069.147    ± 473.407  ops/s
CounterBenchmark.simpleclientInc                    thrpt   15       6837.220     ± 66.340  ops/s
CounterBenchmark.simpleclientNoLabelsInc            thrpt   15       6604.729    ± 222.951  ops/s
HistogramBenchmark.openTelemetryClassic             thrpt   15        532.759     ± 19.142  ops/s
HistogramBenchmark.openTelemetryExponential         thrpt   15        451.102     ± 30.434  ops/s
HistogramBenchmark.prometheusClassic                thrpt   15       3368.672    ± 573.255  ops/s
HistogramBenchmark.prometheusNative                 thrpt   15       1997.460     ± 93.317  ops/s
HistogramBenchmark.simpleclient                     thrpt   15       4447.209     ± 33.950  ops/s
TextFormatUtilBenchmark.openMetricsWriteToByteArray  thrpt   15     298972.191   ± 2054.261  ops/s
TextFormatUtilBenchmark.openMetricsWriteToNull      thrpt   15     300816.589   ± 1044.250  ops/s
TextFormatUtilBenchmark.prometheusWriteToByteArray  thrpt   15     317230.410   ± 1542.723  ops/s
TextFormatUtilBenchmark.prometheusWriteToNull       thrpt   15     320797.489   ± 1612.370  ops/s
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
