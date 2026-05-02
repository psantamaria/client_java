# Prometheus Java Client Benchmarks

## Run Information

- **Date:** 2026-05-02T06:12:29Z
- **Commit:** [`4b69f40`](https://github.com/psantamaria/client_java/commit/4b69f40bd4e616d69468ce99dc4323162287a577)
- **JDK:** 25.0.2 (OpenJDK 64-Bit Server VM)
- **Benchmark config:** 3 fork(s), 3 warmup, 5 measurement, 4 threads
- **Hardware:** AMD EPYC 9V74 80-Core Processor, 4 cores, 16 GB RAM
- **OS:** Linux 6.17.0-1010-azure

## Results

### CounterBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusInc | 59.99K | ± 1.11K | ops/s | **fastest** |
| prometheusNoLabelsInc | 51.72K | ± 56.78 | ops/s | 1.2x slower |
| prometheusAdd | 48.03K | ± 408.76 | ops/s | 1.2x slower |
| codahaleIncNoLabels | 44.03K | ± 140.14 | ops/s | 1.4x slower |
| simpleclientNoLabelsInc | 6.04K | ± 225.51 | ops/s | 9.9x slower |
| simpleclientInc | 5.96K | ± 435.28 | ops/s | 10x slower |
| simpleclientAdd | 5.71K | ± 232.69 | ops/s | 11x slower |
| openTelemetryAdd | 1.44K | ± 66.01 | ops/s | 42x slower |
| openTelemetryInc | 1.36K | ± 44.60 | ops/s | 44x slower |
| openTelemetryIncNoLabels | 1.31K | ± 89.43 | ops/s | 46x slower |

### HistogramBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusClassic | 6.54K | ± 1.25K | ops/s | **fastest** |
| simpleclient | 4.49K | ± 94.33 | ops/s | 1.5x slower |
| prometheusNative | 3.01K | ± 354.67 | ops/s | 2.2x slower |
| openTelemetryClassic | 605.37 | ± 19.25 | ops/s | 11x slower |
| openTelemetryExponential | 543.18 | ± 20.46 | ops/s | 12x slower |

### TextFormatUtilBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusWriteToByteArray | 556.56K | ± 4.33K | ops/s | **fastest** |
| prometheusWriteToNull | 554.32K | ± 6.18K | ops/s | 1.0x slower |
| openMetricsWriteToNull | 538.57K | ± 8.51K | ops/s | 1.0x slower |
| openMetricsWriteToByteArray | 529.78K | ± 983.80 | ops/s | 1.1x slower |

### Raw Results

```
Benchmark                                            Mode  Cnt          Score        Error  Units
CounterBenchmark.codahaleIncNoLabels                thrpt   15      44025.058    ± 140.143  ops/s
CounterBenchmark.openTelemetryAdd                   thrpt   15       1441.854     ± 66.008  ops/s
CounterBenchmark.openTelemetryInc                   thrpt   15       1364.563     ± 44.600  ops/s
CounterBenchmark.openTelemetryIncNoLabels           thrpt   15       1314.441     ± 89.429  ops/s
CounterBenchmark.prometheusAdd                      thrpt   15      48030.764    ± 408.757  ops/s
CounterBenchmark.prometheusInc                      thrpt   15      59993.922   ± 1112.299  ops/s
CounterBenchmark.prometheusNoLabelsInc              thrpt   15      51715.600     ± 56.776  ops/s
CounterBenchmark.simpleclientAdd                    thrpt   15       5705.374    ± 232.691  ops/s
CounterBenchmark.simpleclientInc                    thrpt   15       5957.262    ± 435.285  ops/s
CounterBenchmark.simpleclientNoLabelsInc            thrpt   15       6039.486    ± 225.513  ops/s
HistogramBenchmark.openTelemetryClassic             thrpt   15        605.371     ± 19.247  ops/s
HistogramBenchmark.openTelemetryExponential         thrpt   15        543.178     ± 20.458  ops/s
HistogramBenchmark.prometheusClassic                thrpt   15       6544.988   ± 1248.808  ops/s
HistogramBenchmark.prometheusNative                 thrpt   15       3007.950    ± 354.672  ops/s
HistogramBenchmark.simpleclient                     thrpt   15       4487.772     ± 94.327  ops/s
TextFormatUtilBenchmark.openMetricsWriteToByteArray  thrpt   15     529779.646    ± 983.800  ops/s
TextFormatUtilBenchmark.openMetricsWriteToNull      thrpt   15     538572.915   ± 8511.345  ops/s
TextFormatUtilBenchmark.prometheusWriteToByteArray  thrpt   15     556562.087   ± 4334.107  ops/s
TextFormatUtilBenchmark.prometheusWriteToNull       thrpt   15     554320.470   ± 6182.683  ops/s
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
