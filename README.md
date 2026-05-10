# Prometheus Java Client Benchmarks

## Run Information

- **Date:** 2026-05-10T06:50:05Z
- **Commit:** [`4b69f40`](https://github.com/psantamaria/client_java/commit/4b69f40bd4e616d69468ce99dc4323162287a577)
- **JDK:** 25.0.2 (OpenJDK 64-Bit Server VM)
- **Benchmark config:** 3 fork(s), 3 warmup, 5 measurement, 4 threads
- **Hardware:** Intel(R) Xeon(R) Platinum 8370C CPU @ 2.80GHz, 4 cores, 16 GB RAM
- **OS:** Linux 6.17.0-1010-azure

## Results

### CounterBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusNoLabelsInc | 30.96K | ± 202.97 | ops/s | **fastest** |
| codahaleIncNoLabels | 30.04K | ± 1.47K | ops/s | 1.0x slower |
| prometheusInc | 29.94K | ± 1.22K | ops/s | 1.0x slower |
| prometheusAdd | 28.46K | ± 108.59 | ops/s | 1.1x slower |
| simpleclientNoLabelsInc | 6.73K | ± 81.76 | ops/s | 4.6x slower |
| simpleclientInc | 6.73K | ± 119.02 | ops/s | 4.6x slower |
| simpleclientAdd | 6.40K | ± 76.06 | ops/s | 4.8x slower |
| openTelemetryAdd | 1.33K | ± 23.09 | ops/s | 23x slower |
| openTelemetryIncNoLabels | 1.32K | ± 59.07 | ops/s | 24x slower |
| openTelemetryInc | 1.28K | ± 67.17 | ops/s | 24x slower |

### HistogramBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| simpleclient | 4.38K | ± 60.06 | ops/s | **fastest** |
| prometheusClassic | 3.15K | ± 373.38 | ops/s | 1.4x slower |
| prometheusNative | 2.18K | ± 131.37 | ops/s | 2.0x slower |
| openTelemetryClassic | 469.04 | ± 12.88 | ops/s | 9.3x slower |
| openTelemetryExponential | 418.75 | ± 18.92 | ops/s | 10x slower |

### TextFormatUtilBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusWriteToNull | 294.48K | ± 6.19K | ops/s | **fastest** |
| prometheusWriteToByteArray | 289.39K | ± 4.59K | ops/s | 1.0x slower |
| openMetricsWriteToNull | 281.77K | ± 3.85K | ops/s | 1.0x slower |
| openMetricsWriteToByteArray | 278.14K | ± 3.69K | ops/s | 1.1x slower |

### Raw Results

```
Benchmark                                            Mode  Cnt          Score        Error  Units
CounterBenchmark.codahaleIncNoLabels                thrpt   15      30036.465   ± 1470.218  ops/s
CounterBenchmark.openTelemetryAdd                   thrpt   15       1325.965     ± 23.086  ops/s
CounterBenchmark.openTelemetryInc                   thrpt   15       1281.171     ± 67.168  ops/s
CounterBenchmark.openTelemetryIncNoLabels           thrpt   15       1316.457     ± 59.075  ops/s
CounterBenchmark.prometheusAdd                      thrpt   15      28456.526    ± 108.591  ops/s
CounterBenchmark.prometheusInc                      thrpt   15      29942.771   ± 1221.124  ops/s
CounterBenchmark.prometheusNoLabelsInc              thrpt   15      30957.298    ± 202.968  ops/s
CounterBenchmark.simpleclientAdd                    thrpt   15       6395.843     ± 76.055  ops/s
CounterBenchmark.simpleclientInc                    thrpt   15       6725.706    ± 119.025  ops/s
CounterBenchmark.simpleclientNoLabelsInc            thrpt   15       6733.857     ± 81.761  ops/s
HistogramBenchmark.openTelemetryClassic             thrpt   15        469.038     ± 12.882  ops/s
HistogramBenchmark.openTelemetryExponential         thrpt   15        418.748     ± 18.916  ops/s
HistogramBenchmark.prometheusClassic                thrpt   15       3146.141    ± 373.385  ops/s
HistogramBenchmark.prometheusNative                 thrpt   15       2180.335    ± 131.372  ops/s
HistogramBenchmark.simpleclient                     thrpt   15       4378.773     ± 60.060  ops/s
TextFormatUtilBenchmark.openMetricsWriteToByteArray  thrpt   15     278142.057   ± 3690.477  ops/s
TextFormatUtilBenchmark.openMetricsWriteToNull      thrpt   15     281774.480   ± 3846.637  ops/s
TextFormatUtilBenchmark.prometheusWriteToByteArray  thrpt   15     289394.936   ± 4589.694  ops/s
TextFormatUtilBenchmark.prometheusWriteToNull       thrpt   15     294483.854   ± 6185.427  ops/s
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
