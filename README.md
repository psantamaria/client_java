# Prometheus Java Client Benchmarks

## Run Information

- **Date:** 2026-09-13T08:20:52Z
- **Commit:** [`4b69f40`](https://github.com/psantamaria/client_java/commit/4b69f40bd4e616d69468ce99dc4323162287a577)
- **JDK:** 25.0.2 (OpenJDK 64-Bit Server VM)
- **Benchmark config:** 3 fork(s), 3 warmup, 5 measurement, 4 threads
- **Hardware:** AMD EPYC 7763 64-Core Processor, 4 cores, 16 GB RAM
- **OS:** Linux 6.17.0-1022-azure

## Results

### CounterBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusInc | 64.34K | ± 1.31K | ops/s | **fastest** |
| prometheusNoLabelsInc | 56.68K | ± 378.56 | ops/s | 1.1x slower |
| prometheusAdd | 51.47K | ± 260.42 | ops/s | 1.3x slower |
| codahaleIncNoLabels | 48.73K | ± 1.26K | ops/s | 1.3x slower |
| simpleclientInc | 6.66K | ± 35.43 | ops/s | 9.7x slower |
| simpleclientNoLabelsInc | 6.46K | ± 142.08 | ops/s | 10.0x slower |
| simpleclientAdd | 6.19K | ± 214.35 | ops/s | 10x slower |
| openTelemetryAdd | 1.49K | ± 310.38 | ops/s | 43x slower |
| openTelemetryInc | 1.39K | ± 185.57 | ops/s | 46x slower |
| openTelemetryIncNoLabels | 1.29K | ± 178.94 | ops/s | 50x slower |

### HistogramBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusClassic | 6.61K | ± 1.61K | ops/s | **fastest** |
| simpleclient | 4.42K | ± 16.46 | ops/s | 1.5x slower |
| prometheusNative | 2.72K | ± 335.16 | ops/s | 2.4x slower |
| openTelemetryClassic | 664.57 | ± 5.02 | ops/s | 9.9x slower |
| openTelemetryExponential | 576.10 | ± 13.82 | ops/s | 11x slower |

### TextFormatUtilBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusWriteToNull | 479.39K | ± 7.89K | ops/s | **fastest** |
| prometheusWriteToByteArray | 470.97K | ± 10.52K | ops/s | 1.0x slower |
| openMetricsWriteToNull | 461.61K | ± 5.22K | ops/s | 1.0x slower |
| openMetricsWriteToByteArray | 454.75K | ± 6.76K | ops/s | 1.1x slower |

### Raw Results

```
Benchmark                                            Mode  Cnt          Score        Error  Units
CounterBenchmark.codahaleIncNoLabels                thrpt   15      48732.725   ± 1259.616  ops/s
CounterBenchmark.openTelemetryAdd                   thrpt   15       1491.594    ± 310.381  ops/s
CounterBenchmark.openTelemetryInc                   thrpt   15       1393.673    ± 185.573  ops/s
CounterBenchmark.openTelemetryIncNoLabels           thrpt   15       1289.020    ± 178.939  ops/s
CounterBenchmark.prometheusAdd                      thrpt   15      51472.082    ± 260.420  ops/s
CounterBenchmark.prometheusInc                      thrpt   15      64340.529   ± 1310.481  ops/s
CounterBenchmark.prometheusNoLabelsInc              thrpt   15      56681.669    ± 378.557  ops/s
CounterBenchmark.simpleclientAdd                    thrpt   15       6187.184    ± 214.352  ops/s
CounterBenchmark.simpleclientInc                    thrpt   15       6658.575     ± 35.428  ops/s
CounterBenchmark.simpleclientNoLabelsInc            thrpt   15       6461.415    ± 142.079  ops/s
HistogramBenchmark.openTelemetryClassic             thrpt   15        664.568      ± 5.015  ops/s
HistogramBenchmark.openTelemetryExponential         thrpt   15        576.102     ± 13.823  ops/s
HistogramBenchmark.prometheusClassic                thrpt   15       6605.063   ± 1614.551  ops/s
HistogramBenchmark.prometheusNative                 thrpt   15       2723.014    ± 335.162  ops/s
HistogramBenchmark.simpleclient                     thrpt   15       4419.555     ± 16.461  ops/s
TextFormatUtilBenchmark.openMetricsWriteToByteArray  thrpt   15     454753.053   ± 6759.758  ops/s
TextFormatUtilBenchmark.openMetricsWriteToNull      thrpt   15     461612.781   ± 5217.331  ops/s
TextFormatUtilBenchmark.prometheusWriteToByteArray  thrpt   15     470974.000  ± 10515.827  ops/s
TextFormatUtilBenchmark.prometheusWriteToNull       thrpt   15     479386.000   ± 7885.625  ops/s
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
