# Prometheus Java Client Benchmarks

## Run Information

- **Date:** 2026-04-27T06:36:02Z
- **Commit:** [`4b69f40`](https://github.com/psantamaria/client_java/commit/4b69f40bd4e616d69468ce99dc4323162287a577)
- **JDK:** 25.0.2 (OpenJDK 64-Bit Server VM)
- **Benchmark config:** 3 fork(s), 3 warmup, 5 measurement, 4 threads
- **Hardware:** AMD EPYC 7763 64-Core Processor, 4 cores, 16 GB RAM
- **OS:** Linux 6.17.0-1010-azure

## Results

### CounterBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusInc | 65.23K | ± 1.07K | ops/s | **fastest** |
| prometheusNoLabelsInc | 57.07K | ± 464.80 | ops/s | 1.1x slower |
| prometheusAdd | 49.56K | ± 2.31K | ops/s | 1.3x slower |
| codahaleIncNoLabels | 46.95K | ± 79.32 | ops/s | 1.4x slower |
| simpleclientInc | 6.68K | ± 16.95 | ops/s | 9.8x slower |
| simpleclientNoLabelsInc | 6.40K | ± 164.81 | ops/s | 10x slower |
| simpleclientAdd | 6.19K | ± 211.53 | ops/s | 11x slower |
| openTelemetryAdd | 1.48K | ± 266.45 | ops/s | 44x slower |
| openTelemetryInc | 1.37K | ± 135.27 | ops/s | 48x slower |
| openTelemetryIncNoLabels | 1.26K | ± 54.13 | ops/s | 52x slower |

### HistogramBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusClassic | 6.22K | ± 2.10K | ops/s | **fastest** |
| simpleclient | 4.40K | ± 81.20 | ops/s | 1.4x slower |
| prometheusNative | 2.60K | ± 155.00 | ops/s | 2.4x slower |
| openTelemetryClassic | 684.29 | ± 23.55 | ops/s | 9.1x slower |
| openTelemetryExponential | 564.77 | ± 36.80 | ops/s | 11x slower |

### TextFormatUtilBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusWriteToByteArray | 480.29K | ± 2.99K | ops/s | **fastest** |
| prometheusWriteToNull | 479.25K | ± 3.28K | ops/s | 1.0x slower |
| openMetricsWriteToNull | 470.03K | ± 2.50K | ops/s | 1.0x slower |
| openMetricsWriteToByteArray | 466.31K | ± 8.69K | ops/s | 1.0x slower |

### Raw Results

```
Benchmark                                            Mode  Cnt          Score        Error  Units
CounterBenchmark.codahaleIncNoLabels                thrpt   15      46951.808     ± 79.316  ops/s
CounterBenchmark.openTelemetryAdd                   thrpt   15       1480.164    ± 266.445  ops/s
CounterBenchmark.openTelemetryInc                   thrpt   15       1368.912    ± 135.275  ops/s
CounterBenchmark.openTelemetryIncNoLabels           thrpt   15       1262.783     ± 54.130  ops/s
CounterBenchmark.prometheusAdd                      thrpt   15      49560.154   ± 2310.931  ops/s
CounterBenchmark.prometheusInc                      thrpt   15      65226.811   ± 1065.441  ops/s
CounterBenchmark.prometheusNoLabelsInc              thrpt   15      57069.868    ± 464.798  ops/s
CounterBenchmark.simpleclientAdd                    thrpt   15       6193.373    ± 211.528  ops/s
CounterBenchmark.simpleclientInc                    thrpt   15       6679.287     ± 16.949  ops/s
CounterBenchmark.simpleclientNoLabelsInc            thrpt   15       6399.637    ± 164.813  ops/s
HistogramBenchmark.openTelemetryClassic             thrpt   15        684.295     ± 23.552  ops/s
HistogramBenchmark.openTelemetryExponential         thrpt   15        564.767     ± 36.797  ops/s
HistogramBenchmark.prometheusClassic                thrpt   15       6221.014   ± 2098.929  ops/s
HistogramBenchmark.prometheusNative                 thrpt   15       2603.362    ± 155.000  ops/s
HistogramBenchmark.simpleclient                     thrpt   15       4402.960     ± 81.198  ops/s
TextFormatUtilBenchmark.openMetricsWriteToByteArray  thrpt   15     466306.924   ± 8692.400  ops/s
TextFormatUtilBenchmark.openMetricsWriteToNull      thrpt   15     470029.364   ± 2496.783  ops/s
TextFormatUtilBenchmark.prometheusWriteToByteArray  thrpt   15     480291.138   ± 2994.219  ops/s
TextFormatUtilBenchmark.prometheusWriteToNull       thrpt   15     479251.852   ± 3283.655  ops/s
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
