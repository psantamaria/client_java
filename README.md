# Prometheus Java Client Benchmarks

## Run Information

- **Date:** 2026-05-16T06:39:59Z
- **Commit:** [`4b69f40`](https://github.com/psantamaria/client_java/commit/4b69f40bd4e616d69468ce99dc4323162287a577)
- **JDK:** 25.0.2 (OpenJDK 64-Bit Server VM)
- **Benchmark config:** 3 fork(s), 3 warmup, 5 measurement, 4 threads
- **Hardware:** AMD EPYC 7763 64-Core Processor, 4 cores, 16 GB RAM
- **OS:** Linux 6.17.0-1013-azure

## Results

### CounterBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusInc | 65.63K | ± 742.47 | ops/s | **fastest** |
| prometheusNoLabelsInc | 56.83K | ± 485.30 | ops/s | 1.2x slower |
| prometheusAdd | 51.49K | ± 177.47 | ops/s | 1.3x slower |
| codahaleIncNoLabels | 48.47K | ± 2.77K | ops/s | 1.4x slower |
| simpleclientNoLabelsInc | 6.48K | ± 203.71 | ops/s | 10x slower |
| simpleclientInc | 6.45K | ± 343.77 | ops/s | 10x slower |
| simpleclientAdd | 6.12K | ± 222.22 | ops/s | 11x slower |
| openTelemetryAdd | 1.38K | ± 260.19 | ops/s | 48x slower |
| openTelemetryInc | 1.36K | ± 156.24 | ops/s | 48x slower |
| openTelemetryIncNoLabels | 1.20K | ± 8.30 | ops/s | 55x slower |

### HistogramBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusClassic | 4.71K | ± 866.94 | ops/s | **fastest** |
| simpleclient | 4.40K | ± 63.78 | ops/s | 1.1x slower |
| prometheusNative | 2.98K | ± 305.87 | ops/s | 1.6x slower |
| openTelemetryClassic | 696.82 | ± 24.33 | ops/s | 6.8x slower |
| openTelemetryExponential | 551.24 | ± 17.58 | ops/s | 8.5x slower |

### TextFormatUtilBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusWriteToNull | 437.67K | ± 10.28K | ops/s | **fastest** |
| openMetricsWriteToByteArray | 427.09K | ± 8.05K | ops/s | 1.0x slower |
| prometheusWriteToByteArray | 423.58K | ± 8.02K | ops/s | 1.0x slower |
| openMetricsWriteToNull | 404.60K | ± 19.68K | ops/s | 1.1x slower |

### Raw Results

```
Benchmark                                            Mode  Cnt          Score        Error  Units
CounterBenchmark.codahaleIncNoLabels                thrpt   15      48466.465   ± 2768.160  ops/s
CounterBenchmark.openTelemetryAdd                   thrpt   15       1378.544    ± 260.187  ops/s
CounterBenchmark.openTelemetryInc                   thrpt   15       1356.058    ± 156.238  ops/s
CounterBenchmark.openTelemetryIncNoLabels           thrpt   15       1203.815      ± 8.303  ops/s
CounterBenchmark.prometheusAdd                      thrpt   15      51491.267    ± 177.471  ops/s
CounterBenchmark.prometheusInc                      thrpt   15      65630.612    ± 742.468  ops/s
CounterBenchmark.prometheusNoLabelsInc              thrpt   15      56833.544    ± 485.296  ops/s
CounterBenchmark.simpleclientAdd                    thrpt   15       6122.025    ± 222.223  ops/s
CounterBenchmark.simpleclientInc                    thrpt   15       6446.528    ± 343.774  ops/s
CounterBenchmark.simpleclientNoLabelsInc            thrpt   15       6483.130    ± 203.711  ops/s
HistogramBenchmark.openTelemetryClassic             thrpt   15        696.818     ± 24.329  ops/s
HistogramBenchmark.openTelemetryExponential         thrpt   15        551.242     ± 17.584  ops/s
HistogramBenchmark.prometheusClassic                thrpt   15       4708.146    ± 866.944  ops/s
HistogramBenchmark.prometheusNative                 thrpt   15       2979.621    ± 305.870  ops/s
HistogramBenchmark.simpleclient                     thrpt   15       4396.687     ± 63.781  ops/s
TextFormatUtilBenchmark.openMetricsWriteToByteArray  thrpt   15     427090.377   ± 8053.682  ops/s
TextFormatUtilBenchmark.openMetricsWriteToNull      thrpt   15     404598.711  ± 19677.123  ops/s
TextFormatUtilBenchmark.prometheusWriteToByteArray  thrpt   15     423575.501   ± 8023.667  ops/s
TextFormatUtilBenchmark.prometheusWriteToNull       thrpt   15     437671.007  ± 10283.361  ops/s
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
