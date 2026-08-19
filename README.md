# Prometheus Java Client Benchmarks

## Run Information

- **Date:** 2026-08-19T04:08:25Z
- **Commit:** [`4b69f40`](https://github.com/psantamaria/client_java/commit/4b69f40bd4e616d69468ce99dc4323162287a577)
- **JDK:** 25.0.2 (OpenJDK 64-Bit Server VM)
- **Benchmark config:** 3 fork(s), 3 warmup, 5 measurement, 4 threads
- **Hardware:** AMD EPYC 7763 64-Core Processor, 4 cores, 16 GB RAM
- **OS:** Linux 6.17.0-1022-azure

## Results

### CounterBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusInc | 65.59K | ± 1.67K | ops/s | **fastest** |
| prometheusNoLabelsInc | 57.15K | ± 159.25 | ops/s | 1.1x slower |
| prometheusAdd | 51.44K | ± 151.56 | ops/s | 1.3x slower |
| codahaleIncNoLabels | 49.31K | ± 1.79K | ops/s | 1.3x slower |
| simpleclientInc | 6.70K | ± 7.98 | ops/s | 9.8x slower |
| simpleclientNoLabelsInc | 6.44K | ± 150.00 | ops/s | 10x slower |
| simpleclientAdd | 6.31K | ± 166.08 | ops/s | 10x slower |
| openTelemetryInc | 1.32K | ± 165.46 | ops/s | 50x slower |
| openTelemetryAdd | 1.23K | ± 16.96 | ops/s | 53x slower |
| openTelemetryIncNoLabels | 1.23K | ± 41.27 | ops/s | 53x slower |

### HistogramBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusClassic | 5.39K | ± 1.37K | ops/s | **fastest** |
| simpleclient | 4.48K | ± 34.62 | ops/s | 1.2x slower |
| prometheusNative | 3.22K | ± 83.88 | ops/s | 1.7x slower |
| openTelemetryClassic | 683.92 | ± 7.11 | ops/s | 7.9x slower |
| openTelemetryExponential | 552.37 | ± 36.89 | ops/s | 9.8x slower |

### TextFormatUtilBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusWriteToNull | 486.77K | ± 5.01K | ops/s | **fastest** |
| prometheusWriteToByteArray | 485.58K | ± 1.85K | ops/s | 1.0x slower |
| openMetricsWriteToNull | 472.93K | ± 4.97K | ops/s | 1.0x slower |
| openMetricsWriteToByteArray | 465.23K | ± 1.81K | ops/s | 1.0x slower |

### Raw Results

```
Benchmark                                            Mode  Cnt          Score        Error  Units
CounterBenchmark.codahaleIncNoLabels                thrpt   15      49306.262   ± 1786.840  ops/s
CounterBenchmark.openTelemetryAdd                   thrpt   15       1230.415     ± 16.960  ops/s
CounterBenchmark.openTelemetryInc                   thrpt   15       1323.005    ± 165.461  ops/s
CounterBenchmark.openTelemetryIncNoLabels           thrpt   15       1226.349     ± 41.266  ops/s
CounterBenchmark.prometheusAdd                      thrpt   15      51440.717    ± 151.558  ops/s
CounterBenchmark.prometheusInc                      thrpt   15      65591.481   ± 1666.746  ops/s
CounterBenchmark.prometheusNoLabelsInc              thrpt   15      57150.808    ± 159.254  ops/s
CounterBenchmark.simpleclientAdd                    thrpt   15       6311.198    ± 166.082  ops/s
CounterBenchmark.simpleclientInc                    thrpt   15       6698.013      ± 7.979  ops/s
CounterBenchmark.simpleclientNoLabelsInc            thrpt   15       6437.036    ± 150.001  ops/s
HistogramBenchmark.openTelemetryClassic             thrpt   15        683.924      ± 7.108  ops/s
HistogramBenchmark.openTelemetryExponential         thrpt   15        552.373     ± 36.889  ops/s
HistogramBenchmark.prometheusClassic                thrpt   15       5385.642   ± 1374.864  ops/s
HistogramBenchmark.prometheusNative                 thrpt   15       3220.014     ± 83.880  ops/s
HistogramBenchmark.simpleclient                     thrpt   15       4480.280     ± 34.622  ops/s
TextFormatUtilBenchmark.openMetricsWriteToByteArray  thrpt   15     465225.541   ± 1808.554  ops/s
TextFormatUtilBenchmark.openMetricsWriteToNull      thrpt   15     472928.272   ± 4965.411  ops/s
TextFormatUtilBenchmark.prometheusWriteToByteArray  thrpt   15     485582.619   ± 1847.431  ops/s
TextFormatUtilBenchmark.prometheusWriteToNull       thrpt   15     486767.437   ± 5006.450  ops/s
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
