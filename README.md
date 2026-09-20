# Prometheus Java Client Benchmarks

## Run Information

- **Date:** 2026-09-20T08:37:46Z
- **Commit:** [`4b69f40`](https://github.com/psantamaria/client_java/commit/4b69f40bd4e616d69468ce99dc4323162287a577)
- **JDK:** 25.0.2 (OpenJDK 64-Bit Server VM)
- **Benchmark config:** 3 fork(s), 3 warmup, 5 measurement, 4 threads
- **Hardware:** AMD EPYC 7763 64-Core Processor, 4 cores, 16 GB RAM
- **OS:** Linux 6.17.0-1022-azure

## Results

### CounterBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusInc | 65.15K | ± 1.92K | ops/s | **fastest** |
| prometheusNoLabelsInc | 56.30K | ± 1.35K | ops/s | 1.2x slower |
| prometheusAdd | 51.46K | ± 157.26 | ops/s | 1.3x slower |
| codahaleIncNoLabels | 49.12K | ± 1.62K | ops/s | 1.3x slower |
| simpleclientInc | 6.54K | ± 128.04 | ops/s | 10.0x slower |
| simpleclientNoLabelsInc | 6.31K | ± 253.25 | ops/s | 10x slower |
| simpleclientAdd | 6.18K | ± 184.55 | ops/s | 11x slower |
| openTelemetryAdd | 1.56K | ± 237.77 | ops/s | 42x slower |
| openTelemetryInc | 1.49K | ± 192.81 | ops/s | 44x slower |
| openTelemetryIncNoLabels | 1.18K | ± 28.64 | ops/s | 55x slower |

### HistogramBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| simpleclient | 4.45K | ± 82.83 | ops/s | **fastest** |
| prometheusClassic | 4.16K | ± 322.96 | ops/s | 1.1x slower |
| prometheusNative | 3.11K | ± 81.70 | ops/s | 1.4x slower |
| openTelemetryClassic | 661.34 | ± 9.34 | ops/s | 6.7x slower |
| openTelemetryExponential | 593.46 | ± 21.95 | ops/s | 7.5x slower |

### TextFormatUtilBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusWriteToNull | 489.73K | ± 1.30K | ops/s | **fastest** |
| prometheusWriteToByteArray | 484.22K | ± 6.69K | ops/s | 1.0x slower |
| openMetricsWriteToNull | 482.58K | ± 2.71K | ops/s | 1.0x slower |
| openMetricsWriteToByteArray | 469.96K | ± 4.04K | ops/s | 1.0x slower |

### Raw Results

```
Benchmark                                            Mode  Cnt          Score        Error  Units
CounterBenchmark.codahaleIncNoLabels                thrpt   15      49117.135   ± 1623.952  ops/s
CounterBenchmark.openTelemetryAdd                   thrpt   15       1557.776    ± 237.771  ops/s
CounterBenchmark.openTelemetryInc                   thrpt   15       1493.612    ± 192.810  ops/s
CounterBenchmark.openTelemetryIncNoLabels           thrpt   15       1182.568     ± 28.640  ops/s
CounterBenchmark.prometheusAdd                      thrpt   15      51458.366    ± 157.256  ops/s
CounterBenchmark.prometheusInc                      thrpt   15      65152.472   ± 1923.311  ops/s
CounterBenchmark.prometheusNoLabelsInc              thrpt   15      56298.129   ± 1350.641  ops/s
CounterBenchmark.simpleclientAdd                    thrpt   15       6178.837    ± 184.550  ops/s
CounterBenchmark.simpleclientInc                    thrpt   15       6538.389    ± 128.044  ops/s
CounterBenchmark.simpleclientNoLabelsInc            thrpt   15       6310.210    ± 253.247  ops/s
HistogramBenchmark.openTelemetryClassic             thrpt   15        661.337      ± 9.339  ops/s
HistogramBenchmark.openTelemetryExponential         thrpt   15        593.459     ± 21.946  ops/s
HistogramBenchmark.prometheusClassic                thrpt   15       4158.870    ± 322.964  ops/s
HistogramBenchmark.prometheusNative                 thrpt   15       3106.043     ± 81.701  ops/s
HistogramBenchmark.simpleclient                     thrpt   15       4448.244     ± 82.834  ops/s
TextFormatUtilBenchmark.openMetricsWriteToByteArray  thrpt   15     469962.784   ± 4043.389  ops/s
TextFormatUtilBenchmark.openMetricsWriteToNull      thrpt   15     482579.654   ± 2709.446  ops/s
TextFormatUtilBenchmark.prometheusWriteToByteArray  thrpt   15     484218.904   ± 6690.886  ops/s
TextFormatUtilBenchmark.prometheusWriteToNull       thrpt   15     489728.580   ± 1298.264  ops/s
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
