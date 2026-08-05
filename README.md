# Prometheus Java Client Benchmarks

## Run Information

- **Date:** 2026-08-05T06:26:50Z
- **Commit:** [`4b69f40`](https://github.com/psantamaria/client_java/commit/4b69f40bd4e616d69468ce99dc4323162287a577)
- **JDK:** 25.0.2 (OpenJDK 64-Bit Server VM)
- **Benchmark config:** 3 fork(s), 3 warmup, 5 measurement, 4 threads
- **Hardware:** AMD EPYC 7763 64-Core Processor, 4 cores, 16 GB RAM
- **OS:** Linux 6.17.0-1020-azure

## Results

### CounterBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusInc | 64.89K | ± 1.31K | ops/s | **fastest** |
| prometheusNoLabelsInc | 56.45K | ± 1.15K | ops/s | 1.1x slower |
| prometheusAdd | 51.12K | ± 686.38 | ops/s | 1.3x slower |
| codahaleIncNoLabels | 47.22K | ± 111.76 | ops/s | 1.4x slower |
| simpleclientInc | 6.59K | ± 167.69 | ops/s | 9.8x slower |
| simpleclientNoLabelsInc | 6.46K | ± 189.20 | ops/s | 10x slower |
| simpleclientAdd | 5.98K | ± 204.83 | ops/s | 11x slower |
| openTelemetryAdd | 1.64K | ± 156.50 | ops/s | 40x slower |
| openTelemetryInc | 1.26K | ± 16.77 | ops/s | 52x slower |
| openTelemetryIncNoLabels | 1.14K | ± 79.50 | ops/s | 57x slower |

### HistogramBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusClassic | 6.55K | ± 1.31K | ops/s | **fastest** |
| simpleclient | 4.44K | ± 44.82 | ops/s | 1.5x slower |
| prometheusNative | 2.50K | ± 45.21 | ops/s | 2.6x slower |
| openTelemetryClassic | 665.19 | ± 17.22 | ops/s | 9.9x slower |
| openTelemetryExponential | 575.40 | ± 33.10 | ops/s | 11x slower |

### TextFormatUtilBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusWriteToNull | 472.79K | ± 5.06K | ops/s | **fastest** |
| prometheusWriteToByteArray | 472.27K | ± 6.30K | ops/s | 1.0x slower |
| openMetricsWriteToNull | 467.79K | ± 5.77K | ops/s | 1.0x slower |
| openMetricsWriteToByteArray | 457.52K | ± 6.10K | ops/s | 1.0x slower |

### Raw Results

```
Benchmark                                            Mode  Cnt          Score        Error  Units
CounterBenchmark.codahaleIncNoLabels                thrpt   15      47219.455    ± 111.761  ops/s
CounterBenchmark.openTelemetryAdd                   thrpt   15       1638.131    ± 156.502  ops/s
CounterBenchmark.openTelemetryInc                   thrpt   15       1259.167     ± 16.768  ops/s
CounterBenchmark.openTelemetryIncNoLabels           thrpt   15       1140.499     ± 79.500  ops/s
CounterBenchmark.prometheusAdd                      thrpt   15      51121.961    ± 686.377  ops/s
CounterBenchmark.prometheusInc                      thrpt   15      64888.145   ± 1313.078  ops/s
CounterBenchmark.prometheusNoLabelsInc              thrpt   15      56452.443   ± 1150.769  ops/s
CounterBenchmark.simpleclientAdd                    thrpt   15       5981.850    ± 204.825  ops/s
CounterBenchmark.simpleclientInc                    thrpt   15       6588.171    ± 167.689  ops/s
CounterBenchmark.simpleclientNoLabelsInc            thrpt   15       6462.391    ± 189.196  ops/s
HistogramBenchmark.openTelemetryClassic             thrpt   15        665.187     ± 17.224  ops/s
HistogramBenchmark.openTelemetryExponential         thrpt   15        575.401     ± 33.097  ops/s
HistogramBenchmark.prometheusClassic                thrpt   15       6553.697   ± 1314.584  ops/s
HistogramBenchmark.prometheusNative                 thrpt   15       2498.163     ± 45.208  ops/s
HistogramBenchmark.simpleclient                     thrpt   15       4436.552     ± 44.816  ops/s
TextFormatUtilBenchmark.openMetricsWriteToByteArray  thrpt   15     457523.231   ± 6102.193  ops/s
TextFormatUtilBenchmark.openMetricsWriteToNull      thrpt   15     467791.583   ± 5773.302  ops/s
TextFormatUtilBenchmark.prometheusWriteToByteArray  thrpt   15     472271.516   ± 6302.354  ops/s
TextFormatUtilBenchmark.prometheusWriteToNull       thrpt   15     472793.922   ± 5060.130  ops/s
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
