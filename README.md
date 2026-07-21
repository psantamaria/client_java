# Prometheus Java Client Benchmarks

## Run Information

- **Date:** 2026-07-21T06:32:46Z
- **Commit:** [`4b69f40`](https://github.com/psantamaria/client_java/commit/4b69f40bd4e616d69468ce99dc4323162287a577)
- **JDK:** 25.0.2 (OpenJDK 64-Bit Server VM)
- **Benchmark config:** 3 fork(s), 3 warmup, 5 measurement, 4 threads
- **Hardware:** AMD EPYC 9V74 80-Core Processor, 4 cores, 16 GB RAM
- **OS:** Linux 6.17.0-1020-azure

## Results

### CounterBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusInc | 58.68K | ± 2.82K | ops/s | **fastest** |
| prometheusNoLabelsInc | 51.51K | ± 941.95 | ops/s | 1.1x slower |
| prometheusAdd | 48.25K | ± 340.06 | ops/s | 1.2x slower |
| codahaleIncNoLabels | 44.39K | ± 177.83 | ops/s | 1.3x slower |
| simpleclientInc | 6.30K | ± 26.99 | ops/s | 9.3x slower |
| simpleclientNoLabelsInc | 5.99K | ± 225.34 | ops/s | 9.8x slower |
| simpleclientAdd | 5.89K | ± 142.64 | ops/s | 10.0x slower |
| openTelemetryIncNoLabels | 1.38K | ± 158.95 | ops/s | 42x slower |
| openTelemetryAdd | 1.30K | ± 105.26 | ops/s | 45x slower |
| openTelemetryInc | 1.29K | ± 5.72 | ops/s | 45x slower |

### HistogramBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusClassic | 6.31K | ± 1.74K | ops/s | **fastest** |
| simpleclient | 4.38K | ± 79.05 | ops/s | 1.4x slower |
| prometheusNative | 2.98K | ± 276.08 | ops/s | 2.1x slower |
| openTelemetryClassic | 600.78 | ± 20.65 | ops/s | 10x slower |
| openTelemetryExponential | 514.69 | ± 25.38 | ops/s | 12x slower |

### TextFormatUtilBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusWriteToNull | 539.67K | ± 5.44K | ops/s | **fastest** |
| openMetricsWriteToNull | 517.86K | ± 4.38K | ops/s | 1.0x slower |
| prometheusWriteToByteArray | 515.83K | ± 12.38K | ops/s | 1.0x slower |
| openMetricsWriteToByteArray | 506.02K | ± 7.60K | ops/s | 1.1x slower |

### Raw Results

```
Benchmark                                            Mode  Cnt          Score        Error  Units
CounterBenchmark.codahaleIncNoLabels                thrpt   15      44385.863    ± 177.832  ops/s
CounterBenchmark.openTelemetryAdd                   thrpt   15       1301.464    ± 105.264  ops/s
CounterBenchmark.openTelemetryInc                   thrpt   15       1291.520      ± 5.719  ops/s
CounterBenchmark.openTelemetryIncNoLabels           thrpt   15       1383.532    ± 158.949  ops/s
CounterBenchmark.prometheusAdd                      thrpt   15      48254.743    ± 340.059  ops/s
CounterBenchmark.prometheusInc                      thrpt   15      58682.398   ± 2820.379  ops/s
CounterBenchmark.prometheusNoLabelsInc              thrpt   15      51506.806    ± 941.950  ops/s
CounterBenchmark.simpleclientAdd                    thrpt   15       5894.564    ± 142.642  ops/s
CounterBenchmark.simpleclientInc                    thrpt   15       6295.567     ± 26.985  ops/s
CounterBenchmark.simpleclientNoLabelsInc            thrpt   15       5987.449    ± 225.337  ops/s
HistogramBenchmark.openTelemetryClassic             thrpt   15        600.782     ± 20.654  ops/s
HistogramBenchmark.openTelemetryExponential         thrpt   15        514.693     ± 25.379  ops/s
HistogramBenchmark.prometheusClassic                thrpt   15       6308.029   ± 1743.183  ops/s
HistogramBenchmark.prometheusNative                 thrpt   15       2982.881    ± 276.076  ops/s
HistogramBenchmark.simpleclient                     thrpt   15       4377.734     ± 79.046  ops/s
TextFormatUtilBenchmark.openMetricsWriteToByteArray  thrpt   15     506022.869   ± 7597.607  ops/s
TextFormatUtilBenchmark.openMetricsWriteToNull      thrpt   15     517864.205   ± 4376.224  ops/s
TextFormatUtilBenchmark.prometheusWriteToByteArray  thrpt   15     515826.578  ± 12382.749  ops/s
TextFormatUtilBenchmark.prometheusWriteToNull       thrpt   15     539669.293   ± 5438.638  ops/s
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
