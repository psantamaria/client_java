# Prometheus Java Client Benchmarks

## Run Information

- **Date:** 2026-09-25T08:16:14Z
- **Commit:** [`4b69f40`](https://github.com/psantamaria/client_java/commit/4b69f40bd4e616d69468ce99dc4323162287a577)
- **JDK:** 25.0.2 (OpenJDK 64-Bit Server VM)
- **Benchmark config:** 3 fork(s), 3 warmup, 5 measurement, 4 threads
- **Hardware:** AMD EPYC 7763 64-Core Processor, 4 cores, 16 GB RAM
- **OS:** Linux 6.17.0-1022-azure

## Results

### CounterBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusInc | 66.80K | ± 381.50 | ops/s | **fastest** |
| prometheusNoLabelsInc | 57.03K | ± 106.22 | ops/s | 1.2x slower |
| prometheusAdd | 51.28K | ± 305.64 | ops/s | 1.3x slower |
| codahaleIncNoLabels | 49.22K | ± 1.61K | ops/s | 1.4x slower |
| simpleclientInc | 6.65K | ± 54.58 | ops/s | 10x slower |
| simpleclientNoLabelsInc | 6.51K | ± 139.39 | ops/s | 10x slower |
| simpleclientAdd | 6.25K | ± 346.69 | ops/s | 11x slower |
| openTelemetryIncNoLabels | 1.36K | ± 185.38 | ops/s | 49x slower |
| openTelemetryInc | 1.26K | ± 17.84 | ops/s | 53x slower |
| openTelemetryAdd | 1.25K | ± 53.52 | ops/s | 53x slower |

### HistogramBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusClassic | 6.43K | ± 1.13K | ops/s | **fastest** |
| simpleclient | 4.45K | ± 60.67 | ops/s | 1.4x slower |
| prometheusNative | 3.10K | ± 339.27 | ops/s | 2.1x slower |
| openTelemetryClassic | 662.23 | ± 11.72 | ops/s | 9.7x slower |
| openTelemetryExponential | 546.95 | ± 33.30 | ops/s | 12x slower |

### TextFormatUtilBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusWriteToNull | 489.44K | ± 5.94K | ops/s | **fastest** |
| prometheusWriteToByteArray | 485.23K | ± 3.87K | ops/s | 1.0x slower |
| openMetricsWriteToNull | 483.61K | ± 5.81K | ops/s | 1.0x slower |
| openMetricsWriteToByteArray | 476.74K | ± 4.37K | ops/s | 1.0x slower |

### Raw Results

```
Benchmark                                            Mode  Cnt          Score        Error  Units
CounterBenchmark.codahaleIncNoLabels                thrpt   15      49222.147   ± 1614.242  ops/s
CounterBenchmark.openTelemetryAdd                   thrpt   15       1254.396     ± 53.520  ops/s
CounterBenchmark.openTelemetryInc                   thrpt   15       1260.418     ± 17.836  ops/s
CounterBenchmark.openTelemetryIncNoLabels           thrpt   15       1361.556    ± 185.380  ops/s
CounterBenchmark.prometheusAdd                      thrpt   15      51282.135    ± 305.643  ops/s
CounterBenchmark.prometheusInc                      thrpt   15      66803.314    ± 381.503  ops/s
CounterBenchmark.prometheusNoLabelsInc              thrpt   15      57030.690    ± 106.223  ops/s
CounterBenchmark.simpleclientAdd                    thrpt   15       6248.174    ± 346.692  ops/s
CounterBenchmark.simpleclientInc                    thrpt   15       6652.396     ± 54.585  ops/s
CounterBenchmark.simpleclientNoLabelsInc            thrpt   15       6513.651    ± 139.389  ops/s
HistogramBenchmark.openTelemetryClassic             thrpt   15        662.233     ± 11.722  ops/s
HistogramBenchmark.openTelemetryExponential         thrpt   15        546.949     ± 33.299  ops/s
HistogramBenchmark.prometheusClassic                thrpt   15       6429.300   ± 1131.330  ops/s
HistogramBenchmark.prometheusNative                 thrpt   15       3097.891    ± 339.268  ops/s
HistogramBenchmark.simpleclient                     thrpt   15       4453.695     ± 60.669  ops/s
TextFormatUtilBenchmark.openMetricsWriteToByteArray  thrpt   15     476737.796   ± 4372.779  ops/s
TextFormatUtilBenchmark.openMetricsWriteToNull      thrpt   15     483610.584   ± 5810.379  ops/s
TextFormatUtilBenchmark.prometheusWriteToByteArray  thrpt   15     485231.670   ± 3873.242  ops/s
TextFormatUtilBenchmark.prometheusWriteToNull       thrpt   15     489439.505   ± 5939.676  ops/s
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
