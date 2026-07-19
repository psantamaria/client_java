# Prometheus Java Client Benchmarks

## Run Information

- **Date:** 2026-07-19T06:33:50Z
- **Commit:** [`4b69f40`](https://github.com/psantamaria/client_java/commit/4b69f40bd4e616d69468ce99dc4323162287a577)
- **JDK:** 25.0.2 (OpenJDK 64-Bit Server VM)
- **Benchmark config:** 3 fork(s), 3 warmup, 5 measurement, 4 threads
- **Hardware:** AMD EPYC 7763 64-Core Processor, 4 cores, 16 GB RAM
- **OS:** Linux 6.17.0-1020-azure

## Results

### CounterBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusInc | 65.24K | ± 1.69K | ops/s | **fastest** |
| prometheusNoLabelsInc | 56.33K | ± 220.19 | ops/s | 1.2x slower |
| prometheusAdd | 50.61K | ± 598.52 | ops/s | 1.3x slower |
| codahaleIncNoLabels | 49.24K | ± 1.09K | ops/s | 1.3x slower |
| simpleclientInc | 6.53K | ± 186.88 | ops/s | 10.0x slower |
| simpleclientNoLabelsInc | 6.48K | ± 184.66 | ops/s | 10x slower |
| simpleclientAdd | 6.47K | ± 22.11 | ops/s | 10x slower |
| openTelemetryInc | 1.37K | ± 188.34 | ops/s | 48x slower |
| openTelemetryAdd | 1.32K | ± 31.03 | ops/s | 49x slower |
| openTelemetryIncNoLabels | 1.23K | ± 32.03 | ops/s | 53x slower |

### HistogramBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusClassic | 7.65K | ± 2.11K | ops/s | **fastest** |
| simpleclient | 4.47K | ± 43.08 | ops/s | 1.7x slower |
| prometheusNative | 2.86K | ± 242.53 | ops/s | 2.7x slower |
| openTelemetryClassic | 659.18 | ± 52.25 | ops/s | 12x slower |
| openTelemetryExponential | 583.94 | ± 40.34 | ops/s | 13x slower |

### TextFormatUtilBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusWriteToNull | 480.16K | ± 6.91K | ops/s | **fastest** |
| prometheusWriteToByteArray | 477.21K | ± 3.94K | ops/s | 1.0x slower |
| openMetricsWriteToNull | 464.16K | ± 6.69K | ops/s | 1.0x slower |
| openMetricsWriteToByteArray | 458.44K | ± 2.63K | ops/s | 1.0x slower |

### Raw Results

```
Benchmark                                            Mode  Cnt          Score        Error  Units
CounterBenchmark.codahaleIncNoLabels                thrpt   15      49239.612   ± 1086.748  ops/s
CounterBenchmark.openTelemetryAdd                   thrpt   15       1324.074     ± 31.027  ops/s
CounterBenchmark.openTelemetryInc                   thrpt   15       1368.174    ± 188.339  ops/s
CounterBenchmark.openTelemetryIncNoLabels           thrpt   15       1227.580     ± 32.029  ops/s
CounterBenchmark.prometheusAdd                      thrpt   15      50611.297    ± 598.524  ops/s
CounterBenchmark.prometheusInc                      thrpt   15      65242.084   ± 1692.673  ops/s
CounterBenchmark.prometheusNoLabelsInc              thrpt   15      56326.130    ± 220.193  ops/s
CounterBenchmark.simpleclientAdd                    thrpt   15       6467.445     ± 22.107  ops/s
CounterBenchmark.simpleclientInc                    thrpt   15       6533.798    ± 186.882  ops/s
CounterBenchmark.simpleclientNoLabelsInc            thrpt   15       6476.139    ± 184.663  ops/s
HistogramBenchmark.openTelemetryClassic             thrpt   15        659.177     ± 52.253  ops/s
HistogramBenchmark.openTelemetryExponential         thrpt   15        583.937     ± 40.344  ops/s
HistogramBenchmark.prometheusClassic                thrpt   15       7652.322   ± 2112.780  ops/s
HistogramBenchmark.prometheusNative                 thrpt   15       2861.427    ± 242.533  ops/s
HistogramBenchmark.simpleclient                     thrpt   15       4474.020     ± 43.078  ops/s
TextFormatUtilBenchmark.openMetricsWriteToByteArray  thrpt   15     458444.628   ± 2627.980  ops/s
TextFormatUtilBenchmark.openMetricsWriteToNull      thrpt   15     464162.268   ± 6689.899  ops/s
TextFormatUtilBenchmark.prometheusWriteToByteArray  thrpt   15     477212.163   ± 3936.684  ops/s
TextFormatUtilBenchmark.prometheusWriteToNull       thrpt   15     480164.548   ± 6914.547  ops/s
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
