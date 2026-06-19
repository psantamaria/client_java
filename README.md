# Prometheus Java Client Benchmarks

## Run Information

- **Date:** 2026-06-19T08:17:48Z
- **Commit:** [`4b69f40`](https://github.com/psantamaria/client_java/commit/4b69f40bd4e616d69468ce99dc4323162287a577)
- **JDK:** 25.0.2 (OpenJDK 64-Bit Server VM)
- **Benchmark config:** 3 fork(s), 3 warmup, 5 measurement, 4 threads
- **Hardware:** AMD EPYC 7763 64-Core Processor, 4 cores, 16 GB RAM
- **OS:** Linux 6.17.0-1018-azure

## Results

### CounterBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusInc | 66.99K | ± 447.23 | ops/s | **fastest** |
| prometheusNoLabelsInc | 56.73K | ± 342.33 | ops/s | 1.2x slower |
| prometheusAdd | 51.41K | ± 84.87 | ops/s | 1.3x slower |
| codahaleIncNoLabels | 48.97K | ± 1.93K | ops/s | 1.4x slower |
| simpleclientInc | 6.55K | ± 189.37 | ops/s | 10x slower |
| simpleclientNoLabelsInc | 6.39K | ± 198.88 | ops/s | 10x slower |
| simpleclientAdd | 6.30K | ± 229.91 | ops/s | 11x slower |
| openTelemetryIncNoLabels | 1.41K | ± 169.80 | ops/s | 47x slower |
| openTelemetryInc | 1.25K | ± 32.36 | ops/s | 54x slower |
| openTelemetryAdd | 1.24K | ± 52.91 | ops/s | 54x slower |

### HistogramBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusClassic | 6.09K | ± 1.40K | ops/s | **fastest** |
| simpleclient | 4.42K | ± 36.27 | ops/s | 1.4x slower |
| prometheusNative | 2.81K | ± 166.69 | ops/s | 2.2x slower |
| openTelemetryClassic | 686.38 | ± 14.68 | ops/s | 8.9x slower |
| openTelemetryExponential | 546.76 | ± 37.78 | ops/s | 11x slower |

### TextFormatUtilBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusWriteToNull | 493.25K | ± 4.03K | ops/s | **fastest** |
| prometheusWriteToByteArray | 484.38K | ± 1.90K | ops/s | 1.0x slower |
| openMetricsWriteToNull | 482.15K | ± 7.42K | ops/s | 1.0x slower |
| openMetricsWriteToByteArray | 477.82K | ± 3.81K | ops/s | 1.0x slower |

### Raw Results

```
Benchmark                                            Mode  Cnt          Score        Error  Units
CounterBenchmark.codahaleIncNoLabels                thrpt   15      48970.100   ± 1932.017  ops/s
CounterBenchmark.openTelemetryAdd                   thrpt   15       1244.055     ± 52.910  ops/s
CounterBenchmark.openTelemetryInc                   thrpt   15       1247.649     ± 32.361  ops/s
CounterBenchmark.openTelemetryIncNoLabels           thrpt   15       1413.459    ± 169.798  ops/s
CounterBenchmark.prometheusAdd                      thrpt   15      51412.625     ± 84.874  ops/s
CounterBenchmark.prometheusInc                      thrpt   15      66990.677    ± 447.233  ops/s
CounterBenchmark.prometheusNoLabelsInc              thrpt   15      56730.263    ± 342.325  ops/s
CounterBenchmark.simpleclientAdd                    thrpt   15       6302.991    ± 229.912  ops/s
CounterBenchmark.simpleclientInc                    thrpt   15       6553.655    ± 189.371  ops/s
CounterBenchmark.simpleclientNoLabelsInc            thrpt   15       6390.980    ± 198.884  ops/s
HistogramBenchmark.openTelemetryClassic             thrpt   15        686.377     ± 14.679  ops/s
HistogramBenchmark.openTelemetryExponential         thrpt   15        546.763     ± 37.782  ops/s
HistogramBenchmark.prometheusClassic                thrpt   15       6091.876   ± 1400.745  ops/s
HistogramBenchmark.prometheusNative                 thrpt   15       2812.339    ± 166.685  ops/s
HistogramBenchmark.simpleclient                     thrpt   15       4416.618     ± 36.265  ops/s
TextFormatUtilBenchmark.openMetricsWriteToByteArray  thrpt   15     477817.062   ± 3810.027  ops/s
TextFormatUtilBenchmark.openMetricsWriteToNull      thrpt   15     482147.899   ± 7415.413  ops/s
TextFormatUtilBenchmark.prometheusWriteToByteArray  thrpt   15     484382.862   ± 1903.436  ops/s
TextFormatUtilBenchmark.prometheusWriteToNull       thrpt   15     493251.678   ± 4028.167  ops/s
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
