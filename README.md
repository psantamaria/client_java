# Prometheus Java Client Benchmarks

## Run Information

- **Date:** 2026-08-25T04:09:13Z
- **Commit:** [`4b69f40`](https://github.com/psantamaria/client_java/commit/4b69f40bd4e616d69468ce99dc4323162287a577)
- **JDK:** 25.0.2 (OpenJDK 64-Bit Server VM)
- **Benchmark config:** 3 fork(s), 3 warmup, 5 measurement, 4 threads
- **Hardware:** AMD EPYC 9V74 80-Core Processor, 4 cores, 16 GB RAM
- **OS:** Linux 6.17.0-1022-azure

## Results

### CounterBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusInc | 60.73K | ± 868.45 | ops/s | **fastest** |
| prometheusNoLabelsInc | 51.95K | ± 39.29 | ops/s | 1.2x slower |
| prometheusAdd | 48.02K | ± 454.66 | ops/s | 1.3x slower |
| codahaleIncNoLabels | 44.70K | ± 752.98 | ops/s | 1.4x slower |
| simpleclientInc | 6.26K | ± 136.79 | ops/s | 9.7x slower |
| simpleclientNoLabelsInc | 6.09K | ± 265.69 | ops/s | 10.0x slower |
| simpleclientAdd | 5.76K | ± 46.72 | ops/s | 11x slower |
| openTelemetryInc | 1.43K | ± 92.40 | ops/s | 42x slower |
| openTelemetryAdd | 1.31K | ± 50.03 | ops/s | 47x slower |
| openTelemetryIncNoLabels | 1.30K | ± 57.17 | ops/s | 47x slower |

### HistogramBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusClassic | 5.86K | ± 3.30K | ops/s | **fastest** |
| simpleclient | 4.54K | ± 63.61 | ops/s | 1.3x slower |
| prometheusNative | 3.02K | ± 191.10 | ops/s | 1.9x slower |
| openTelemetryClassic | 600.68 | ± 13.19 | ops/s | 9.8x slower |
| openTelemetryExponential | 500.35 | ± 14.37 | ops/s | 12x slower |

### TextFormatUtilBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusWriteToNull | 566.56K | ± 3.50K | ops/s | **fastest** |
| prometheusWriteToByteArray | 545.83K | ± 2.31K | ops/s | 1.0x slower |
| openMetricsWriteToNull | 542.78K | ± 2.95K | ops/s | 1.0x slower |
| openMetricsWriteToByteArray | 520.46K | ± 4.17K | ops/s | 1.1x slower |

### Raw Results

```
Benchmark                                            Mode  Cnt          Score        Error  Units
CounterBenchmark.codahaleIncNoLabels                thrpt   15      44697.982    ± 752.979  ops/s
CounterBenchmark.openTelemetryAdd                   thrpt   15       1305.261     ± 50.030  ops/s
CounterBenchmark.openTelemetryInc                   thrpt   15       1431.651     ± 92.399  ops/s
CounterBenchmark.openTelemetryIncNoLabels           thrpt   15       1303.191     ± 57.166  ops/s
CounterBenchmark.prometheusAdd                      thrpt   15      48019.084    ± 454.660  ops/s
CounterBenchmark.prometheusInc                      thrpt   15      60726.945    ± 868.446  ops/s
CounterBenchmark.prometheusNoLabelsInc              thrpt   15      51954.921     ± 39.294  ops/s
CounterBenchmark.simpleclientAdd                    thrpt   15       5761.110     ± 46.718  ops/s
CounterBenchmark.simpleclientInc                    thrpt   15       6258.415    ± 136.790  ops/s
CounterBenchmark.simpleclientNoLabelsInc            thrpt   15       6093.136    ± 265.689  ops/s
HistogramBenchmark.openTelemetryClassic             thrpt   15        600.682     ± 13.192  ops/s
HistogramBenchmark.openTelemetryExponential         thrpt   15        500.354     ± 14.372  ops/s
HistogramBenchmark.prometheusClassic                thrpt   15       5859.001   ± 3296.640  ops/s
HistogramBenchmark.prometheusNative                 thrpt   15       3022.041    ± 191.104  ops/s
HistogramBenchmark.simpleclient                     thrpt   15       4544.749     ± 63.610  ops/s
TextFormatUtilBenchmark.openMetricsWriteToByteArray  thrpt   15     520460.783   ± 4174.234  ops/s
TextFormatUtilBenchmark.openMetricsWriteToNull      thrpt   15     542784.778   ± 2945.407  ops/s
TextFormatUtilBenchmark.prometheusWriteToByteArray  thrpt   15     545834.438   ± 2308.004  ops/s
TextFormatUtilBenchmark.prometheusWriteToNull       thrpt   15     566558.809   ± 3497.768  ops/s
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
