# Prometheus Java Client Benchmarks

## Run Information

- **Date:** 2026-08-02T06:38:19Z
- **Commit:** [`4b69f40`](https://github.com/psantamaria/client_java/commit/4b69f40bd4e616d69468ce99dc4323162287a577)
- **JDK:** 25.0.2 (OpenJDK 64-Bit Server VM)
- **Benchmark config:** 3 fork(s), 3 warmup, 5 measurement, 4 threads
- **Hardware:** AMD EPYC 9V74 80-Core Processor, 4 cores, 16 GB RAM
- **OS:** Linux 6.17.0-1020-azure

## Results

### CounterBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusInc | 59.99K | ± 1.04K | ops/s | **fastest** |
| prometheusNoLabelsInc | 51.02K | ± 1.23K | ops/s | 1.2x slower |
| prometheusAdd | 48.65K | ± 907.79 | ops/s | 1.2x slower |
| codahaleIncNoLabels | 40.46K | ± 5.63K | ops/s | 1.5x slower |
| simpleclientInc | 6.25K | ± 101.42 | ops/s | 9.6x slower |
| simpleclientNoLabelsInc | 6.13K | ± 184.55 | ops/s | 9.8x slower |
| simpleclientAdd | 5.98K | ± 127.05 | ops/s | 10x slower |
| openTelemetryInc | 1.46K | ± 85.34 | ops/s | 41x slower |
| openTelemetryAdd | 1.39K | ± 83.14 | ops/s | 43x slower |
| openTelemetryIncNoLabels | 1.32K | ± 49.55 | ops/s | 45x slower |

### HistogramBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusClassic | 4.81K | ± 882.85 | ops/s | **fastest** |
| simpleclient | 4.54K | ± 57.46 | ops/s | 1.1x slower |
| prometheusNative | 3.05K | ± 255.77 | ops/s | 1.6x slower |
| openTelemetryClassic | 609.84 | ± 11.38 | ops/s | 7.9x slower |
| openTelemetryExponential | 511.59 | ± 23.32 | ops/s | 9.4x slower |

### TextFormatUtilBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusWriteToNull | 555.82K | ± 2.82K | ops/s | **fastest** |
| prometheusWriteToByteArray | 538.75K | ± 5.49K | ops/s | 1.0x slower |
| openMetricsWriteToNull | 536.09K | ± 3.94K | ops/s | 1.0x slower |
| openMetricsWriteToByteArray | 530.53K | ± 7.42K | ops/s | 1.0x slower |

### Raw Results

```
Benchmark                                            Mode  Cnt          Score        Error  Units
CounterBenchmark.codahaleIncNoLabels                thrpt   15      40459.441   ± 5634.887  ops/s
CounterBenchmark.openTelemetryAdd                   thrpt   15       1392.970     ± 83.144  ops/s
CounterBenchmark.openTelemetryInc                   thrpt   15       1458.226     ± 85.341  ops/s
CounterBenchmark.openTelemetryIncNoLabels           thrpt   15       1322.944     ± 49.553  ops/s
CounterBenchmark.prometheusAdd                      thrpt   15      48650.368    ± 907.790  ops/s
CounterBenchmark.prometheusInc                      thrpt   15      59991.779   ± 1042.126  ops/s
CounterBenchmark.prometheusNoLabelsInc              thrpt   15      51017.596   ± 1230.960  ops/s
CounterBenchmark.simpleclientAdd                    thrpt   15       5984.268    ± 127.053  ops/s
CounterBenchmark.simpleclientInc                    thrpt   15       6245.630    ± 101.422  ops/s
CounterBenchmark.simpleclientNoLabelsInc            thrpt   15       6127.216    ± 184.547  ops/s
HistogramBenchmark.openTelemetryClassic             thrpt   15        609.836     ± 11.379  ops/s
HistogramBenchmark.openTelemetryExponential         thrpt   15        511.585     ± 23.324  ops/s
HistogramBenchmark.prometheusClassic                thrpt   15       4805.430    ± 882.855  ops/s
HistogramBenchmark.prometheusNative                 thrpt   15       3045.525    ± 255.767  ops/s
HistogramBenchmark.simpleclient                     thrpt   15       4542.023     ± 57.462  ops/s
TextFormatUtilBenchmark.openMetricsWriteToByteArray  thrpt   15     530534.858   ± 7416.780  ops/s
TextFormatUtilBenchmark.openMetricsWriteToNull      thrpt   15     536091.829   ± 3944.640  ops/s
TextFormatUtilBenchmark.prometheusWriteToByteArray  thrpt   15     538752.186   ± 5486.679  ops/s
TextFormatUtilBenchmark.prometheusWriteToNull       thrpt   15     555823.564   ± 2815.828  ops/s
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
