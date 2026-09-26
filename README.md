# Prometheus Java Client Benchmarks

## Run Information

- **Date:** 2026-09-26T08:14:25Z
- **Commit:** [`4b69f40`](https://github.com/psantamaria/client_java/commit/4b69f40bd4e616d69468ce99dc4323162287a577)
- **JDK:** 25.0.2 (OpenJDK 64-Bit Server VM)
- **Benchmark config:** 3 fork(s), 3 warmup, 5 measurement, 4 threads
- **Hardware:** AMD EPYC 9V45 96-Core Processor, 4 cores, 16 GB RAM
- **OS:** Linux 6.17.0-1022-azure

## Results

### CounterBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusInc | 69.02K | ± 1.70K | ops/s | **fastest** |
| prometheusNoLabelsInc | 68.59K | ± 332.88 | ops/s | 1.0x slower |
| codahaleIncNoLabels | 63.05K | ± 539.62 | ops/s | 1.1x slower |
| prometheusAdd | 57.91K | ± 483.08 | ops/s | 1.2x slower |
| simpleclientNoLabelsInc | 11.07K | ± 46.57 | ops/s | 6.2x slower |
| simpleclientInc | 11.03K | ± 48.34 | ops/s | 6.3x slower |
| simpleclientAdd | 10.66K | ± 79.06 | ops/s | 6.5x slower |
| openTelemetryAdd | 2.20K | ± 289.67 | ops/s | 31x slower |
| openTelemetryInc | 2.14K | ± 308.83 | ops/s | 32x slower |
| openTelemetryIncNoLabels | 1.78K | ± 23.65 | ops/s | 39x slower |

### HistogramBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusClassic | 9.80K | ± 2.91K | ops/s | **fastest** |
| simpleclient | 7.24K | ± 92.71 | ops/s | 1.4x slower |
| prometheusNative | 5.45K | ± 555.70 | ops/s | 1.8x slower |
| openTelemetryClassic | 967.17 | ± 38.07 | ops/s | 10x slower |
| openTelemetryExponential | 755.96 | ± 26.12 | ops/s | 13x slower |

### TextFormatUtilBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusWriteToByteArray | 750.86K | ± 28.09K | ops/s | **fastest** |
| prometheusWriteToNull | 722.05K | ± 20.22K | ops/s | 1.0x slower |
| openMetricsWriteToByteArray | 672.00K | ± 14.81K | ops/s | 1.1x slower |
| openMetricsWriteToNull | 671.16K | ± 13.15K | ops/s | 1.1x slower |

### Raw Results

```
Benchmark                                            Mode  Cnt          Score        Error  Units
CounterBenchmark.codahaleIncNoLabels                thrpt   15      63051.946    ± 539.616  ops/s
CounterBenchmark.openTelemetryAdd                   thrpt   15       2201.814    ± 289.674  ops/s
CounterBenchmark.openTelemetryInc                   thrpt   15       2141.187    ± 308.834  ops/s
CounterBenchmark.openTelemetryIncNoLabels           thrpt   15       1780.855     ± 23.645  ops/s
CounterBenchmark.prometheusAdd                      thrpt   15      57914.778    ± 483.075  ops/s
CounterBenchmark.prometheusInc                      thrpt   15      69022.291   ± 1701.663  ops/s
CounterBenchmark.prometheusNoLabelsInc              thrpt   15      68587.191    ± 332.877  ops/s
CounterBenchmark.simpleclientAdd                    thrpt   15      10660.613     ± 79.063  ops/s
CounterBenchmark.simpleclientInc                    thrpt   15      11028.305     ± 48.338  ops/s
CounterBenchmark.simpleclientNoLabelsInc            thrpt   15      11073.193     ± 46.575  ops/s
HistogramBenchmark.openTelemetryClassic             thrpt   15        967.172     ± 38.068  ops/s
HistogramBenchmark.openTelemetryExponential         thrpt   15        755.962     ± 26.120  ops/s
HistogramBenchmark.prometheusClassic                thrpt   15       9799.245   ± 2905.339  ops/s
HistogramBenchmark.prometheusNative                 thrpt   15       5450.613    ± 555.703  ops/s
HistogramBenchmark.simpleclient                     thrpt   15       7242.494     ± 92.706  ops/s
TextFormatUtilBenchmark.openMetricsWriteToByteArray  thrpt   15     672000.272  ± 14807.565  ops/s
TextFormatUtilBenchmark.openMetricsWriteToNull      thrpt   15     671159.245  ± 13145.084  ops/s
TextFormatUtilBenchmark.prometheusWriteToByteArray  thrpt   15     750858.783  ± 28090.472  ops/s
TextFormatUtilBenchmark.prometheusWriteToNull       thrpt   15     722053.055  ± 20220.737  ops/s
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
