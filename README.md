# Prometheus Java Client Benchmarks

## Run Information

- **Date:** 2026-09-22T08:27:15Z
- **Commit:** [`4b69f40`](https://github.com/psantamaria/client_java/commit/4b69f40bd4e616d69468ce99dc4323162287a577)
- **JDK:** 25.0.2 (OpenJDK 64-Bit Server VM)
- **Benchmark config:** 3 fork(s), 3 warmup, 5 measurement, 4 threads
- **Hardware:** AMD EPYC 9V45 96-Core Processor, 4 cores, 16 GB RAM
- **OS:** Linux 6.17.0-1022-azure

## Results

### CounterBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusNoLabelsInc | 67.46K | ± 627.66 | ops/s | **fastest** |
| prometheusInc | 67.46K | ± 1.27K | ops/s | 1.0x slower |
| codahaleIncNoLabels | 65.06K | ± 2.77K | ops/s | 1.0x slower |
| prometheusAdd | 57.46K | ± 551.71 | ops/s | 1.2x slower |
| simpleclientInc | 10.91K | ± 185.46 | ops/s | 6.2x slower |
| simpleclientAdd | 10.81K | ± 337.02 | ops/s | 6.2x slower |
| simpleclientNoLabelsInc | 10.73K | ± 140.35 | ops/s | 6.3x slower |
| openTelemetryAdd | 2.09K | ± 250.50 | ops/s | 32x slower |
| openTelemetryInc | 1.92K | ± 217.82 | ops/s | 35x slower |
| openTelemetryIncNoLabels | 1.67K | ± 114.98 | ops/s | 40x slower |

### HistogramBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| simpleclient | 7.12K | ± 196.83 | ops/s | **fastest** |
| prometheusClassic | 6.26K | ± 735.09 | ops/s | 1.1x slower |
| prometheusNative | 5.55K | ± 247.83 | ops/s | 1.3x slower |
| openTelemetryClassic | 837.41 | ± 44.91 | ops/s | 8.5x slower |
| openTelemetryExponential | 656.65 | ± 22.49 | ops/s | 11x slower |

### TextFormatUtilBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusWriteToNull | 736.40K | ± 32.56K | ops/s | **fastest** |
| prometheusWriteToByteArray | 734.02K | ± 25.21K | ops/s | 1.0x slower |
| openMetricsWriteToByteArray | 688.11K | ± 20.49K | ops/s | 1.1x slower |
| openMetricsWriteToNull | 669.98K | ± 23.21K | ops/s | 1.1x slower |

### Raw Results

```
Benchmark                                            Mode  Cnt          Score        Error  Units
CounterBenchmark.codahaleIncNoLabels                thrpt   15      65062.331   ± 2774.834  ops/s
CounterBenchmark.openTelemetryAdd                   thrpt   15       2091.695    ± 250.501  ops/s
CounterBenchmark.openTelemetryInc                   thrpt   15       1920.715    ± 217.823  ops/s
CounterBenchmark.openTelemetryIncNoLabels           thrpt   15       1674.269    ± 114.982  ops/s
CounterBenchmark.prometheusAdd                      thrpt   15      57460.540    ± 551.711  ops/s
CounterBenchmark.prometheusInc                      thrpt   15      67458.409   ± 1274.439  ops/s
CounterBenchmark.prometheusNoLabelsInc              thrpt   15      67459.135    ± 627.658  ops/s
CounterBenchmark.simpleclientAdd                    thrpt   15      10811.253    ± 337.018  ops/s
CounterBenchmark.simpleclientInc                    thrpt   15      10911.254    ± 185.460  ops/s
CounterBenchmark.simpleclientNoLabelsInc            thrpt   15      10734.246    ± 140.348  ops/s
HistogramBenchmark.openTelemetryClassic             thrpt   15        837.415     ± 44.908  ops/s
HistogramBenchmark.openTelemetryExponential         thrpt   15        656.646     ± 22.490  ops/s
HistogramBenchmark.prometheusClassic                thrpt   15       6263.850    ± 735.088  ops/s
HistogramBenchmark.prometheusNative                 thrpt   15       5547.772    ± 247.834  ops/s
HistogramBenchmark.simpleclient                     thrpt   15       7115.639    ± 196.834  ops/s
TextFormatUtilBenchmark.openMetricsWriteToByteArray  thrpt   15     688107.556  ± 20486.425  ops/s
TextFormatUtilBenchmark.openMetricsWriteToNull      thrpt   15     669980.536  ± 23211.392  ops/s
TextFormatUtilBenchmark.prometheusWriteToByteArray  thrpt   15     734021.560  ± 25210.435  ops/s
TextFormatUtilBenchmark.prometheusWriteToNull       thrpt   15     736402.728  ± 32556.714  ops/s
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
