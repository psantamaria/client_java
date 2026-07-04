# Prometheus Java Client Benchmarks

## Run Information

- **Date:** 2026-07-04T06:57:38Z
- **Commit:** [`4b69f40`](https://github.com/psantamaria/client_java/commit/4b69f40bd4e616d69468ce99dc4323162287a577)
- **JDK:** 25.0.2 (OpenJDK 64-Bit Server VM)
- **Benchmark config:** 3 fork(s), 3 warmup, 5 measurement, 4 threads
- **Hardware:** AMD EPYC 7763 64-Core Processor, 4 cores, 16 GB RAM
- **OS:** Linux 6.17.0-1018-azure

## Results

### CounterBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusInc | 66.65K | ± 452.50 | ops/s | **fastest** |
| prometheusNoLabelsInc | 55.97K | ± 1.17K | ops/s | 1.2x slower |
| prometheusAdd | 51.24K | ± 354.51 | ops/s | 1.3x slower |
| codahaleIncNoLabels | 49.79K | ± 542.08 | ops/s | 1.3x slower |
| simpleclientNoLabelsInc | 6.61K | ± 18.59 | ops/s | 10x slower |
| simpleclientInc | 6.58K | ± 169.91 | ops/s | 10x slower |
| simpleclientAdd | 6.19K | ± 235.91 | ops/s | 11x slower |
| openTelemetryAdd | 1.27K | ± 20.95 | ops/s | 52x slower |
| openTelemetryInc | 1.25K | ± 22.57 | ops/s | 53x slower |
| openTelemetryIncNoLabels | 1.23K | ± 33.93 | ops/s | 54x slower |

### HistogramBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusClassic | 6.50K | ± 1.33K | ops/s | **fastest** |
| simpleclient | 4.39K | ± 26.09 | ops/s | 1.5x slower |
| prometheusNative | 2.95K | ± 375.38 | ops/s | 2.2x slower |
| openTelemetryClassic | 679.37 | ± 10.30 | ops/s | 9.6x slower |
| openTelemetryExponential | 565.95 | ± 10.88 | ops/s | 11x slower |

### TextFormatUtilBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusWriteToNull | 488.82K | ± 3.56K | ops/s | **fastest** |
| prometheusWriteToByteArray | 482.44K | ± 4.65K | ops/s | 1.0x slower |
| openMetricsWriteToNull | 474.59K | ± 2.55K | ops/s | 1.0x slower |
| openMetricsWriteToByteArray | 463.98K | ± 5.20K | ops/s | 1.1x slower |

### Raw Results

```
Benchmark                                            Mode  Cnt          Score        Error  Units
CounterBenchmark.codahaleIncNoLabels                thrpt   15      49785.455    ± 542.081  ops/s
CounterBenchmark.openTelemetryAdd                   thrpt   15       1272.143     ± 20.949  ops/s
CounterBenchmark.openTelemetryInc                   thrpt   15       1253.760     ± 22.573  ops/s
CounterBenchmark.openTelemetryIncNoLabels           thrpt   15       1225.332     ± 33.932  ops/s
CounterBenchmark.prometheusAdd                      thrpt   15      51236.605    ± 354.505  ops/s
CounterBenchmark.prometheusInc                      thrpt   15      66652.638    ± 452.504  ops/s
CounterBenchmark.prometheusNoLabelsInc              thrpt   15      55967.153   ± 1170.548  ops/s
CounterBenchmark.simpleclientAdd                    thrpt   15       6185.307    ± 235.910  ops/s
CounterBenchmark.simpleclientInc                    thrpt   15       6579.340    ± 169.913  ops/s
CounterBenchmark.simpleclientNoLabelsInc            thrpt   15       6610.793     ± 18.589  ops/s
HistogramBenchmark.openTelemetryClassic             thrpt   15        679.374     ± 10.298  ops/s
HistogramBenchmark.openTelemetryExponential         thrpt   15        565.946     ± 10.881  ops/s
HistogramBenchmark.prometheusClassic                thrpt   15       6501.446   ± 1331.321  ops/s
HistogramBenchmark.prometheusNative                 thrpt   15       2945.190    ± 375.378  ops/s
HistogramBenchmark.simpleclient                     thrpt   15       4392.224     ± 26.093  ops/s
TextFormatUtilBenchmark.openMetricsWriteToByteArray  thrpt   15     463977.751   ± 5196.063  ops/s
TextFormatUtilBenchmark.openMetricsWriteToNull      thrpt   15     474593.400   ± 2551.022  ops/s
TextFormatUtilBenchmark.prometheusWriteToByteArray  thrpt   15     482441.699   ± 4651.133  ops/s
TextFormatUtilBenchmark.prometheusWriteToNull       thrpt   15     488820.186   ± 3560.898  ops/s
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
