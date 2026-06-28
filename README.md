# Prometheus Java Client Benchmarks

## Run Information

- **Date:** 2026-06-28T07:31:01Z
- **Commit:** [`4b69f40`](https://github.com/psantamaria/client_java/commit/4b69f40bd4e616d69468ce99dc4323162287a577)
- **JDK:** 25.0.2 (OpenJDK 64-Bit Server VM)
- **Benchmark config:** 3 fork(s), 3 warmup, 5 measurement, 4 threads
- **Hardware:** AMD EPYC 7763 64-Core Processor, 4 cores, 16 GB RAM
- **OS:** Linux 6.17.0-1018-azure

## Results

### CounterBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusInc | 65.28K | ± 1.01K | ops/s | **fastest** |
| prometheusNoLabelsInc | 57.08K | ± 83.76 | ops/s | 1.1x slower |
| prometheusAdd | 51.18K | ± 511.25 | ops/s | 1.3x slower |
| codahaleIncNoLabels | 48.21K | ± 1.73K | ops/s | 1.4x slower |
| simpleclientInc | 6.67K | ± 57.86 | ops/s | 9.8x slower |
| simpleclientNoLabelsInc | 6.35K | ± 195.21 | ops/s | 10x slower |
| simpleclientAdd | 6.30K | ± 226.22 | ops/s | 10x slower |
| openTelemetryInc | 1.42K | ± 222.25 | ops/s | 46x slower |
| openTelemetryIncNoLabels | 1.32K | ± 12.46 | ops/s | 49x slower |
| openTelemetryAdd | 1.27K | ± 54.41 | ops/s | 51x slower |

### HistogramBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusClassic | 5.52K | ± 1.21K | ops/s | **fastest** |
| simpleclient | 4.37K | ± 33.22 | ops/s | 1.3x slower |
| prometheusNative | 2.79K | ± 190.36 | ops/s | 2.0x slower |
| openTelemetryClassic | 704.67 | ± 28.68 | ops/s | 7.8x slower |
| openTelemetryExponential | 597.90 | ± 48.10 | ops/s | 9.2x slower |

### TextFormatUtilBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusWriteToNull | 491.45K | ± 3.55K | ops/s | **fastest** |
| prometheusWriteToByteArray | 488.38K | ± 3.88K | ops/s | 1.0x slower |
| openMetricsWriteToNull | 476.85K | ± 11.60K | ops/s | 1.0x slower |
| openMetricsWriteToByteArray | 475.76K | ± 7.26K | ops/s | 1.0x slower |

### Raw Results

```
Benchmark                                            Mode  Cnt          Score        Error  Units
CounterBenchmark.codahaleIncNoLabels                thrpt   15      48207.086   ± 1734.046  ops/s
CounterBenchmark.openTelemetryAdd                   thrpt   15       1268.378     ± 54.408  ops/s
CounterBenchmark.openTelemetryInc                   thrpt   15       1420.984    ± 222.252  ops/s
CounterBenchmark.openTelemetryIncNoLabels           thrpt   15       1324.601     ± 12.456  ops/s
CounterBenchmark.prometheusAdd                      thrpt   15      51181.378    ± 511.254  ops/s
CounterBenchmark.prometheusInc                      thrpt   15      65280.507   ± 1008.600  ops/s
CounterBenchmark.prometheusNoLabelsInc              thrpt   15      57078.814     ± 83.761  ops/s
CounterBenchmark.simpleclientAdd                    thrpt   15       6298.633    ± 226.219  ops/s
CounterBenchmark.simpleclientInc                    thrpt   15       6670.902     ± 57.863  ops/s
CounterBenchmark.simpleclientNoLabelsInc            thrpt   15       6346.138    ± 195.208  ops/s
HistogramBenchmark.openTelemetryClassic             thrpt   15        704.673     ± 28.675  ops/s
HistogramBenchmark.openTelemetryExponential         thrpt   15        597.902     ± 48.096  ops/s
HistogramBenchmark.prometheusClassic                thrpt   15       5516.783   ± 1211.395  ops/s
HistogramBenchmark.prometheusNative                 thrpt   15       2792.685    ± 190.360  ops/s
HistogramBenchmark.simpleclient                     thrpt   15       4374.569     ± 33.219  ops/s
TextFormatUtilBenchmark.openMetricsWriteToByteArray  thrpt   15     475762.697   ± 7264.961  ops/s
TextFormatUtilBenchmark.openMetricsWriteToNull      thrpt   15     476854.650  ± 11602.562  ops/s
TextFormatUtilBenchmark.prometheusWriteToByteArray  thrpt   15     488377.392   ± 3881.309  ops/s
TextFormatUtilBenchmark.prometheusWriteToNull       thrpt   15     491446.373   ± 3554.610  ops/s
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
