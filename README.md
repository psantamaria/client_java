# Prometheus Java Client Benchmarks

## Run Information

- **Date:** 2026-08-04T06:15:35Z
- **Commit:** [`4b69f40`](https://github.com/psantamaria/client_java/commit/4b69f40bd4e616d69468ce99dc4323162287a577)
- **JDK:** 25.0.2 (OpenJDK 64-Bit Server VM)
- **Benchmark config:** 3 fork(s), 3 warmup, 5 measurement, 4 threads
- **Hardware:** AMD EPYC 9V74 80-Core Processor, 4 cores, 16 GB RAM
- **OS:** Linux 6.17.0-1020-azure

## Results

### CounterBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusInc | 77.23K | ± 96.63 | ops/s | **fastest** |
| prometheusNoLabelsInc | 66.89K | ± 1.02K | ops/s | 1.2x slower |
| prometheusAdd | 61.30K | ± 1.02K | ops/s | 1.3x slower |
| codahaleIncNoLabels | 56.42K | ± 1.77K | ops/s | 1.4x slower |
| simpleclientInc | 8.04K | ± 63.21 | ops/s | 9.6x slower |
| simpleclientNoLabelsInc | 7.90K | ± 336.24 | ops/s | 9.8x slower |
| simpleclientAdd | 7.61K | ± 185.61 | ops/s | 10x slower |
| openTelemetryAdd | 1.97K | ± 268.91 | ops/s | 39x slower |
| openTelemetryInc | 1.87K | ± 119.14 | ops/s | 41x slower |
| openTelemetryIncNoLabels | 1.81K | ± 122.44 | ops/s | 43x slower |

### HistogramBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusClassic | 7.30K | ± 1.72K | ops/s | **fastest** |
| simpleclient | 5.40K | ± 51.79 | ops/s | 1.4x slower |
| prometheusNative | 3.99K | ± 154.85 | ops/s | 1.8x slower |
| openTelemetryClassic | 810.63 | ± 19.43 | ops/s | 9.0x slower |
| openTelemetryExponential | 685.49 | ± 23.29 | ops/s | 11x slower |

### TextFormatUtilBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusWriteToNull | 676.59K | ± 2.45K | ops/s | **fastest** |
| prometheusWriteToByteArray | 657.82K | ± 9.84K | ops/s | 1.0x slower |
| openMetricsWriteToNull | 643.76K | ± 7.22K | ops/s | 1.1x slower |
| openMetricsWriteToByteArray | 633.33K | ± 2.99K | ops/s | 1.1x slower |

### Raw Results

```
Benchmark                                            Mode  Cnt          Score        Error  Units
CounterBenchmark.codahaleIncNoLabels                thrpt   15      56420.461   ± 1767.318  ops/s
CounterBenchmark.openTelemetryAdd                   thrpt   15       1966.434    ± 268.913  ops/s
CounterBenchmark.openTelemetryInc                   thrpt   15       1865.843    ± 119.141  ops/s
CounterBenchmark.openTelemetryIncNoLabels           thrpt   15       1809.454    ± 122.435  ops/s
CounterBenchmark.prometheusAdd                      thrpt   15      61301.064   ± 1020.593  ops/s
CounterBenchmark.prometheusInc                      thrpt   15      77230.367     ± 96.628  ops/s
CounterBenchmark.prometheusNoLabelsInc              thrpt   15      66891.387   ± 1018.179  ops/s
CounterBenchmark.simpleclientAdd                    thrpt   15       7614.848    ± 185.606  ops/s
CounterBenchmark.simpleclientInc                    thrpt   15       8036.649     ± 63.213  ops/s
CounterBenchmark.simpleclientNoLabelsInc            thrpt   15       7904.159    ± 336.242  ops/s
HistogramBenchmark.openTelemetryClassic             thrpt   15        810.626     ± 19.430  ops/s
HistogramBenchmark.openTelemetryExponential         thrpt   15        685.493     ± 23.286  ops/s
HistogramBenchmark.prometheusClassic                thrpt   15       7303.468   ± 1718.359  ops/s
HistogramBenchmark.prometheusNative                 thrpt   15       3992.190    ± 154.851  ops/s
HistogramBenchmark.simpleclient                     thrpt   15       5401.657     ± 51.793  ops/s
TextFormatUtilBenchmark.openMetricsWriteToByteArray  thrpt   15     633331.098   ± 2994.177  ops/s
TextFormatUtilBenchmark.openMetricsWriteToNull      thrpt   15     643762.695   ± 7221.772  ops/s
TextFormatUtilBenchmark.prometheusWriteToByteArray  thrpt   15     657816.544   ± 9836.958  ops/s
TextFormatUtilBenchmark.prometheusWriteToNull       thrpt   15     676591.066   ± 2450.299  ops/s
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
