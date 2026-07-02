# Prometheus Java Client Benchmarks

## Run Information

- **Date:** 2026-07-02T07:10:31Z
- **Commit:** [`4b69f40`](https://github.com/psantamaria/client_java/commit/4b69f40bd4e616d69468ce99dc4323162287a577)
- **JDK:** 25.0.2 (OpenJDK 64-Bit Server VM)
- **Benchmark config:** 3 fork(s), 3 warmup, 5 measurement, 4 threads
- **Hardware:** AMD EPYC 7763 64-Core Processor, 4 cores, 16 GB RAM
- **OS:** Linux 6.17.0-1018-azure

## Results

### CounterBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusInc | 65.30K | ± 1.47K | ops/s | **fastest** |
| prometheusNoLabelsInc | 56.01K | ± 1.21K | ops/s | 1.2x slower |
| prometheusAdd | 51.24K | ± 199.06 | ops/s | 1.3x slower |
| codahaleIncNoLabels | 48.65K | ± 2.20K | ops/s | 1.3x slower |
| simpleclientInc | 6.53K | ± 105.95 | ops/s | 10x slower |
| simpleclientNoLabelsInc | 6.49K | ± 191.76 | ops/s | 10x slower |
| simpleclientAdd | 6.44K | ± 40.31 | ops/s | 10x slower |
| openTelemetryIncNoLabels | 1.34K | ± 254.37 | ops/s | 49x slower |
| openTelemetryInc | 1.26K | ± 47.54 | ops/s | 52x slower |
| openTelemetryAdd | 1.24K | ± 19.60 | ops/s | 52x slower |

### HistogramBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusClassic | 5.71K | ± 1.32K | ops/s | **fastest** |
| simpleclient | 4.49K | ± 27.43 | ops/s | 1.3x slower |
| prometheusNative | 3.16K | ± 109.91 | ops/s | 1.8x slower |
| openTelemetryClassic | 663.84 | ± 38.21 | ops/s | 8.6x slower |
| openTelemetryExponential | 563.52 | ± 57.44 | ops/s | 10x slower |

### TextFormatUtilBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusWriteToByteArray | 491.02K | ± 1.57K | ops/s | **fastest** |
| prometheusWriteToNull | 488.53K | ± 7.66K | ops/s | 1.0x slower |
| openMetricsWriteToNull | 483.75K | ± 4.20K | ops/s | 1.0x slower |
| openMetricsWriteToByteArray | 471.96K | ± 3.76K | ops/s | 1.0x slower |

### Raw Results

```
Benchmark                                            Mode  Cnt          Score        Error  Units
CounterBenchmark.codahaleIncNoLabels                thrpt   15      48645.711   ± 2201.481  ops/s
CounterBenchmark.openTelemetryAdd                   thrpt   15       1244.919     ± 19.602  ops/s
CounterBenchmark.openTelemetryInc                   thrpt   15       1255.227     ± 47.537  ops/s
CounterBenchmark.openTelemetryIncNoLabels           thrpt   15       1344.405    ± 254.365  ops/s
CounterBenchmark.prometheusAdd                      thrpt   15      51235.115    ± 199.056  ops/s
CounterBenchmark.prometheusInc                      thrpt   15      65302.635   ± 1468.021  ops/s
CounterBenchmark.prometheusNoLabelsInc              thrpt   15      56008.267   ± 1207.525  ops/s
CounterBenchmark.simpleclientAdd                    thrpt   15       6439.937     ± 40.310  ops/s
CounterBenchmark.simpleclientInc                    thrpt   15       6525.195    ± 105.953  ops/s
CounterBenchmark.simpleclientNoLabelsInc            thrpt   15       6490.620    ± 191.759  ops/s
HistogramBenchmark.openTelemetryClassic             thrpt   15        663.838     ± 38.213  ops/s
HistogramBenchmark.openTelemetryExponential         thrpt   15        563.516     ± 57.441  ops/s
HistogramBenchmark.prometheusClassic                thrpt   15       5711.473   ± 1318.293  ops/s
HistogramBenchmark.prometheusNative                 thrpt   15       3160.609    ± 109.908  ops/s
HistogramBenchmark.simpleclient                     thrpt   15       4485.123     ± 27.430  ops/s
TextFormatUtilBenchmark.openMetricsWriteToByteArray  thrpt   15     471964.548   ± 3757.074  ops/s
TextFormatUtilBenchmark.openMetricsWriteToNull      thrpt   15     483748.088   ± 4200.040  ops/s
TextFormatUtilBenchmark.prometheusWriteToByteArray  thrpt   15     491024.036   ± 1567.475  ops/s
TextFormatUtilBenchmark.prometheusWriteToNull       thrpt   15     488533.535   ± 7664.115  ops/s
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
