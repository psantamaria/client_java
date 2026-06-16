# Prometheus Java Client Benchmarks

## Run Information

- **Date:** 2026-06-16T08:38:20Z
- **Commit:** [`4b69f40`](https://github.com/psantamaria/client_java/commit/4b69f40bd4e616d69468ce99dc4323162287a577)
- **JDK:** 25.0.2 (OpenJDK 64-Bit Server VM)
- **Benchmark config:** 3 fork(s), 3 warmup, 5 measurement, 4 threads
- **Hardware:** AMD EPYC 9V74 80-Core Processor, 4 cores, 16 GB RAM
- **OS:** Linux 6.17.0-1018-azure

## Results

### CounterBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusInc | 58.95K | ± 55.54 | ops/s | **fastest** |
| prometheusNoLabelsInc | 51.37K | ± 424.57 | ops/s | 1.1x slower |
| prometheusAdd | 47.90K | ± 546.60 | ops/s | 1.2x slower |
| codahaleIncNoLabels | 43.36K | ± 1.23K | ops/s | 1.4x slower |
| simpleclientInc | 6.32K | ± 48.03 | ops/s | 9.3x slower |
| simpleclientNoLabelsInc | 5.79K | ± 102.54 | ops/s | 10x slower |
| simpleclientAdd | 5.78K | ± 124.62 | ops/s | 10x slower |
| openTelemetryAdd | 1.38K | ± 43.64 | ops/s | 43x slower |
| openTelemetryInc | 1.36K | ± 21.27 | ops/s | 43x slower |
| openTelemetryIncNoLabels | 1.36K | ± 15.76 | ops/s | 43x slower |

### HistogramBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusClassic | 5.66K | ± 1.20K | ops/s | **fastest** |
| simpleclient | 4.40K | ± 27.82 | ops/s | 1.3x slower |
| prometheusNative | 2.96K | ± 227.45 | ops/s | 1.9x slower |
| openTelemetryClassic | 602.29 | ± 32.48 | ops/s | 9.4x slower |
| openTelemetryExponential | 547.75 | ± 13.64 | ops/s | 10x slower |

### TextFormatUtilBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusWriteToNull | 551.37K | ± 5.65K | ops/s | **fastest** |
| prometheusWriteToByteArray | 548.92K | ± 1.94K | ops/s | 1.0x slower |
| openMetricsWriteToNull | 534.38K | ± 3.14K | ops/s | 1.0x slower |
| openMetricsWriteToByteArray | 521.95K | ± 11.43K | ops/s | 1.1x slower |

### Raw Results

```
Benchmark                                            Mode  Cnt          Score        Error  Units
CounterBenchmark.codahaleIncNoLabels                thrpt   15      43359.527   ± 1227.803  ops/s
CounterBenchmark.openTelemetryAdd                   thrpt   15       1383.355     ± 43.636  ops/s
CounterBenchmark.openTelemetryInc                   thrpt   15       1364.777     ± 21.266  ops/s
CounterBenchmark.openTelemetryIncNoLabels           thrpt   15       1357.504     ± 15.760  ops/s
CounterBenchmark.prometheusAdd                      thrpt   15      47900.664    ± 546.602  ops/s
CounterBenchmark.prometheusInc                      thrpt   15      58950.147     ± 55.536  ops/s
CounterBenchmark.prometheusNoLabelsInc              thrpt   15      51374.184    ± 424.565  ops/s
CounterBenchmark.simpleclientAdd                    thrpt   15       5783.880    ± 124.619  ops/s
CounterBenchmark.simpleclientInc                    thrpt   15       6316.046     ± 48.025  ops/s
CounterBenchmark.simpleclientNoLabelsInc            thrpt   15       5785.445    ± 102.543  ops/s
HistogramBenchmark.openTelemetryClassic             thrpt   15        602.289     ± 32.484  ops/s
HistogramBenchmark.openTelemetryExponential         thrpt   15        547.746     ± 13.640  ops/s
HistogramBenchmark.prometheusClassic                thrpt   15       5661.171   ± 1200.602  ops/s
HistogramBenchmark.prometheusNative                 thrpt   15       2956.135    ± 227.449  ops/s
HistogramBenchmark.simpleclient                     thrpt   15       4399.174     ± 27.821  ops/s
TextFormatUtilBenchmark.openMetricsWriteToByteArray  thrpt   15     521954.260  ± 11430.079  ops/s
TextFormatUtilBenchmark.openMetricsWriteToNull      thrpt   15     534375.704   ± 3140.931  ops/s
TextFormatUtilBenchmark.prometheusWriteToByteArray  thrpt   15     548921.462   ± 1942.711  ops/s
TextFormatUtilBenchmark.prometheusWriteToNull       thrpt   15     551371.645   ± 5645.783  ops/s
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
