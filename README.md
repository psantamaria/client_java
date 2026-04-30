# Prometheus Java Client Benchmarks

## Run Information

- **Date:** 2026-04-30T06:43:13Z
- **Commit:** [`4b69f40`](https://github.com/psantamaria/client_java/commit/4b69f40bd4e616d69468ce99dc4323162287a577)
- **JDK:** 25.0.2 (OpenJDK 64-Bit Server VM)
- **Benchmark config:** 3 fork(s), 3 warmup, 5 measurement, 4 threads
- **Hardware:** AMD EPYC 9V74 80-Core Processor, 4 cores, 16 GB RAM
- **OS:** Linux 6.17.0-1010-azure

## Results

### CounterBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusInc | 78.00K | ± 1.02K | ops/s | **fastest** |
| prometheusNoLabelsInc | 67.34K | ± 567.37 | ops/s | 1.2x slower |
| prometheusAdd | 62.30K | ± 310.90 | ops/s | 1.3x slower |
| codahaleIncNoLabels | 57.42K | ± 968.47 | ops/s | 1.4x slower |
| simpleclientNoLabelsInc | 8.08K | ± 34.98 | ops/s | 9.6x slower |
| simpleclientInc | 8.00K | ± 189.76 | ops/s | 9.8x slower |
| simpleclientAdd | 7.44K | ± 127.12 | ops/s | 10x slower |
| openTelemetryIncNoLabels | 1.67K | ± 60.19 | ops/s | 47x slower |
| openTelemetryAdd | 1.61K | ± 17.14 | ops/s | 48x slower |
| openTelemetryInc | 1.61K | ± 47.33 | ops/s | 49x slower |

### HistogramBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusClassic | 7.57K | ± 1.45K | ops/s | **fastest** |
| simpleclient | 5.63K | ± 216.73 | ops/s | 1.3x slower |
| prometheusNative | 3.86K | ± 380.16 | ops/s | 2.0x slower |
| openTelemetryClassic | 760.15 | ± 18.66 | ops/s | 10.0x slower |
| openTelemetryExponential | 632.98 | ± 22.50 | ops/s | 12x slower |

### TextFormatUtilBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusWriteToNull | 673.28K | ± 2.52K | ops/s | **fastest** |
| prometheusWriteToByteArray | 662.10K | ± 3.26K | ops/s | 1.0x slower |
| openMetricsWriteToNull | 648.03K | ± 7.47K | ops/s | 1.0x slower |
| openMetricsWriteToByteArray | 636.29K | ± 8.73K | ops/s | 1.1x slower |

### Raw Results

```
Benchmark                                            Mode  Cnt          Score        Error  Units
CounterBenchmark.codahaleIncNoLabels                thrpt   15      57416.584    ± 968.466  ops/s
CounterBenchmark.openTelemetryAdd                   thrpt   15       1609.907     ± 17.138  ops/s
CounterBenchmark.openTelemetryInc                   thrpt   15       1605.912     ± 47.326  ops/s
CounterBenchmark.openTelemetryIncNoLabels           thrpt   15       1670.730     ± 60.192  ops/s
CounterBenchmark.prometheusAdd                      thrpt   15      62303.561    ± 310.900  ops/s
CounterBenchmark.prometheusInc                      thrpt   15      78003.346   ± 1020.078  ops/s
CounterBenchmark.prometheusNoLabelsInc              thrpt   15      67341.693    ± 567.374  ops/s
CounterBenchmark.simpleclientAdd                    thrpt   15       7436.327    ± 127.116  ops/s
CounterBenchmark.simpleclientInc                    thrpt   15       7999.812    ± 189.761  ops/s
CounterBenchmark.simpleclientNoLabelsInc            thrpt   15       8084.043     ± 34.980  ops/s
HistogramBenchmark.openTelemetryClassic             thrpt   15        760.149     ± 18.664  ops/s
HistogramBenchmark.openTelemetryExponential         thrpt   15        632.980     ± 22.504  ops/s
HistogramBenchmark.prometheusClassic                thrpt   15       7566.214   ± 1445.786  ops/s
HistogramBenchmark.prometheusNative                 thrpt   15       3857.743    ± 380.163  ops/s
HistogramBenchmark.simpleclient                     thrpt   15       5634.905    ± 216.734  ops/s
TextFormatUtilBenchmark.openMetricsWriteToByteArray  thrpt   15     636294.045   ± 8730.729  ops/s
TextFormatUtilBenchmark.openMetricsWriteToNull      thrpt   15     648034.246   ± 7466.965  ops/s
TextFormatUtilBenchmark.prometheusWriteToByteArray  thrpt   15     662099.332   ± 3261.901  ops/s
TextFormatUtilBenchmark.prometheusWriteToNull       thrpt   15     673283.447   ± 2521.769  ops/s
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
