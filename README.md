# Prometheus Java Client Benchmarks

## Run Information

- **Date:** 2026-07-22T06:31:40Z
- **Commit:** [`4b69f40`](https://github.com/psantamaria/client_java/commit/4b69f40bd4e616d69468ce99dc4323162287a577)
- **JDK:** 25.0.2 (OpenJDK 64-Bit Server VM)
- **Benchmark config:** 3 fork(s), 3 warmup, 5 measurement, 4 threads
- **Hardware:** AMD EPYC 7763 64-Core Processor, 4 cores, 16 GB RAM
- **OS:** Linux 6.17.0-1020-azure

## Results

### CounterBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusInc | 63.37K | ± 3.84K | ops/s | **fastest** |
| prometheusNoLabelsInc | 57.00K | ± 417.14 | ops/s | 1.1x slower |
| prometheusAdd | 51.31K | ± 217.07 | ops/s | 1.2x slower |
| codahaleIncNoLabels | 40.39K | ± 13.98K | ops/s | 1.6x slower |
| simpleclientInc | 6.56K | ± 219.43 | ops/s | 9.7x slower |
| simpleclientNoLabelsInc | 6.37K | ± 195.73 | ops/s | 9.9x slower |
| simpleclientAdd | 6.04K | ± 340.74 | ops/s | 10x slower |
| openTelemetryIncNoLabels | 1.47K | ± 78.65 | ops/s | 43x slower |
| openTelemetryAdd | 1.41K | ± 264.60 | ops/s | 45x slower |
| openTelemetryInc | 1.27K | ± 25.82 | ops/s | 50x slower |

### HistogramBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusClassic | 4.72K | ± 602.24 | ops/s | **fastest** |
| simpleclient | 4.44K | ± 51.23 | ops/s | 1.1x slower |
| prometheusNative | 2.78K | ± 227.06 | ops/s | 1.7x slower |
| openTelemetryClassic | 690.78 | ± 28.91 | ops/s | 6.8x slower |
| openTelemetryExponential | 565.64 | ± 38.83 | ops/s | 8.4x slower |

### TextFormatUtilBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusWriteToNull | 484.73K | ± 4.23K | ops/s | **fastest** |
| prometheusWriteToByteArray | 482.65K | ± 5.75K | ops/s | 1.0x slower |
| openMetricsWriteToNull | 481.58K | ± 8.84K | ops/s | 1.0x slower |
| openMetricsWriteToByteArray | 471.87K | ± 8.23K | ops/s | 1.0x slower |

### Raw Results

```
Benchmark                                            Mode  Cnt          Score        Error  Units
CounterBenchmark.codahaleIncNoLabels                thrpt   15      40391.053  ± 13977.284  ops/s
CounterBenchmark.openTelemetryAdd                   thrpt   15       1414.366    ± 264.597  ops/s
CounterBenchmark.openTelemetryInc                   thrpt   15       1274.757     ± 25.824  ops/s
CounterBenchmark.openTelemetryIncNoLabels           thrpt   15       1469.603     ± 78.649  ops/s
CounterBenchmark.prometheusAdd                      thrpt   15      51306.070    ± 217.073  ops/s
CounterBenchmark.prometheusInc                      thrpt   15      63365.441   ± 3844.829  ops/s
CounterBenchmark.prometheusNoLabelsInc              thrpt   15      57004.750    ± 417.136  ops/s
CounterBenchmark.simpleclientAdd                    thrpt   15       6044.314    ± 340.736  ops/s
CounterBenchmark.simpleclientInc                    thrpt   15       6561.920    ± 219.435  ops/s
CounterBenchmark.simpleclientNoLabelsInc            thrpt   15       6368.850    ± 195.731  ops/s
HistogramBenchmark.openTelemetryClassic             thrpt   15        690.778     ± 28.908  ops/s
HistogramBenchmark.openTelemetryExponential         thrpt   15        565.637     ± 38.832  ops/s
HistogramBenchmark.prometheusClassic                thrpt   15       4723.084    ± 602.240  ops/s
HistogramBenchmark.prometheusNative                 thrpt   15       2783.567    ± 227.064  ops/s
HistogramBenchmark.simpleclient                     thrpt   15       4440.158     ± 51.226  ops/s
TextFormatUtilBenchmark.openMetricsWriteToByteArray  thrpt   15     471870.124   ± 8232.238  ops/s
TextFormatUtilBenchmark.openMetricsWriteToNull      thrpt   15     481576.646   ± 8837.331  ops/s
TextFormatUtilBenchmark.prometheusWriteToByteArray  thrpt   15     482648.397   ± 5747.889  ops/s
TextFormatUtilBenchmark.prometheusWriteToNull       thrpt   15     484728.065   ± 4233.515  ops/s
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
