# Prometheus Java Client Benchmarks

## Run Information

- **Date:** 2026-05-12T06:51:03Z
- **Commit:** [`4b69f40`](https://github.com/psantamaria/client_java/commit/4b69f40bd4e616d69468ce99dc4323162287a577)
- **JDK:** 25.0.2 (OpenJDK 64-Bit Server VM)
- **Benchmark config:** 3 fork(s), 3 warmup, 5 measurement, 4 threads
- **Hardware:** AMD EPYC 9V74 80-Core Processor, 4 cores, 16 GB RAM
- **OS:** Linux 6.17.0-1010-azure

## Results

### CounterBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusInc | 77.01K | ± 523.95 | ops/s | **fastest** |
| prometheusNoLabelsInc | 67.17K | ± 652.68 | ops/s | 1.1x slower |
| prometheusAdd | 61.53K | ± 4.28K | ops/s | 1.3x slower |
| codahaleIncNoLabels | 56.97K | ± 375.63 | ops/s | 1.4x slower |
| simpleclientInc | 8.09K | ± 30.11 | ops/s | 9.5x slower |
| simpleclientNoLabelsInc | 7.91K | ± 343.13 | ops/s | 9.7x slower |
| simpleclientAdd | 7.84K | ± 232.31 | ops/s | 9.8x slower |
| openTelemetryAdd | 1.80K | ± 36.17 | ops/s | 43x slower |
| openTelemetryIncNoLabels | 1.78K | ± 160.67 | ops/s | 43x slower |
| openTelemetryInc | 1.76K | ± 104.30 | ops/s | 44x slower |

### HistogramBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusClassic | 7.70K | ± 1.57K | ops/s | **fastest** |
| simpleclient | 5.85K | ± 202.55 | ops/s | 1.3x slower |
| prometheusNative | 3.67K | ± 334.54 | ops/s | 2.1x slower |
| openTelemetryClassic | 841.59 | ± 44.53 | ops/s | 9.1x slower |
| openTelemetryExponential | 689.53 | ± 34.02 | ops/s | 11x slower |

### TextFormatUtilBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusWriteToNull | 679.18K | ± 4.31K | ops/s | **fastest** |
| prometheusWriteToByteArray | 663.74K | ± 7.56K | ops/s | 1.0x slower |
| openMetricsWriteToNull | 657.83K | ± 3.72K | ops/s | 1.0x slower |
| openMetricsWriteToByteArray | 628.68K | ± 3.20K | ops/s | 1.1x slower |

### Raw Results

```
Benchmark                                            Mode  Cnt          Score        Error  Units
CounterBenchmark.codahaleIncNoLabels                thrpt   15      56971.553    ± 375.629  ops/s
CounterBenchmark.openTelemetryAdd                   thrpt   15       1798.678     ± 36.175  ops/s
CounterBenchmark.openTelemetryInc                   thrpt   15       1755.766    ± 104.304  ops/s
CounterBenchmark.openTelemetryIncNoLabels           thrpt   15       1781.604    ± 160.672  ops/s
CounterBenchmark.prometheusAdd                      thrpt   15      61531.455   ± 4284.072  ops/s
CounterBenchmark.prometheusInc                      thrpt   15      77014.485    ± 523.953  ops/s
CounterBenchmark.prometheusNoLabelsInc              thrpt   15      67170.906    ± 652.680  ops/s
CounterBenchmark.simpleclientAdd                    thrpt   15       7839.453    ± 232.307  ops/s
CounterBenchmark.simpleclientInc                    thrpt   15       8085.948     ± 30.113  ops/s
CounterBenchmark.simpleclientNoLabelsInc            thrpt   15       7906.826    ± 343.127  ops/s
HistogramBenchmark.openTelemetryClassic             thrpt   15        841.586     ± 44.526  ops/s
HistogramBenchmark.openTelemetryExponential         thrpt   15        689.532     ± 34.021  ops/s
HistogramBenchmark.prometheusClassic                thrpt   15       7695.312   ± 1572.761  ops/s
HistogramBenchmark.prometheusNative                 thrpt   15       3668.724    ± 334.540  ops/s
HistogramBenchmark.simpleclient                     thrpt   15       5854.664    ± 202.553  ops/s
TextFormatUtilBenchmark.openMetricsWriteToByteArray  thrpt   15     628676.591   ± 3197.545  ops/s
TextFormatUtilBenchmark.openMetricsWriteToNull      thrpt   15     657826.840   ± 3723.110  ops/s
TextFormatUtilBenchmark.prometheusWriteToByteArray  thrpt   15     663735.537   ± 7556.245  ops/s
TextFormatUtilBenchmark.prometheusWriteToNull       thrpt   15     679183.767   ± 4308.232  ops/s
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
