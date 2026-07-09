# Prometheus Java Client Benchmarks

## Run Information

- **Date:** 2026-07-09T07:16:08Z
- **Commit:** [`4b69f40`](https://github.com/psantamaria/client_java/commit/4b69f40bd4e616d69468ce99dc4323162287a577)
- **JDK:** 25.0.2 (OpenJDK 64-Bit Server VM)
- **Benchmark config:** 3 fork(s), 3 warmup, 5 measurement, 4 threads
- **Hardware:** INTEL(R) XEON(R) PLATINUM 8573C, 4 cores, 16 GB RAM
- **OS:** Linux 6.17.0-1018-azure

## Results

### CounterBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| codahaleIncNoLabels | 31.09K | ± 271.14 | ops/s | **fastest** |
| prometheusNoLabelsInc | 29.95K | ± 419.63 | ops/s | 1.0x slower |
| prometheusInc | 29.80K | ± 153.42 | ops/s | 1.0x slower |
| prometheusAdd | 29.28K | ± 171.53 | ops/s | 1.1x slower |
| simpleclientInc | 7.63K | ± 108.51 | ops/s | 4.1x slower |
| simpleclientNoLabelsInc | 7.50K | ± 78.42 | ops/s | 4.1x slower |
| simpleclientAdd | 7.39K | ± 109.64 | ops/s | 4.2x slower |
| openTelemetryAdd | 1.19K | ± 84.12 | ops/s | 26x slower |
| openTelemetryIncNoLabels | 1.18K | ± 115.34 | ops/s | 26x slower |
| openTelemetryInc | 1.16K | ± 91.25 | ops/s | 27x slower |

### HistogramBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| simpleclient | 5.00K | ± 31.79 | ops/s | **fastest** |
| prometheusClassic | 2.72K | ± 441.01 | ops/s | 1.8x slower |
| prometheusNative | 2.34K | ± 237.33 | ops/s | 2.1x slower |
| openTelemetryClassic | 418.37 | ± 14.52 | ops/s | 12x slower |
| openTelemetryExponential | 337.48 | ± 10.23 | ops/s | 15x slower |

### TextFormatUtilBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusWriteToByteArray | 321.09K | ± 7.08K | ops/s | **fastest** |
| prometheusWriteToNull | 316.65K | ± 1.62K | ops/s | 1.0x slower |
| openMetricsWriteToNull | 306.16K | ± 4.79K | ops/s | 1.0x slower |
| openMetricsWriteToByteArray | 304.06K | ± 4.63K | ops/s | 1.1x slower |

### Raw Results

```
Benchmark                                            Mode  Cnt          Score        Error  Units
CounterBenchmark.codahaleIncNoLabels                thrpt   15      31092.532    ± 271.140  ops/s
CounterBenchmark.openTelemetryAdd                   thrpt   15       1194.684     ± 84.121  ops/s
CounterBenchmark.openTelemetryInc                   thrpt   15       1163.209     ± 91.252  ops/s
CounterBenchmark.openTelemetryIncNoLabels           thrpt   15       1178.158    ± 115.344  ops/s
CounterBenchmark.prometheusAdd                      thrpt   15      29276.428    ± 171.534  ops/s
CounterBenchmark.prometheusInc                      thrpt   15      29803.996    ± 153.421  ops/s
CounterBenchmark.prometheusNoLabelsInc              thrpt   15      29945.032    ± 419.626  ops/s
CounterBenchmark.simpleclientAdd                    thrpt   15       7389.437    ± 109.642  ops/s
CounterBenchmark.simpleclientInc                    thrpt   15       7634.344    ± 108.514  ops/s
CounterBenchmark.simpleclientNoLabelsInc            thrpt   15       7501.080     ± 78.425  ops/s
HistogramBenchmark.openTelemetryClassic             thrpt   15        418.367     ± 14.524  ops/s
HistogramBenchmark.openTelemetryExponential         thrpt   15        337.481     ± 10.234  ops/s
HistogramBenchmark.prometheusClassic                thrpt   15       2722.116    ± 441.013  ops/s
HistogramBenchmark.prometheusNative                 thrpt   15       2336.788    ± 237.329  ops/s
HistogramBenchmark.simpleclient                     thrpt   15       4997.812     ± 31.789  ops/s
TextFormatUtilBenchmark.openMetricsWriteToByteArray  thrpt   15     304063.567   ± 4625.374  ops/s
TextFormatUtilBenchmark.openMetricsWriteToNull      thrpt   15     306163.169   ± 4785.024  ops/s
TextFormatUtilBenchmark.prometheusWriteToByteArray  thrpt   15     321085.931   ± 7078.580  ops/s
TextFormatUtilBenchmark.prometheusWriteToNull       thrpt   15     316645.959   ± 1621.747  ops/s
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
