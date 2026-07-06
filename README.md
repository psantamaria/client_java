# Prometheus Java Client Benchmarks

## Run Information

- **Date:** 2026-07-06T07:39:27Z
- **Commit:** [`4b69f40`](https://github.com/psantamaria/client_java/commit/4b69f40bd4e616d69468ce99dc4323162287a577)
- **JDK:** 25.0.2 (OpenJDK 64-Bit Server VM)
- **Benchmark config:** 3 fork(s), 3 warmup, 5 measurement, 4 threads
- **Hardware:** AMD EPYC 9V74 80-Core Processor, 4 cores, 16 GB RAM
- **OS:** Linux 6.17.0-1018-azure

## Results

### CounterBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusInc | 76.30K | ± 1.20K | ops/s | **fastest** |
| prometheusNoLabelsInc | 66.33K | ± 530.16 | ops/s | 1.2x slower |
| codahaleIncNoLabels | 57.29K | ± 537.11 | ops/s | 1.3x slower |
| prometheusAdd | 54.77K | ± 13.54K | ops/s | 1.4x slower |
| simpleclientNoLabelsInc | 7.98K | ± 226.93 | ops/s | 9.6x slower |
| simpleclientInc | 7.98K | ± 112.11 | ops/s | 9.6x slower |
| simpleclientAdd | 7.68K | ± 501.67 | ops/s | 9.9x slower |
| openTelemetryInc | 1.73K | ± 46.16 | ops/s | 44x slower |
| openTelemetryAdd | 1.71K | ± 39.51 | ops/s | 45x slower |
| openTelemetryIncNoLabels | 1.70K | ± 69.32 | ops/s | 45x slower |

### HistogramBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusClassic | 7.08K | ± 2.14K | ops/s | **fastest** |
| simpleclient | 5.94K | ± 69.27 | ops/s | 1.2x slower |
| prometheusNative | 4.02K | ± 235.06 | ops/s | 1.8x slower |
| openTelemetryClassic | 772.31 | ± 47.11 | ops/s | 9.2x slower |
| openTelemetryExponential | 670.81 | ± 34.28 | ops/s | 11x slower |

### TextFormatUtilBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusWriteToNull | 670.31K | ± 3.85K | ops/s | **fastest** |
| prometheusWriteToByteArray | 657.50K | ± 7.54K | ops/s | 1.0x slower |
| openMetricsWriteToByteArray | 633.63K | ± 4.49K | ops/s | 1.1x slower |
| openMetricsWriteToNull | 629.42K | ± 13.29K | ops/s | 1.1x slower |

### Raw Results

```
Benchmark                                            Mode  Cnt          Score        Error  Units
CounterBenchmark.codahaleIncNoLabels                thrpt   15      57286.705    ± 537.109  ops/s
CounterBenchmark.openTelemetryAdd                   thrpt   15       1709.959     ± 39.510  ops/s
CounterBenchmark.openTelemetryInc                   thrpt   15       1727.790     ± 46.158  ops/s
CounterBenchmark.openTelemetryIncNoLabels           thrpt   15       1700.586     ± 69.319  ops/s
CounterBenchmark.prometheusAdd                      thrpt   15      54771.191  ± 13537.234  ops/s
CounterBenchmark.prometheusInc                      thrpt   15      76298.726   ± 1201.057  ops/s
CounterBenchmark.prometheusNoLabelsInc              thrpt   15      66328.076    ± 530.163  ops/s
CounterBenchmark.simpleclientAdd                    thrpt   15       7680.405    ± 501.665  ops/s
CounterBenchmark.simpleclientInc                    thrpt   15       7977.102    ± 112.108  ops/s
CounterBenchmark.simpleclientNoLabelsInc            thrpt   15       7977.532    ± 226.933  ops/s
HistogramBenchmark.openTelemetryClassic             thrpt   15        772.312     ± 47.113  ops/s
HistogramBenchmark.openTelemetryExponential         thrpt   15        670.809     ± 34.283  ops/s
HistogramBenchmark.prometheusClassic                thrpt   15       7081.239   ± 2140.465  ops/s
HistogramBenchmark.prometheusNative                 thrpt   15       4021.811    ± 235.065  ops/s
HistogramBenchmark.simpleclient                     thrpt   15       5940.218     ± 69.268  ops/s
TextFormatUtilBenchmark.openMetricsWriteToByteArray  thrpt   15     633634.139   ± 4488.647  ops/s
TextFormatUtilBenchmark.openMetricsWriteToNull      thrpt   15     629419.504  ± 13294.034  ops/s
TextFormatUtilBenchmark.prometheusWriteToByteArray  thrpt   15     657495.557   ± 7541.728  ops/s
TextFormatUtilBenchmark.prometheusWriteToNull       thrpt   15     670313.556   ± 3850.098  ops/s
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
