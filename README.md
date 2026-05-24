# Prometheus Java Client Benchmarks

## Run Information

- **Date:** 2026-05-24T07:13:49Z
- **Commit:** [`4b69f40`](https://github.com/psantamaria/client_java/commit/4b69f40bd4e616d69468ce99dc4323162287a577)
- **JDK:** 25.0.2 (OpenJDK 64-Bit Server VM)
- **Benchmark config:** 3 fork(s), 3 warmup, 5 measurement, 4 threads
- **Hardware:** AMD EPYC 7763 64-Core Processor, 4 cores, 16 GB RAM
- **OS:** Linux 6.17.0-1013-azure

## Results

### CounterBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusInc | 65.27K | ± 1.21K | ops/s | **fastest** |
| prometheusNoLabelsInc | 57.08K | ± 222.90 | ops/s | 1.1x slower |
| prometheusAdd | 51.55K | ± 193.66 | ops/s | 1.3x slower |
| codahaleIncNoLabels | 49.34K | ± 1.59K | ops/s | 1.3x slower |
| simpleclientInc | 6.69K | ± 17.24 | ops/s | 9.8x slower |
| simpleclientNoLabelsInc | 6.48K | ± 202.22 | ops/s | 10x slower |
| simpleclientAdd | 6.32K | ± 222.50 | ops/s | 10x slower |
| openTelemetryAdd | 1.44K | ± 263.59 | ops/s | 45x slower |
| openTelemetryIncNoLabels | 1.28K | ± 187.73 | ops/s | 51x slower |
| openTelemetryInc | 1.26K | ± 48.32 | ops/s | 52x slower |

### HistogramBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusClassic | 4.88K | ± 662.18 | ops/s | **fastest** |
| simpleclient | 4.48K | ± 28.60 | ops/s | 1.1x slower |
| prometheusNative | 2.85K | ± 306.84 | ops/s | 1.7x slower |
| openTelemetryClassic | 700.53 | ± 41.45 | ops/s | 7.0x slower |
| openTelemetryExponential | 567.28 | ± 17.61 | ops/s | 8.6x slower |

### TextFormatUtilBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusWriteToNull | 491.52K | ± 1.43K | ops/s | **fastest** |
| prometheusWriteToByteArray | 487.64K | ± 3.87K | ops/s | 1.0x slower |
| openMetricsWriteToNull | 487.28K | ± 2.27K | ops/s | 1.0x slower |
| openMetricsWriteToByteArray | 472.22K | ± 4.65K | ops/s | 1.0x slower |

### Raw Results

```
Benchmark                                            Mode  Cnt          Score        Error  Units
CounterBenchmark.codahaleIncNoLabels                thrpt   15      49343.924   ± 1586.844  ops/s
CounterBenchmark.openTelemetryAdd                   thrpt   15       1444.696    ± 263.586  ops/s
CounterBenchmark.openTelemetryInc                   thrpt   15       1257.390     ± 48.316  ops/s
CounterBenchmark.openTelemetryIncNoLabels           thrpt   15       1275.434    ± 187.728  ops/s
CounterBenchmark.prometheusAdd                      thrpt   15      51548.825    ± 193.657  ops/s
CounterBenchmark.prometheusInc                      thrpt   15      65269.095   ± 1214.694  ops/s
CounterBenchmark.prometheusNoLabelsInc              thrpt   15      57080.855    ± 222.899  ops/s
CounterBenchmark.simpleclientAdd                    thrpt   15       6315.499    ± 222.504  ops/s
CounterBenchmark.simpleclientInc                    thrpt   15       6690.339     ± 17.244  ops/s
CounterBenchmark.simpleclientNoLabelsInc            thrpt   15       6482.948    ± 202.216  ops/s
HistogramBenchmark.openTelemetryClassic             thrpt   15        700.532     ± 41.448  ops/s
HistogramBenchmark.openTelemetryExponential         thrpt   15        567.280     ± 17.606  ops/s
HistogramBenchmark.prometheusClassic                thrpt   15       4881.199    ± 662.182  ops/s
HistogramBenchmark.prometheusNative                 thrpt   15       2851.309    ± 306.839  ops/s
HistogramBenchmark.simpleclient                     thrpt   15       4476.396     ± 28.604  ops/s
TextFormatUtilBenchmark.openMetricsWriteToByteArray  thrpt   15     472219.486   ± 4654.074  ops/s
TextFormatUtilBenchmark.openMetricsWriteToNull      thrpt   15     487281.795   ± 2265.394  ops/s
TextFormatUtilBenchmark.prometheusWriteToByteArray  thrpt   15     487641.235   ± 3870.253  ops/s
TextFormatUtilBenchmark.prometheusWriteToNull       thrpt   15     491521.478   ± 1431.865  ops/s
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
