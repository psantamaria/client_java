# Prometheus Java Client Benchmarks

## Run Information

- **Date:** 2026-07-20T06:50:50Z
- **Commit:** [`4b69f40`](https://github.com/psantamaria/client_java/commit/4b69f40bd4e616d69468ce99dc4323162287a577)
- **JDK:** 25.0.2 (OpenJDK 64-Bit Server VM)
- **Benchmark config:** 3 fork(s), 3 warmup, 5 measurement, 4 threads
- **Hardware:** AMD EPYC 7763 64-Core Processor, 4 cores, 16 GB RAM
- **OS:** Linux 6.17.0-1020-azure

## Results

### CounterBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusNoLabelsInc | 56.55K | ± 1.17K | ops/s | **fastest** |
| prometheusInc | 55.70K | ± 13.14K | ops/s | 1.0x slower |
| prometheusAdd | 50.83K | ± 540.24 | ops/s | 1.1x slower |
| codahaleIncNoLabels | 49.54K | ± 944.63 | ops/s | 1.1x slower |
| simpleclientInc | 6.49K | ± 105.84 | ops/s | 8.7x slower |
| simpleclientNoLabelsInc | 6.35K | ± 191.14 | ops/s | 8.9x slower |
| simpleclientAdd | 6.23K | ± 403.45 | ops/s | 9.1x slower |
| openTelemetryIncNoLabels | 1.34K | ± 136.44 | ops/s | 42x slower |
| openTelemetryInc | 1.33K | ± 179.73 | ops/s | 42x slower |
| openTelemetryAdd | 1.28K | ± 76.05 | ops/s | 44x slower |

### HistogramBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusClassic | 6.23K | ± 1.95K | ops/s | **fastest** |
| simpleclient | 4.36K | ± 49.57 | ops/s | 1.4x slower |
| prometheusNative | 3.18K | ± 28.45 | ops/s | 2.0x slower |
| openTelemetryClassic | 682.92 | ± 39.58 | ops/s | 9.1x slower |
| openTelemetryExponential | 560.93 | ± 32.95 | ops/s | 11x slower |

### TextFormatUtilBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusWriteToNull | 489.39K | ± 3.90K | ops/s | **fastest** |
| prometheusWriteToByteArray | 484.47K | ± 4.79K | ops/s | 1.0x slower |
| openMetricsWriteToNull | 471.39K | ± 4.98K | ops/s | 1.0x slower |
| openMetricsWriteToByteArray | 466.78K | ± 1.85K | ops/s | 1.0x slower |

### Raw Results

```
Benchmark                                            Mode  Cnt          Score        Error  Units
CounterBenchmark.codahaleIncNoLabels                thrpt   15      49540.978    ± 944.628  ops/s
CounterBenchmark.openTelemetryAdd                   thrpt   15       1283.636     ± 76.045  ops/s
CounterBenchmark.openTelemetryInc                   thrpt   15       1331.278    ± 179.732  ops/s
CounterBenchmark.openTelemetryIncNoLabels           thrpt   15       1336.706    ± 136.438  ops/s
CounterBenchmark.prometheusAdd                      thrpt   15      50832.897    ± 540.238  ops/s
CounterBenchmark.prometheusInc                      thrpt   15      55697.810  ± 13139.535  ops/s
CounterBenchmark.prometheusNoLabelsInc              thrpt   15      56553.226   ± 1173.929  ops/s
CounterBenchmark.simpleclientAdd                    thrpt   15       6232.796    ± 403.452  ops/s
CounterBenchmark.simpleclientInc                    thrpt   15       6493.283    ± 105.836  ops/s
CounterBenchmark.simpleclientNoLabelsInc            thrpt   15       6351.007    ± 191.141  ops/s
HistogramBenchmark.openTelemetryClassic             thrpt   15        682.923     ± 39.578  ops/s
HistogramBenchmark.openTelemetryExponential         thrpt   15        560.929     ± 32.948  ops/s
HistogramBenchmark.prometheusClassic                thrpt   15       6228.636   ± 1950.624  ops/s
HistogramBenchmark.prometheusNative                 thrpt   15       3177.185     ± 28.447  ops/s
HistogramBenchmark.simpleclient                     thrpt   15       4362.512     ± 49.574  ops/s
TextFormatUtilBenchmark.openMetricsWriteToByteArray  thrpt   15     466784.021   ± 1846.723  ops/s
TextFormatUtilBenchmark.openMetricsWriteToNull      thrpt   15     471389.826   ± 4984.033  ops/s
TextFormatUtilBenchmark.prometheusWriteToByteArray  thrpt   15     484472.567   ± 4794.331  ops/s
TextFormatUtilBenchmark.prometheusWriteToNull       thrpt   15     489393.342   ± 3900.295  ops/s
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
