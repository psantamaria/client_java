# Prometheus Java Client Benchmarks

## Run Information

- **Date:** 2026-07-11T06:16:00Z
- **Commit:** [`4b69f40`](https://github.com/psantamaria/client_java/commit/4b69f40bd4e616d69468ce99dc4323162287a577)
- **JDK:** 25.0.2 (OpenJDK 64-Bit Server VM)
- **Benchmark config:** 3 fork(s), 3 warmup, 5 measurement, 4 threads
- **Hardware:** AMD EPYC 7763 64-Core Processor, 4 cores, 16 GB RAM
- **OS:** Linux 6.17.0-1018-azure

## Results

### CounterBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusInc | 65.29K | ± 1.46K | ops/s | **fastest** |
| prometheusAdd | 51.45K | ± 206.16 | ops/s | 1.3x slower |
| prometheusNoLabelsInc | 51.23K | ± 6.27K | ops/s | 1.3x slower |
| codahaleIncNoLabels | 47.05K | ± 219.94 | ops/s | 1.4x slower |
| simpleclientInc | 6.50K | ± 187.97 | ops/s | 10x slower |
| simpleclientNoLabelsInc | 6.43K | ± 140.82 | ops/s | 10x slower |
| simpleclientAdd | 6.12K | ± 285.11 | ops/s | 11x slower |
| openTelemetryAdd | 1.41K | ± 245.85 | ops/s | 46x slower |
| openTelemetryInc | 1.27K | ± 12.92 | ops/s | 51x slower |
| openTelemetryIncNoLabels | 1.21K | ± 17.64 | ops/s | 54x slower |

### HistogramBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusClassic | 5.28K | ± 1.48K | ops/s | **fastest** |
| simpleclient | 4.39K | ± 38.69 | ops/s | 1.2x slower |
| prometheusNative | 2.98K | ± 252.74 | ops/s | 1.8x slower |
| openTelemetryClassic | 667.00 | ± 5.85 | ops/s | 7.9x slower |
| openTelemetryExponential | 580.16 | ± 18.53 | ops/s | 9.1x slower |

### TextFormatUtilBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusWriteToNull | 494.85K | ± 3.42K | ops/s | **fastest** |
| prometheusWriteToByteArray | 489.32K | ± 5.08K | ops/s | 1.0x slower |
| openMetricsWriteToNull | 487.42K | ± 5.09K | ops/s | 1.0x slower |
| openMetricsWriteToByteArray | 482.33K | ± 4.70K | ops/s | 1.0x slower |

### Raw Results

```
Benchmark                                            Mode  Cnt          Score        Error  Units
CounterBenchmark.codahaleIncNoLabels                thrpt   15      47051.167    ± 219.935  ops/s
CounterBenchmark.openTelemetryAdd                   thrpt   15       1412.480    ± 245.851  ops/s
CounterBenchmark.openTelemetryInc                   thrpt   15       1274.527     ± 12.924  ops/s
CounterBenchmark.openTelemetryIncNoLabels           thrpt   15       1212.043     ± 17.636  ops/s
CounterBenchmark.prometheusAdd                      thrpt   15      51446.133    ± 206.163  ops/s
CounterBenchmark.prometheusInc                      thrpt   15      65285.796   ± 1464.177  ops/s
CounterBenchmark.prometheusNoLabelsInc              thrpt   15      51231.096   ± 6272.609  ops/s
CounterBenchmark.simpleclientAdd                    thrpt   15       6118.903    ± 285.114  ops/s
CounterBenchmark.simpleclientInc                    thrpt   15       6497.837    ± 187.966  ops/s
CounterBenchmark.simpleclientNoLabelsInc            thrpt   15       6429.961    ± 140.821  ops/s
HistogramBenchmark.openTelemetryClassic             thrpt   15        666.999      ± 5.851  ops/s
HistogramBenchmark.openTelemetryExponential         thrpt   15        580.157     ± 18.532  ops/s
HistogramBenchmark.prometheusClassic                thrpt   15       5278.120   ± 1484.224  ops/s
HistogramBenchmark.prometheusNative                 thrpt   15       2975.067    ± 252.744  ops/s
HistogramBenchmark.simpleclient                     thrpt   15       4392.277     ± 38.695  ops/s
TextFormatUtilBenchmark.openMetricsWriteToByteArray  thrpt   15     482329.719   ± 4702.971  ops/s
TextFormatUtilBenchmark.openMetricsWriteToNull      thrpt   15     487416.573   ± 5090.550  ops/s
TextFormatUtilBenchmark.prometheusWriteToByteArray  thrpt   15     489322.923   ± 5080.633  ops/s
TextFormatUtilBenchmark.prometheusWriteToNull       thrpt   15     494848.699   ± 3415.789  ops/s
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
