# Prometheus Java Client Benchmarks

## Run Information

- **Date:** 2026-08-18T04:07:20Z
- **Commit:** [`4b69f40`](https://github.com/psantamaria/client_java/commit/4b69f40bd4e616d69468ce99dc4323162287a577)
- **JDK:** 25.0.2 (OpenJDK 64-Bit Server VM)
- **Benchmark config:** 3 fork(s), 3 warmup, 5 measurement, 4 threads
- **Hardware:** AMD EPYC 7763 64-Core Processor, 4 cores, 16 GB RAM
- **OS:** Linux 6.17.0-1022-azure

## Results

### CounterBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusInc | 65.23K | ± 1.28K | ops/s | **fastest** |
| prometheusNoLabelsInc | 56.73K | ± 361.83 | ops/s | 1.1x slower |
| prometheusAdd | 51.03K | ± 342.84 | ops/s | 1.3x slower |
| codahaleIncNoLabels | 47.44K | ± 753.55 | ops/s | 1.4x slower |
| simpleclientInc | 6.67K | ± 58.11 | ops/s | 9.8x slower |
| simpleclientNoLabelsInc | 6.47K | ± 223.35 | ops/s | 10x slower |
| simpleclientAdd | 6.22K | ± 401.94 | ops/s | 10x slower |
| openTelemetryIncNoLabels | 1.39K | ± 145.86 | ops/s | 47x slower |
| openTelemetryAdd | 1.26K | ± 53.02 | ops/s | 52x slower |
| openTelemetryInc | 1.24K | ± 37.82 | ops/s | 53x slower |

### HistogramBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusClassic | 5.06K | ± 1.00K | ops/s | **fastest** |
| simpleclient | 4.43K | ± 47.52 | ops/s | 1.1x slower |
| prometheusNative | 3.12K | ± 72.65 | ops/s | 1.6x slower |
| openTelemetryClassic | 685.51 | ± 21.77 | ops/s | 7.4x slower |
| openTelemetryExponential | 560.57 | ± 12.20 | ops/s | 9.0x slower |

### TextFormatUtilBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusWriteToNull | 484.88K | ± 3.79K | ops/s | **fastest** |
| prometheusWriteToByteArray | 482.08K | ± 2.41K | ops/s | 1.0x slower |
| openMetricsWriteToNull | 469.21K | ± 5.06K | ops/s | 1.0x slower |
| openMetricsWriteToByteArray | 464.67K | ± 1.53K | ops/s | 1.0x slower |

### Raw Results

```
Benchmark                                            Mode  Cnt          Score        Error  Units
CounterBenchmark.codahaleIncNoLabels                thrpt   15      47439.663    ± 753.547  ops/s
CounterBenchmark.openTelemetryAdd                   thrpt   15       1258.676     ± 53.019  ops/s
CounterBenchmark.openTelemetryInc                   thrpt   15       1235.067     ± 37.822  ops/s
CounterBenchmark.openTelemetryIncNoLabels           thrpt   15       1389.398    ± 145.863  ops/s
CounterBenchmark.prometheusAdd                      thrpt   15      51031.719    ± 342.837  ops/s
CounterBenchmark.prometheusInc                      thrpt   15      65230.187   ± 1281.073  ops/s
CounterBenchmark.prometheusNoLabelsInc              thrpt   15      56734.603    ± 361.830  ops/s
CounterBenchmark.simpleclientAdd                    thrpt   15       6218.684    ± 401.938  ops/s
CounterBenchmark.simpleclientInc                    thrpt   15       6667.036     ± 58.107  ops/s
CounterBenchmark.simpleclientNoLabelsInc            thrpt   15       6465.608    ± 223.346  ops/s
HistogramBenchmark.openTelemetryClassic             thrpt   15        685.509     ± 21.773  ops/s
HistogramBenchmark.openTelemetryExponential         thrpt   15        560.567     ± 12.196  ops/s
HistogramBenchmark.prometheusClassic                thrpt   15       5064.940   ± 1003.366  ops/s
HistogramBenchmark.prometheusNative                 thrpt   15       3121.227     ± 72.655  ops/s
HistogramBenchmark.simpleclient                     thrpt   15       4430.886     ± 47.524  ops/s
TextFormatUtilBenchmark.openMetricsWriteToByteArray  thrpt   15     464670.258   ± 1530.393  ops/s
TextFormatUtilBenchmark.openMetricsWriteToNull      thrpt   15     469211.204   ± 5061.611  ops/s
TextFormatUtilBenchmark.prometheusWriteToByteArray  thrpt   15     482080.407   ± 2412.728  ops/s
TextFormatUtilBenchmark.prometheusWriteToNull       thrpt   15     484880.256   ± 3792.831  ops/s
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
