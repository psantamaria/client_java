# Prometheus Java Client Benchmarks

## Run Information

- **Date:** 2026-04-20T06:13:35Z
- **Commit:** [`4b69f40`](https://github.com/psantamaria/client_java/commit/4b69f40bd4e616d69468ce99dc4323162287a577)
- **JDK:** 25.0.2 (OpenJDK 64-Bit Server VM)
- **Benchmark config:** 3 fork(s), 3 warmup, 5 measurement, 4 threads
- **Hardware:** AMD EPYC 7763 64-Core Processor, 4 cores, 16 GB RAM
- **OS:** Linux 6.17.0-1010-azure

## Results

### CounterBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusInc | 65.50K | ± 1.43K | ops/s | **fastest** |
| prometheusNoLabelsInc | 57.22K | ± 165.32 | ops/s | 1.1x slower |
| prometheusAdd | 51.48K | ± 166.95 | ops/s | 1.3x slower |
| codahaleIncNoLabels | 48.07K | ± 1.72K | ops/s | 1.4x slower |
| simpleclientInc | 6.52K | ± 197.16 | ops/s | 10x slower |
| simpleclientNoLabelsInc | 6.50K | ± 194.71 | ops/s | 10x slower |
| simpleclientAdd | 6.30K | ± 267.98 | ops/s | 10x slower |
| openTelemetryInc | 1.35K | ± 198.96 | ops/s | 48x slower |
| openTelemetryAdd | 1.27K | ± 36.97 | ops/s | 52x slower |
| openTelemetryIncNoLabels | 1.23K | ± 31.08 | ops/s | 53x slower |

### HistogramBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusClassic | 5.79K | ± 1.31K | ops/s | **fastest** |
| simpleclient | 4.50K | ± 12.68 | ops/s | 1.3x slower |
| prometheusNative | 2.71K | ± 388.04 | ops/s | 2.1x slower |
| openTelemetryClassic | 710.86 | ± 16.26 | ops/s | 8.1x slower |
| openTelemetryExponential | 550.42 | ± 35.80 | ops/s | 11x slower |

### TextFormatUtilBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusWriteToNull | 482.51K | ± 2.86K | ops/s | **fastest** |
| openMetricsWriteToNull | 473.47K | ± 7.04K | ops/s | 1.0x slower |
| prometheusWriteToByteArray | 471.26K | ± 4.27K | ops/s | 1.0x slower |
| openMetricsWriteToByteArray | 463.84K | ± 2.47K | ops/s | 1.0x slower |

### Raw Results

```
Benchmark                                            Mode  Cnt          Score        Error  Units
CounterBenchmark.codahaleIncNoLabels                thrpt   15      48066.807   ± 1716.556  ops/s
CounterBenchmark.openTelemetryAdd                   thrpt   15       1269.749     ± 36.968  ops/s
CounterBenchmark.openTelemetryInc                   thrpt   15       1354.997    ± 198.957  ops/s
CounterBenchmark.openTelemetryIncNoLabels           thrpt   15       1232.270     ± 31.083  ops/s
CounterBenchmark.prometheusAdd                      thrpt   15      51480.521    ± 166.954  ops/s
CounterBenchmark.prometheusInc                      thrpt   15      65496.180   ± 1430.227  ops/s
CounterBenchmark.prometheusNoLabelsInc              thrpt   15      57215.707    ± 165.324  ops/s
CounterBenchmark.simpleclientAdd                    thrpt   15       6304.493    ± 267.977  ops/s
CounterBenchmark.simpleclientInc                    thrpt   15       6521.435    ± 197.160  ops/s
CounterBenchmark.simpleclientNoLabelsInc            thrpt   15       6501.169    ± 194.712  ops/s
HistogramBenchmark.openTelemetryClassic             thrpt   15        710.862     ± 16.261  ops/s
HistogramBenchmark.openTelemetryExponential         thrpt   15        550.419     ± 35.801  ops/s
HistogramBenchmark.prometheusClassic                thrpt   15       5786.844   ± 1310.381  ops/s
HistogramBenchmark.prometheusNative                 thrpt   15       2705.704    ± 388.043  ops/s
HistogramBenchmark.simpleclient                     thrpt   15       4497.933     ± 12.684  ops/s
TextFormatUtilBenchmark.openMetricsWriteToByteArray  thrpt   15     463844.037   ± 2474.670  ops/s
TextFormatUtilBenchmark.openMetricsWriteToNull      thrpt   15     473466.976   ± 7044.217  ops/s
TextFormatUtilBenchmark.prometheusWriteToByteArray  thrpt   15     471256.070   ± 4266.706  ops/s
TextFormatUtilBenchmark.prometheusWriteToNull       thrpt   15     482513.519   ± 2859.307  ops/s
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
