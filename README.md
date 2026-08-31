# Prometheus Java Client Benchmarks

## Run Information

- **Date:** 2026-08-31T09:16:00Z
- **Commit:** [`4b69f40`](https://github.com/psantamaria/client_java/commit/4b69f40bd4e616d69468ce99dc4323162287a577)
- **JDK:** 25.0.2 (OpenJDK 64-Bit Server VM)
- **Benchmark config:** 3 fork(s), 3 warmup, 5 measurement, 4 threads
- **Hardware:** AMD EPYC 7763 64-Core Processor, 4 cores, 16 GB RAM
- **OS:** Linux 6.17.0-1022-azure

## Results

### CounterBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusInc | 64.13K | ± 1.26K | ops/s | **fastest** |
| prometheusNoLabelsInc | 55.89K | ± 1.17K | ops/s | 1.1x slower |
| prometheusAdd | 50.37K | ± 1.12K | ops/s | 1.3x slower |
| codahaleIncNoLabels | 47.91K | ± 1.01K | ops/s | 1.3x slower |
| simpleclientNoLabelsInc | 6.52K | ± 126.70 | ops/s | 9.8x slower |
| simpleclientInc | 6.52K | ± 171.21 | ops/s | 9.8x slower |
| simpleclientAdd | 6.31K | ± 243.09 | ops/s | 10x slower |
| openTelemetryAdd | 1.44K | ± 243.79 | ops/s | 45x slower |
| openTelemetryInc | 1.35K | ± 158.90 | ops/s | 47x slower |
| openTelemetryIncNoLabels | 1.26K | ± 5.98 | ops/s | 51x slower |

### HistogramBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusClassic | 6.80K | ± 436.59 | ops/s | **fastest** |
| simpleclient | 4.32K | ± 92.04 | ops/s | 1.6x slower |
| prometheusNative | 3.05K | ± 310.80 | ops/s | 2.2x slower |
| openTelemetryClassic | 696.95 | ± 17.11 | ops/s | 9.8x slower |
| openTelemetryExponential | 542.58 | ± 4.16 | ops/s | 13x slower |

### TextFormatUtilBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusWriteToNull | 485.61K | ± 1.85K | ops/s | **fastest** |
| prometheusWriteToByteArray | 481.96K | ± 1.92K | ops/s | 1.0x slower |
| openMetricsWriteToNull | 475.38K | ± 3.57K | ops/s | 1.0x slower |
| openMetricsWriteToByteArray | 466.39K | ± 5.54K | ops/s | 1.0x slower |

### Raw Results

```
Benchmark                                            Mode  Cnt          Score        Error  Units
CounterBenchmark.codahaleIncNoLabels                thrpt   15      47913.457   ± 1012.141  ops/s
CounterBenchmark.openTelemetryAdd                   thrpt   15       1436.578    ± 243.792  ops/s
CounterBenchmark.openTelemetryInc                   thrpt   15       1351.490    ± 158.902  ops/s
CounterBenchmark.openTelemetryIncNoLabels           thrpt   15       1255.822      ± 5.984  ops/s
CounterBenchmark.prometheusAdd                      thrpt   15      50374.976   ± 1116.312  ops/s
CounterBenchmark.prometheusInc                      thrpt   15      64134.959   ± 1255.900  ops/s
CounterBenchmark.prometheusNoLabelsInc              thrpt   15      55892.541   ± 1165.514  ops/s
CounterBenchmark.simpleclientAdd                    thrpt   15       6306.416    ± 243.088  ops/s
CounterBenchmark.simpleclientInc                    thrpt   15       6519.160    ± 171.209  ops/s
CounterBenchmark.simpleclientNoLabelsInc            thrpt   15       6520.306    ± 126.700  ops/s
HistogramBenchmark.openTelemetryClassic             thrpt   15        696.948     ± 17.112  ops/s
HistogramBenchmark.openTelemetryExponential         thrpt   15        542.583      ± 4.157  ops/s
HistogramBenchmark.prometheusClassic                thrpt   15       6798.410    ± 436.594  ops/s
HistogramBenchmark.prometheusNative                 thrpt   15       3051.236    ± 310.795  ops/s
HistogramBenchmark.simpleclient                     thrpt   15       4315.495     ± 92.044  ops/s
TextFormatUtilBenchmark.openMetricsWriteToByteArray  thrpt   15     466393.620   ± 5542.502  ops/s
TextFormatUtilBenchmark.openMetricsWriteToNull      thrpt   15     475377.251   ± 3565.360  ops/s
TextFormatUtilBenchmark.prometheusWriteToByteArray  thrpt   15     481962.279   ± 1915.896  ops/s
TextFormatUtilBenchmark.prometheusWriteToNull       thrpt   15     485611.225   ± 1849.222  ops/s
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
