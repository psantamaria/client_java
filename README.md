# Prometheus Java Client Benchmarks

## Run Information

- **Date:** 2026-05-05T06:13:43Z
- **Commit:** [`4b69f40`](https://github.com/psantamaria/client_java/commit/4b69f40bd4e616d69468ce99dc4323162287a577)
- **JDK:** 25.0.2 (OpenJDK 64-Bit Server VM)
- **Benchmark config:** 3 fork(s), 3 warmup, 5 measurement, 4 threads
- **Hardware:** AMD EPYC 9V74 80-Core Processor, 4 cores, 16 GB RAM
- **OS:** Linux 6.17.0-1010-azure

## Results

### CounterBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusInc | 57.15K | ± 3.22K | ops/s | **fastest** |
| prometheusNoLabelsInc | 50.88K | ± 444.93 | ops/s | 1.1x slower |
| prometheusAdd | 48.91K | ± 571.60 | ops/s | 1.2x slower |
| codahaleIncNoLabels | 42.48K | ± 1.30K | ops/s | 1.3x slower |
| simpleclientNoLabelsInc | 6.16K | ± 148.68 | ops/s | 9.3x slower |
| simpleclientInc | 6.14K | ± 141.83 | ops/s | 9.3x slower |
| simpleclientAdd | 5.88K | ± 151.49 | ops/s | 9.7x slower |
| openTelemetryAdd | 1.37K | ± 73.18 | ops/s | 42x slower |
| openTelemetryInc | 1.34K | ± 45.00 | ops/s | 43x slower |
| openTelemetryIncNoLabels | 1.24K | ± 64.01 | ops/s | 46x slower |

### HistogramBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusClassic | 5.80K | ± 1.29K | ops/s | **fastest** |
| simpleclient | 4.56K | ± 76.14 | ops/s | 1.3x slower |
| prometheusNative | 2.85K | ± 286.27 | ops/s | 2.0x slower |
| openTelemetryClassic | 601.40 | ± 10.77 | ops/s | 9.7x slower |
| openTelemetryExponential | 519.56 | ± 18.89 | ops/s | 11x slower |

### TextFormatUtilBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusWriteToNull | 558.87K | ± 6.05K | ops/s | **fastest** |
| prometheusWriteToByteArray | 542.79K | ± 3.41K | ops/s | 1.0x slower |
| openMetricsWriteToNull | 533.63K | ± 2.30K | ops/s | 1.0x slower |
| openMetricsWriteToByteArray | 520.35K | ± 14.24K | ops/s | 1.1x slower |

### Raw Results

```
Benchmark                                            Mode  Cnt          Score        Error  Units
CounterBenchmark.codahaleIncNoLabels                thrpt   15      42479.875   ± 1301.687  ops/s
CounterBenchmark.openTelemetryAdd                   thrpt   15       1366.919     ± 73.180  ops/s
CounterBenchmark.openTelemetryInc                   thrpt   15       1339.369     ± 44.997  ops/s
CounterBenchmark.openTelemetryIncNoLabels           thrpt   15       1243.669     ± 64.014  ops/s
CounterBenchmark.prometheusAdd                      thrpt   15      48912.386    ± 571.597  ops/s
CounterBenchmark.prometheusInc                      thrpt   15      57145.493   ± 3224.870  ops/s
CounterBenchmark.prometheusNoLabelsInc              thrpt   15      50877.474    ± 444.930  ops/s
CounterBenchmark.simpleclientAdd                    thrpt   15       5884.855    ± 151.494  ops/s
CounterBenchmark.simpleclientInc                    thrpt   15       6136.448    ± 141.830  ops/s
CounterBenchmark.simpleclientNoLabelsInc            thrpt   15       6156.267    ± 148.681  ops/s
HistogramBenchmark.openTelemetryClassic             thrpt   15        601.405     ± 10.769  ops/s
HistogramBenchmark.openTelemetryExponential         thrpt   15        519.559     ± 18.895  ops/s
HistogramBenchmark.prometheusClassic                thrpt   15       5803.665   ± 1289.635  ops/s
HistogramBenchmark.prometheusNative                 thrpt   15       2853.660    ± 286.275  ops/s
HistogramBenchmark.simpleclient                     thrpt   15       4556.762     ± 76.145  ops/s
TextFormatUtilBenchmark.openMetricsWriteToByteArray  thrpt   15     520352.077  ± 14237.501  ops/s
TextFormatUtilBenchmark.openMetricsWriteToNull      thrpt   15     533628.107   ± 2298.883  ops/s
TextFormatUtilBenchmark.prometheusWriteToByteArray  thrpt   15     542793.374   ± 3405.176  ops/s
TextFormatUtilBenchmark.prometheusWriteToNull       thrpt   15     558871.541   ± 6053.887  ops/s
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
