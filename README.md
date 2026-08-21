# Prometheus Java Client Benchmarks

## Run Information

- **Date:** 2026-08-21T04:13:21Z
- **Commit:** [`4b69f40`](https://github.com/psantamaria/client_java/commit/4b69f40bd4e616d69468ce99dc4323162287a577)
- **JDK:** 25.0.2 (OpenJDK 64-Bit Server VM)
- **Benchmark config:** 3 fork(s), 3 warmup, 5 measurement, 4 threads
- **Hardware:** AMD EPYC 9V74 80-Core Processor, 4 cores, 16 GB RAM
- **OS:** Linux 6.17.0-1022-azure

## Results

### CounterBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusInc | 59.71K | ± 1.17K | ops/s | **fastest** |
| prometheusNoLabelsInc | 51.59K | ± 853.86 | ops/s | 1.2x slower |
| prometheusAdd | 48.73K | ± 370.64 | ops/s | 1.2x slower |
| codahaleIncNoLabels | 43.73K | ± 344.64 | ops/s | 1.4x slower |
| simpleclientInc | 6.16K | ± 165.10 | ops/s | 9.7x slower |
| simpleclientNoLabelsInc | 6.00K | ± 255.66 | ops/s | 9.9x slower |
| simpleclientAdd | 5.96K | ± 319.24 | ops/s | 10x slower |
| openTelemetryAdd | 1.54K | ± 187.01 | ops/s | 39x slower |
| openTelemetryInc | 1.46K | ± 78.37 | ops/s | 41x slower |
| openTelemetryIncNoLabels | 1.42K | ± 23.11 | ops/s | 42x slower |

### HistogramBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusClassic | 5.69K | ± 1.41K | ops/s | **fastest** |
| simpleclient | 4.51K | ± 76.80 | ops/s | 1.3x slower |
| prometheusNative | 2.90K | ± 202.04 | ops/s | 2.0x slower |
| openTelemetryClassic | 594.28 | ± 12.77 | ops/s | 9.6x slower |
| openTelemetryExponential | 525.42 | ± 13.96 | ops/s | 11x slower |

### TextFormatUtilBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusWriteToNull | 552.67K | ± 9.72K | ops/s | **fastest** |
| prometheusWriteToByteArray | 538.12K | ± 12.72K | ops/s | 1.0x slower |
| openMetricsWriteToNull | 534.76K | ± 4.94K | ops/s | 1.0x slower |
| openMetricsWriteToByteArray | 527.37K | ± 5.29K | ops/s | 1.0x slower |

### Raw Results

```
Benchmark                                            Mode  Cnt          Score        Error  Units
CounterBenchmark.codahaleIncNoLabels                thrpt   15      43730.657    ± 344.638  ops/s
CounterBenchmark.openTelemetryAdd                   thrpt   15       1536.890    ± 187.012  ops/s
CounterBenchmark.openTelemetryInc                   thrpt   15       1463.602     ± 78.374  ops/s
CounterBenchmark.openTelemetryIncNoLabels           thrpt   15       1416.775     ± 23.110  ops/s
CounterBenchmark.prometheusAdd                      thrpt   15      48731.887    ± 370.644  ops/s
CounterBenchmark.prometheusInc                      thrpt   15      59712.556   ± 1173.462  ops/s
CounterBenchmark.prometheusNoLabelsInc              thrpt   15      51588.019    ± 853.856  ops/s
CounterBenchmark.simpleclientAdd                    thrpt   15       5957.946    ± 319.244  ops/s
CounterBenchmark.simpleclientInc                    thrpt   15       6161.756    ± 165.099  ops/s
CounterBenchmark.simpleclientNoLabelsInc            thrpt   15       6001.392    ± 255.660  ops/s
HistogramBenchmark.openTelemetryClassic             thrpt   15        594.284     ± 12.773  ops/s
HistogramBenchmark.openTelemetryExponential         thrpt   15        525.420     ± 13.958  ops/s
HistogramBenchmark.prometheusClassic                thrpt   15       5692.108   ± 1410.546  ops/s
HistogramBenchmark.prometheusNative                 thrpt   15       2901.072    ± 202.041  ops/s
HistogramBenchmark.simpleclient                     thrpt   15       4505.890     ± 76.805  ops/s
TextFormatUtilBenchmark.openMetricsWriteToByteArray  thrpt   15     527372.740   ± 5294.924  ops/s
TextFormatUtilBenchmark.openMetricsWriteToNull      thrpt   15     534755.253   ± 4941.874  ops/s
TextFormatUtilBenchmark.prometheusWriteToByteArray  thrpt   15     538116.413  ± 12723.655  ops/s
TextFormatUtilBenchmark.prometheusWriteToNull       thrpt   15     552668.213   ± 9721.598  ops/s
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
