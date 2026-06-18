# Prometheus Java Client Benchmarks

## Run Information

- **Date:** 2026-06-18T08:03:48Z
- **Commit:** [`4b69f40`](https://github.com/psantamaria/client_java/commit/4b69f40bd4e616d69468ce99dc4323162287a577)
- **JDK:** 25.0.2 (OpenJDK 64-Bit Server VM)
- **Benchmark config:** 3 fork(s), 3 warmup, 5 measurement, 4 threads
- **Hardware:** AMD EPYC 7763 64-Core Processor, 4 cores, 16 GB RAM
- **OS:** Linux 6.17.0-1018-azure

## Results

### CounterBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusInc | 64.08K | ± 1.80K | ops/s | **fastest** |
| prometheusNoLabelsInc | 56.65K | ± 680.20 | ops/s | 1.1x slower |
| prometheusAdd | 51.08K | ± 624.62 | ops/s | 1.3x slower |
| codahaleIncNoLabels | 43.99K | ± 7.55K | ops/s | 1.5x slower |
| simpleclientInc | 6.55K | ± 162.39 | ops/s | 9.8x slower |
| simpleclientNoLabelsInc | 6.31K | ± 170.99 | ops/s | 10x slower |
| simpleclientAdd | 6.16K | ± 157.52 | ops/s | 10x slower |
| openTelemetryAdd | 1.42K | ± 325.73 | ops/s | 45x slower |
| openTelemetryInc | 1.23K | ± 12.46 | ops/s | 52x slower |
| openTelemetryIncNoLabels | 1.20K | ± 43.41 | ops/s | 53x slower |

### HistogramBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusClassic | 4.58K | ± 964.19 | ops/s | **fastest** |
| simpleclient | 4.42K | ± 63.25 | ops/s | 1.0x slower |
| prometheusNative | 3.12K | ± 141.70 | ops/s | 1.5x slower |
| openTelemetryClassic | 677.39 | ± 53.20 | ops/s | 6.8x slower |
| openTelemetryExponential | 541.04 | ± 10.28 | ops/s | 8.5x slower |

### TextFormatUtilBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusWriteToNull | 489.48K | ± 5.15K | ops/s | **fastest** |
| prometheusWriteToByteArray | 485.19K | ± 4.29K | ops/s | 1.0x slower |
| openMetricsWriteToNull | 480.78K | ± 7.54K | ops/s | 1.0x slower |
| openMetricsWriteToByteArray | 473.41K | ± 6.47K | ops/s | 1.0x slower |

### Raw Results

```
Benchmark                                            Mode  Cnt          Score        Error  Units
CounterBenchmark.codahaleIncNoLabels                thrpt   15      43992.510   ± 7551.145  ops/s
CounterBenchmark.openTelemetryAdd                   thrpt   15       1417.813    ± 325.731  ops/s
CounterBenchmark.openTelemetryInc                   thrpt   15       1231.601     ± 12.461  ops/s
CounterBenchmark.openTelemetryIncNoLabels           thrpt   15       1204.646     ± 43.414  ops/s
CounterBenchmark.prometheusAdd                      thrpt   15      51082.769    ± 624.623  ops/s
CounterBenchmark.prometheusInc                      thrpt   15      64080.493   ± 1796.122  ops/s
CounterBenchmark.prometheusNoLabelsInc              thrpt   15      56654.556    ± 680.203  ops/s
CounterBenchmark.simpleclientAdd                    thrpt   15       6160.867    ± 157.521  ops/s
CounterBenchmark.simpleclientInc                    thrpt   15       6548.051    ± 162.393  ops/s
CounterBenchmark.simpleclientNoLabelsInc            thrpt   15       6308.663    ± 170.990  ops/s
HistogramBenchmark.openTelemetryClassic             thrpt   15        677.392     ± 53.205  ops/s
HistogramBenchmark.openTelemetryExponential         thrpt   15        541.044     ± 10.280  ops/s
HistogramBenchmark.prometheusClassic                thrpt   15       4582.162    ± 964.191  ops/s
HistogramBenchmark.prometheusNative                 thrpt   15       3121.343    ± 141.696  ops/s
HistogramBenchmark.simpleclient                     thrpt   15       4416.489     ± 63.250  ops/s
TextFormatUtilBenchmark.openMetricsWriteToByteArray  thrpt   15     473405.544   ± 6472.732  ops/s
TextFormatUtilBenchmark.openMetricsWriteToNull      thrpt   15     480783.112   ± 7543.903  ops/s
TextFormatUtilBenchmark.prometheusWriteToByteArray  thrpt   15     485194.142   ± 4294.744  ops/s
TextFormatUtilBenchmark.prometheusWriteToNull       thrpt   15     489476.438   ± 5151.192  ops/s
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
