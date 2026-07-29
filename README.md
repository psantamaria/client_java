# Prometheus Java Client Benchmarks

## Run Information

- **Date:** 2026-07-29T06:33:34Z
- **Commit:** [`4b69f40`](https://github.com/psantamaria/client_java/commit/4b69f40bd4e616d69468ce99dc4323162287a577)
- **JDK:** 25.0.2 (OpenJDK 64-Bit Server VM)
- **Benchmark config:** 3 fork(s), 3 warmup, 5 measurement, 4 threads
- **Hardware:** AMD EPYC 9V74 80-Core Processor, 4 cores, 16 GB RAM
- **OS:** Linux 6.17.0-1020-azure

## Results

### CounterBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusInc | 75.16K | ± 4.64K | ops/s | **fastest** |
| prometheusNoLabelsInc | 66.98K | ± 894.83 | ops/s | 1.1x slower |
| prometheusAdd | 63.14K | ± 1.11K | ops/s | 1.2x slower |
| codahaleIncNoLabels | 51.27K | ± 7.43K | ops/s | 1.5x slower |
| simpleclientInc | 8.13K | ± 67.18 | ops/s | 9.2x slower |
| simpleclientNoLabelsInc | 7.86K | ± 298.73 | ops/s | 9.6x slower |
| simpleclientAdd | 7.80K | ± 234.16 | ops/s | 9.6x slower |
| openTelemetryAdd | 1.82K | ± 164.07 | ops/s | 41x slower |
| openTelemetryInc | 1.77K | ± 98.47 | ops/s | 43x slower |
| openTelemetryIncNoLabels | 1.69K | ± 186.41 | ops/s | 44x slower |

### HistogramBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusClassic | 6.92K | ± 1.86K | ops/s | **fastest** |
| simpleclient | 5.38K | ± 32.37 | ops/s | 1.3x slower |
| prometheusNative | 3.96K | ± 156.32 | ops/s | 1.7x slower |
| openTelemetryClassic | 755.39 | ± 23.81 | ops/s | 9.2x slower |
| openTelemetryExponential | 672.77 | ± 20.22 | ops/s | 10x slower |

### TextFormatUtilBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusWriteToNull | 673.79K | ± 4.29K | ops/s | **fastest** |
| prometheusWriteToByteArray | 659.84K | ± 6.80K | ops/s | 1.0x slower |
| openMetricsWriteToNull | 641.53K | ± 9.68K | ops/s | 1.1x slower |
| openMetricsWriteToByteArray | 627.48K | ± 9.32K | ops/s | 1.1x slower |

### Raw Results

```
Benchmark                                            Mode  Cnt          Score        Error  Units
CounterBenchmark.codahaleIncNoLabels                thrpt   15      51272.514   ± 7432.047  ops/s
CounterBenchmark.openTelemetryAdd                   thrpt   15       1818.563    ± 164.067  ops/s
CounterBenchmark.openTelemetryInc                   thrpt   15       1767.282     ± 98.466  ops/s
CounterBenchmark.openTelemetryIncNoLabels           thrpt   15       1691.683    ± 186.414  ops/s
CounterBenchmark.prometheusAdd                      thrpt   15      63136.123   ± 1109.742  ops/s
CounterBenchmark.prometheusInc                      thrpt   15      75160.761   ± 4641.882  ops/s
CounterBenchmark.prometheusNoLabelsInc              thrpt   15      66984.598    ± 894.829  ops/s
CounterBenchmark.simpleclientAdd                    thrpt   15       7801.446    ± 234.157  ops/s
CounterBenchmark.simpleclientInc                    thrpt   15       8133.059     ± 67.177  ops/s
CounterBenchmark.simpleclientNoLabelsInc            thrpt   15       7856.724    ± 298.730  ops/s
HistogramBenchmark.openTelemetryClassic             thrpt   15        755.388     ± 23.805  ops/s
HistogramBenchmark.openTelemetryExponential         thrpt   15        672.772     ± 20.217  ops/s
HistogramBenchmark.prometheusClassic                thrpt   15       6916.560   ± 1860.079  ops/s
HistogramBenchmark.prometheusNative                 thrpt   15       3955.207    ± 156.324  ops/s
HistogramBenchmark.simpleclient                     thrpt   15       5379.226     ± 32.372  ops/s
TextFormatUtilBenchmark.openMetricsWriteToByteArray  thrpt   15     627482.127   ± 9318.755  ops/s
TextFormatUtilBenchmark.openMetricsWriteToNull      thrpt   15     641526.575   ± 9680.479  ops/s
TextFormatUtilBenchmark.prometheusWriteToByteArray  thrpt   15     659835.263   ± 6800.019  ops/s
TextFormatUtilBenchmark.prometheusWriteToNull       thrpt   15     673787.109   ± 4291.326  ops/s
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
