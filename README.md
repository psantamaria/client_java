# Prometheus Java Client Benchmarks

## Run Information

- **Date:** 2026-08-01T06:38:47Z
- **Commit:** [`4b69f40`](https://github.com/psantamaria/client_java/commit/4b69f40bd4e616d69468ce99dc4323162287a577)
- **JDK:** 25.0.2 (OpenJDK 64-Bit Server VM)
- **Benchmark config:** 3 fork(s), 3 warmup, 5 measurement, 4 threads
- **Hardware:** AMD EPYC 7763 64-Core Processor, 4 cores, 16 GB RAM
- **OS:** Linux 6.17.0-1020-azure

## Results

### CounterBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusInc | 65.73K | ± 1.65K | ops/s | **fastest** |
| prometheusNoLabelsInc | 56.25K | ± 976.59 | ops/s | 1.2x slower |
| prometheusAdd | 50.93K | ± 286.99 | ops/s | 1.3x slower |
| codahaleIncNoLabels | 48.67K | ± 1.94K | ops/s | 1.4x slower |
| simpleclientInc | 6.63K | ± 54.04 | ops/s | 9.9x slower |
| simpleclientNoLabelsInc | 6.49K | ± 215.18 | ops/s | 10x slower |
| simpleclientAdd | 6.33K | ± 203.47 | ops/s | 10x slower |
| openTelemetryInc | 1.36K | ± 148.65 | ops/s | 48x slower |
| openTelemetryIncNoLabels | 1.33K | ± 179.46 | ops/s | 49x slower |
| openTelemetryAdd | 1.27K | ± 29.98 | ops/s | 52x slower |

### HistogramBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusClassic | 5.34K | ± 1.48K | ops/s | **fastest** |
| simpleclient | 4.37K | ± 22.00 | ops/s | 1.2x slower |
| prometheusNative | 3.17K | ± 51.14 | ops/s | 1.7x slower |
| openTelemetryClassic | 683.09 | ± 8.82 | ops/s | 7.8x slower |
| openTelemetryExponential | 547.01 | ± 47.86 | ops/s | 9.8x slower |

### TextFormatUtilBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusWriteToNull | 481.46K | ± 6.34K | ops/s | **fastest** |
| prometheusWriteToByteArray | 467.83K | ± 7.24K | ops/s | 1.0x slower |
| openMetricsWriteToNull | 466.94K | ± 9.26K | ops/s | 1.0x slower |
| openMetricsWriteToByteArray | 457.92K | ± 8.86K | ops/s | 1.1x slower |

### Raw Results

```
Benchmark                                            Mode  Cnt          Score        Error  Units
CounterBenchmark.codahaleIncNoLabels                thrpt   15      48672.408   ± 1939.972  ops/s
CounterBenchmark.openTelemetryAdd                   thrpt   15       1269.312     ± 29.977  ops/s
CounterBenchmark.openTelemetryInc                   thrpt   15       1355.370    ± 148.654  ops/s
CounterBenchmark.openTelemetryIncNoLabels           thrpt   15       1328.626    ± 179.462  ops/s
CounterBenchmark.prometheusAdd                      thrpt   15      50927.610    ± 286.993  ops/s
CounterBenchmark.prometheusInc                      thrpt   15      65734.578   ± 1650.580  ops/s
CounterBenchmark.prometheusNoLabelsInc              thrpt   15      56245.646    ± 976.592  ops/s
CounterBenchmark.simpleclientAdd                    thrpt   15       6331.525    ± 203.466  ops/s
CounterBenchmark.simpleclientInc                    thrpt   15       6629.772     ± 54.040  ops/s
CounterBenchmark.simpleclientNoLabelsInc            thrpt   15       6486.454    ± 215.185  ops/s
HistogramBenchmark.openTelemetryClassic             thrpt   15        683.086      ± 8.822  ops/s
HistogramBenchmark.openTelemetryExponential         thrpt   15        547.011     ± 47.857  ops/s
HistogramBenchmark.prometheusClassic                thrpt   15       5340.671   ± 1482.477  ops/s
HistogramBenchmark.prometheusNative                 thrpt   15       3174.874     ± 51.136  ops/s
HistogramBenchmark.simpleclient                     thrpt   15       4372.694     ± 22.001  ops/s
TextFormatUtilBenchmark.openMetricsWriteToByteArray  thrpt   15     457917.887   ± 8855.616  ops/s
TextFormatUtilBenchmark.openMetricsWriteToNull      thrpt   15     466940.767   ± 9258.776  ops/s
TextFormatUtilBenchmark.prometheusWriteToByteArray  thrpt   15     467833.738   ± 7238.974  ops/s
TextFormatUtilBenchmark.prometheusWriteToNull       thrpt   15     481457.991   ± 6341.947  ops/s
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
