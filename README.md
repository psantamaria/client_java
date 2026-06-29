# Prometheus Java Client Benchmarks

## Run Information

- **Date:** 2026-06-29T07:57:11Z
- **Commit:** [`4b69f40`](https://github.com/psantamaria/client_java/commit/4b69f40bd4e616d69468ce99dc4323162287a577)
- **JDK:** 25.0.2 (OpenJDK 64-Bit Server VM)
- **Benchmark config:** 3 fork(s), 3 warmup, 5 measurement, 4 threads
- **Hardware:** Intel(R) Xeon(R) Platinum 8370C CPU @ 2.80GHz, 4 cores, 16 GB RAM
- **OS:** Linux 6.17.0-1018-azure

## Results

### CounterBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusInc | 30.71K | ± 1.26K | ops/s | **fastest** |
| prometheusNoLabelsInc | 30.42K | ± 1.03K | ops/s | 1.0x slower |
| codahaleIncNoLabels | 28.73K | ± 726.36 | ops/s | 1.1x slower |
| prometheusAdd | 28.50K | ± 129.49 | ops/s | 1.1x slower |
| simpleclientInc | 6.91K | ± 106.03 | ops/s | 4.4x slower |
| simpleclientAdd | 6.65K | ± 37.63 | ops/s | 4.6x slower |
| simpleclientNoLabelsInc | 6.57K | ± 91.01 | ops/s | 4.7x slower |
| openTelemetryInc | 1.42K | ± 71.89 | ops/s | 22x slower |
| openTelemetryAdd | 1.40K | ± 53.34 | ops/s | 22x slower |
| openTelemetryIncNoLabels | 1.38K | ± 63.49 | ops/s | 22x slower |

### HistogramBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| simpleclient | 4.51K | ± 26.51 | ops/s | **fastest** |
| prometheusClassic | 3.51K | ± 161.56 | ops/s | 1.3x slower |
| prometheusNative | 2.37K | ± 287.51 | ops/s | 1.9x slower |
| openTelemetryClassic | 508.35 | ± 26.86 | ops/s | 8.9x slower |
| openTelemetryExponential | 418.33 | ± 17.76 | ops/s | 11x slower |

### TextFormatUtilBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusWriteToNull | 315.83K | ± 1.65K | ops/s | **fastest** |
| prometheusWriteToByteArray | 310.27K | ± 6.16K | ops/s | 1.0x slower |
| openMetricsWriteToNull | 296.15K | ± 1.19K | ops/s | 1.1x slower |
| openMetricsWriteToByteArray | 294.29K | ± 1.26K | ops/s | 1.1x slower |

### Raw Results

```
Benchmark                                            Mode  Cnt          Score        Error  Units
CounterBenchmark.codahaleIncNoLabels                thrpt   15      28728.446    ± 726.359  ops/s
CounterBenchmark.openTelemetryAdd                   thrpt   15       1400.310     ± 53.343  ops/s
CounterBenchmark.openTelemetryInc                   thrpt   15       1417.782     ± 71.886  ops/s
CounterBenchmark.openTelemetryIncNoLabels           thrpt   15       1375.742     ± 63.490  ops/s
CounterBenchmark.prometheusAdd                      thrpt   15      28501.814    ± 129.490  ops/s
CounterBenchmark.prometheusInc                      thrpt   15      30708.367   ± 1263.028  ops/s
CounterBenchmark.prometheusNoLabelsInc              thrpt   15      30423.384   ± 1029.611  ops/s
CounterBenchmark.simpleclientAdd                    thrpt   15       6648.519     ± 37.628  ops/s
CounterBenchmark.simpleclientInc                    thrpt   15       6914.178    ± 106.031  ops/s
CounterBenchmark.simpleclientNoLabelsInc            thrpt   15       6568.565     ± 91.007  ops/s
HistogramBenchmark.openTelemetryClassic             thrpt   15        508.350     ± 26.858  ops/s
HistogramBenchmark.openTelemetryExponential         thrpt   15        418.331     ± 17.763  ops/s
HistogramBenchmark.prometheusClassic                thrpt   15       3509.157    ± 161.558  ops/s
HistogramBenchmark.prometheusNative                 thrpt   15       2365.294    ± 287.511  ops/s
HistogramBenchmark.simpleclient                     thrpt   15       4508.474     ± 26.511  ops/s
TextFormatUtilBenchmark.openMetricsWriteToByteArray  thrpt   15     294287.553   ± 1260.438  ops/s
TextFormatUtilBenchmark.openMetricsWriteToNull      thrpt   15     296154.961   ± 1193.149  ops/s
TextFormatUtilBenchmark.prometheusWriteToByteArray  thrpt   15     310265.547   ± 6157.442  ops/s
TextFormatUtilBenchmark.prometheusWriteToNull       thrpt   15     315834.690   ± 1653.500  ops/s
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
