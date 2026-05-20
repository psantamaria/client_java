# Prometheus Java Client Benchmarks

## Run Information

- **Date:** 2026-05-20T07:19:09Z
- **Commit:** [`4b69f40`](https://github.com/psantamaria/client_java/commit/4b69f40bd4e616d69468ce99dc4323162287a577)
- **JDK:** 25.0.2 (OpenJDK 64-Bit Server VM)
- **Benchmark config:** 3 fork(s), 3 warmup, 5 measurement, 4 threads
- **Hardware:** AMD EPYC 9V74 80-Core Processor, 4 cores, 16 GB RAM
- **OS:** Linux 6.17.0-1013-azure

## Results

### CounterBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusInc | 59.54K | ± 474.36 | ops/s | **fastest** |
| prometheusNoLabelsInc | 51.77K | ± 826.63 | ops/s | 1.2x slower |
| prometheusAdd | 48.24K | ± 317.44 | ops/s | 1.2x slower |
| codahaleIncNoLabels | 43.87K | ± 249.00 | ops/s | 1.4x slower |
| simpleclientInc | 6.34K | ± 47.17 | ops/s | 9.4x slower |
| simpleclientNoLabelsInc | 6.00K | ± 219.07 | ops/s | 9.9x slower |
| simpleclientAdd | 5.91K | ± 254.72 | ops/s | 10x slower |
| openTelemetryInc | 1.44K | ± 144.82 | ops/s | 41x slower |
| openTelemetryIncNoLabels | 1.37K | ± 71.90 | ops/s | 43x slower |
| openTelemetryAdd | 1.35K | ± 31.52 | ops/s | 44x slower |

### HistogramBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusClassic | 6.26K | ± 1.88K | ops/s | **fastest** |
| simpleclient | 4.51K | ± 62.87 | ops/s | 1.4x slower |
| prometheusNative | 2.83K | ± 244.48 | ops/s | 2.2x slower |
| openTelemetryClassic | 625.59 | ± 43.55 | ops/s | 10x slower |
| openTelemetryExponential | 541.34 | ± 12.65 | ops/s | 12x slower |

### TextFormatUtilBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusWriteToNull | 535.57K | ± 5.32K | ops/s | **fastest** |
| prometheusWriteToByteArray | 526.63K | ± 4.21K | ops/s | 1.0x slower |
| openMetricsWriteToNull | 515.78K | ± 4.71K | ops/s | 1.0x slower |
| openMetricsWriteToByteArray | 511.54K | ± 2.77K | ops/s | 1.0x slower |

### Raw Results

```
Benchmark                                            Mode  Cnt          Score        Error  Units
CounterBenchmark.codahaleIncNoLabels                thrpt   15      43868.151    ± 249.005  ops/s
CounterBenchmark.openTelemetryAdd                   thrpt   15       1351.691     ± 31.518  ops/s
CounterBenchmark.openTelemetryInc                   thrpt   15       1437.739    ± 144.825  ops/s
CounterBenchmark.openTelemetryIncNoLabels           thrpt   15       1370.106     ± 71.900  ops/s
CounterBenchmark.prometheusAdd                      thrpt   15      48242.995    ± 317.444  ops/s
CounterBenchmark.prometheusInc                      thrpt   15      59541.052    ± 474.359  ops/s
CounterBenchmark.prometheusNoLabelsInc              thrpt   15      51766.008    ± 826.632  ops/s
CounterBenchmark.simpleclientAdd                    thrpt   15       5911.243    ± 254.724  ops/s
CounterBenchmark.simpleclientInc                    thrpt   15       6343.024     ± 47.165  ops/s
CounterBenchmark.simpleclientNoLabelsInc            thrpt   15       6004.154    ± 219.070  ops/s
HistogramBenchmark.openTelemetryClassic             thrpt   15        625.593     ± 43.545  ops/s
HistogramBenchmark.openTelemetryExponential         thrpt   15        541.341     ± 12.649  ops/s
HistogramBenchmark.prometheusClassic                thrpt   15       6261.013   ± 1876.556  ops/s
HistogramBenchmark.prometheusNative                 thrpt   15       2834.838    ± 244.483  ops/s
HistogramBenchmark.simpleclient                     thrpt   15       4507.355     ± 62.874  ops/s
TextFormatUtilBenchmark.openMetricsWriteToByteArray  thrpt   15     511537.456   ± 2768.864  ops/s
TextFormatUtilBenchmark.openMetricsWriteToNull      thrpt   15     515780.123   ± 4714.175  ops/s
TextFormatUtilBenchmark.prometheusWriteToByteArray  thrpt   15     526632.365   ± 4210.484  ops/s
TextFormatUtilBenchmark.prometheusWriteToNull       thrpt   15     535567.836   ± 5315.039  ops/s
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
