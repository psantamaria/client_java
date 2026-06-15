# Prometheus Java Client Benchmarks

## Run Information

- **Date:** 2026-06-15T08:29:32Z
- **Commit:** [`4b69f40`](https://github.com/psantamaria/client_java/commit/4b69f40bd4e616d69468ce99dc4323162287a577)
- **JDK:** 25.0.2 (OpenJDK 64-Bit Server VM)
- **Benchmark config:** 3 fork(s), 3 warmup, 5 measurement, 4 threads
- **Hardware:** AMD EPYC 7763 64-Core Processor, 4 cores, 16 GB RAM
- **OS:** Linux 6.17.0-1018-azure

## Results

### CounterBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusInc | 65.71K | ± 1.77K | ops/s | **fastest** |
| prometheusNoLabelsInc | 56.85K | ± 402.24 | ops/s | 1.2x slower |
| prometheusAdd | 51.06K | ± 551.94 | ops/s | 1.3x slower |
| codahaleIncNoLabels | 47.97K | ± 1.79K | ops/s | 1.4x slower |
| simpleclientInc | 6.49K | ± 174.58 | ops/s | 10x slower |
| simpleclientAdd | 6.46K | ± 15.86 | ops/s | 10x slower |
| simpleclientNoLabelsInc | 6.40K | ± 157.33 | ops/s | 10x slower |
| openTelemetryAdd | 1.44K | ± 324.55 | ops/s | 46x slower |
| openTelemetryInc | 1.25K | ± 5.33 | ops/s | 53x slower |
| openTelemetryIncNoLabels | 1.24K | ± 12.77 | ops/s | 53x slower |

### HistogramBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusClassic | 5.62K | ± 1.15K | ops/s | **fastest** |
| simpleclient | 4.39K | ± 28.30 | ops/s | 1.3x slower |
| prometheusNative | 3.01K | ± 377.39 | ops/s | 1.9x slower |
| openTelemetryClassic | 719.44 | ± 50.81 | ops/s | 7.8x slower |
| openTelemetryExponential | 560.67 | ± 16.54 | ops/s | 10x slower |

### TextFormatUtilBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusWriteToNull | 486.68K | ± 3.95K | ops/s | **fastest** |
| prometheusWriteToByteArray | 483.39K | ± 3.43K | ops/s | 1.0x slower |
| openMetricsWriteToNull | 481.08K | ± 5.26K | ops/s | 1.0x slower |
| openMetricsWriteToByteArray | 475.12K | ± 4.19K | ops/s | 1.0x slower |

### Raw Results

```
Benchmark                                            Mode  Cnt          Score        Error  Units
CounterBenchmark.codahaleIncNoLabels                thrpt   15      47968.288   ± 1789.242  ops/s
CounterBenchmark.openTelemetryAdd                   thrpt   15       1441.189    ± 324.551  ops/s
CounterBenchmark.openTelemetryInc                   thrpt   15       1246.732      ± 5.328  ops/s
CounterBenchmark.openTelemetryIncNoLabels           thrpt   15       1237.939     ± 12.768  ops/s
CounterBenchmark.prometheusAdd                      thrpt   15      51064.537    ± 551.935  ops/s
CounterBenchmark.prometheusInc                      thrpt   15      65709.283   ± 1772.764  ops/s
CounterBenchmark.prometheusNoLabelsInc              thrpt   15      56854.051    ± 402.243  ops/s
CounterBenchmark.simpleclientAdd                    thrpt   15       6460.983     ± 15.855  ops/s
CounterBenchmark.simpleclientInc                    thrpt   15       6493.678    ± 174.582  ops/s
CounterBenchmark.simpleclientNoLabelsInc            thrpt   15       6404.284    ± 157.333  ops/s
HistogramBenchmark.openTelemetryClassic             thrpt   15        719.440     ± 50.807  ops/s
HistogramBenchmark.openTelemetryExponential         thrpt   15        560.675     ± 16.537  ops/s
HistogramBenchmark.prometheusClassic                thrpt   15       5617.803   ± 1145.289  ops/s
HistogramBenchmark.prometheusNative                 thrpt   15       3007.806    ± 377.386  ops/s
HistogramBenchmark.simpleclient                     thrpt   15       4390.968     ± 28.303  ops/s
TextFormatUtilBenchmark.openMetricsWriteToByteArray  thrpt   15     475117.917   ± 4191.160  ops/s
TextFormatUtilBenchmark.openMetricsWriteToNull      thrpt   15     481075.855   ± 5261.261  ops/s
TextFormatUtilBenchmark.prometheusWriteToByteArray  thrpt   15     483387.374   ± 3427.349  ops/s
TextFormatUtilBenchmark.prometheusWriteToNull       thrpt   15     486678.968   ± 3948.640  ops/s
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
