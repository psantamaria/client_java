# Prometheus Java Client Benchmarks

## Run Information

- **Date:** 2026-09-12T08:03:02Z
- **Commit:** [`4b69f40`](https://github.com/psantamaria/client_java/commit/4b69f40bd4e616d69468ce99dc4323162287a577)
- **JDK:** 25.0.2 (OpenJDK 64-Bit Server VM)
- **Benchmark config:** 3 fork(s), 3 warmup, 5 measurement, 4 threads
- **Hardware:** AMD EPYC 7763 64-Core Processor, 4 cores, 16 GB RAM
- **OS:** Linux 6.17.0-1022-azure

## Results

### CounterBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusInc | 66.46K | ± 636.94 | ops/s | **fastest** |
| prometheusNoLabelsInc | 54.48K | ± 1.71K | ops/s | 1.2x slower |
| prometheusAdd | 51.43K | ± 227.02 | ops/s | 1.3x slower |
| codahaleIncNoLabels | 48.49K | ± 1.37K | ops/s | 1.4x slower |
| simpleclientInc | 6.68K | ± 22.12 | ops/s | 9.9x slower |
| simpleclientNoLabelsInc | 6.49K | ± 193.49 | ops/s | 10x slower |
| simpleclientAdd | 6.06K | ± 373.88 | ops/s | 11x slower |
| openTelemetryAdd | 1.43K | ± 243.04 | ops/s | 46x slower |
| openTelemetryIncNoLabels | 1.34K | ± 52.62 | ops/s | 50x slower |
| openTelemetryInc | 1.24K | ± 77.88 | ops/s | 53x slower |

### HistogramBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| simpleclient | 4.45K | ± 51.18 | ops/s | **fastest** |
| prometheusClassic | 4.41K | ± 451.37 | ops/s | 1.0x slower |
| prometheusNative | 2.98K | ± 343.10 | ops/s | 1.5x slower |
| openTelemetryClassic | 726.84 | ± 31.19 | ops/s | 6.1x slower |
| openTelemetryExponential | 599.78 | ± 39.51 | ops/s | 7.4x slower |

### TextFormatUtilBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusWriteToNull | 498.83K | ± 2.14K | ops/s | **fastest** |
| prometheusWriteToByteArray | 494.96K | ± 1.58K | ops/s | 1.0x slower |
| openMetricsWriteToNull | 492.22K | ± 4.32K | ops/s | 1.0x slower |
| openMetricsWriteToByteArray | 481.61K | ± 7.69K | ops/s | 1.0x slower |

### Raw Results

```
Benchmark                                            Mode  Cnt          Score        Error  Units
CounterBenchmark.codahaleIncNoLabels                thrpt   15      48491.740   ± 1370.182  ops/s
CounterBenchmark.openTelemetryAdd                   thrpt   15       1430.353    ± 243.036  ops/s
CounterBenchmark.openTelemetryInc                   thrpt   15       1244.205     ± 77.879  ops/s
CounterBenchmark.openTelemetryIncNoLabels           thrpt   15       1337.348     ± 52.620  ops/s
CounterBenchmark.prometheusAdd                      thrpt   15      51426.264    ± 227.022  ops/s
CounterBenchmark.prometheusInc                      thrpt   15      66463.977    ± 636.941  ops/s
CounterBenchmark.prometheusNoLabelsInc              thrpt   15      54481.735   ± 1705.241  ops/s
CounterBenchmark.simpleclientAdd                    thrpt   15       6063.089    ± 373.882  ops/s
CounterBenchmark.simpleclientInc                    thrpt   15       6684.676     ± 22.120  ops/s
CounterBenchmark.simpleclientNoLabelsInc            thrpt   15       6487.621    ± 193.493  ops/s
HistogramBenchmark.openTelemetryClassic             thrpt   15        726.837     ± 31.193  ops/s
HistogramBenchmark.openTelemetryExponential         thrpt   15        599.775     ± 39.507  ops/s
HistogramBenchmark.prometheusClassic                thrpt   15       4414.896    ± 451.365  ops/s
HistogramBenchmark.prometheusNative                 thrpt   15       2980.035    ± 343.097  ops/s
HistogramBenchmark.simpleclient                     thrpt   15       4445.338     ± 51.177  ops/s
TextFormatUtilBenchmark.openMetricsWriteToByteArray  thrpt   15     481613.741   ± 7694.074  ops/s
TextFormatUtilBenchmark.openMetricsWriteToNull      thrpt   15     492224.497   ± 4315.639  ops/s
TextFormatUtilBenchmark.prometheusWriteToByteArray  thrpt   15     494959.328   ± 1584.825  ops/s
TextFormatUtilBenchmark.prometheusWriteToNull       thrpt   15     498827.093   ± 2143.462  ops/s
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
