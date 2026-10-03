# Prometheus Java Client Benchmarks

## Run Information

- **Date:** 2026-10-03T08:43:24Z
- **Commit:** [`4b69f40`](https://github.com/psantamaria/client_java/commit/4b69f40bd4e616d69468ce99dc4323162287a577)
- **JDK:** 25.0.2 (OpenJDK 64-Bit Server VM)
- **Benchmark config:** 3 fork(s), 3 warmup, 5 measurement, 4 threads
- **Hardware:** AMD EPYC 9V45 96-Core Processor, 4 cores, 16 GB RAM
- **OS:** Linux 6.17.0-1022-azure

## Results

### CounterBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusInc | 67.84K | ± 829.77 | ops/s | **fastest** |
| prometheusNoLabelsInc | 65.02K | ± 1.03K | ops/s | 1.0x slower |
| codahaleIncNoLabels | 59.33K | ± 249.92 | ops/s | 1.1x slower |
| prometheusAdd | 58.95K | ± 1.83K | ops/s | 1.2x slower |
| simpleclientInc | 10.96K | ± 140.83 | ops/s | 6.2x slower |
| simpleclientNoLabelsInc | 10.73K | ± 106.52 | ops/s | 6.3x slower |
| simpleclientAdd | 10.30K | ± 263.57 | ops/s | 6.6x slower |
| openTelemetryIncNoLabels | 2.20K | ± 283.15 | ops/s | 31x slower |
| openTelemetryAdd | 1.95K | ± 253.96 | ops/s | 35x slower |
| openTelemetryInc | 1.87K | ± 143.71 | ops/s | 36x slower |

### HistogramBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusClassic | 7.72K | ± 2.06K | ops/s | **fastest** |
| simpleclient | 7.17K | ± 132.21 | ops/s | 1.1x slower |
| prometheusNative | 4.90K | ± 554.80 | ops/s | 1.6x slower |
| openTelemetryClassic | 947.47 | ± 35.69 | ops/s | 8.1x slower |
| openTelemetryExponential | 753.66 | ± 50.85 | ops/s | 10x slower |

### TextFormatUtilBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusWriteToNull | 736.34K | ± 44.55K | ops/s | **fastest** |
| openMetricsWriteToNull | 685.06K | ± 46.64K | ops/s | 1.1x slower |
| prometheusWriteToByteArray | 682.20K | ± 15.86K | ops/s | 1.1x slower |
| openMetricsWriteToByteArray | 671.37K | ± 11.95K | ops/s | 1.1x slower |

### Raw Results

```
Benchmark                                            Mode  Cnt          Score        Error  Units
CounterBenchmark.codahaleIncNoLabels                thrpt   15      59326.823    ± 249.923  ops/s
CounterBenchmark.openTelemetryAdd                   thrpt   15       1953.719    ± 253.956  ops/s
CounterBenchmark.openTelemetryInc                   thrpt   15       1866.316    ± 143.707  ops/s
CounterBenchmark.openTelemetryIncNoLabels           thrpt   15       2197.936    ± 283.151  ops/s
CounterBenchmark.prometheusAdd                      thrpt   15      58952.558   ± 1834.080  ops/s
CounterBenchmark.prometheusInc                      thrpt   15      67842.618    ± 829.769  ops/s
CounterBenchmark.prometheusNoLabelsInc              thrpt   15      65017.756   ± 1030.076  ops/s
CounterBenchmark.simpleclientAdd                    thrpt   15      10295.639    ± 263.572  ops/s
CounterBenchmark.simpleclientInc                    thrpt   15      10961.463    ± 140.826  ops/s
CounterBenchmark.simpleclientNoLabelsInc            thrpt   15      10730.009    ± 106.517  ops/s
HistogramBenchmark.openTelemetryClassic             thrpt   15        947.465     ± 35.691  ops/s
HistogramBenchmark.openTelemetryExponential         thrpt   15        753.660     ± 50.853  ops/s
HistogramBenchmark.prometheusClassic                thrpt   15       7720.996   ± 2056.040  ops/s
HistogramBenchmark.prometheusNative                 thrpt   15       4900.789    ± 554.805  ops/s
HistogramBenchmark.simpleclient                     thrpt   15       7174.091    ± 132.212  ops/s
TextFormatUtilBenchmark.openMetricsWriteToByteArray  thrpt   15     671371.631  ± 11953.394  ops/s
TextFormatUtilBenchmark.openMetricsWriteToNull      thrpt   15     685056.948  ± 46641.376  ops/s
TextFormatUtilBenchmark.prometheusWriteToByteArray  thrpt   15     682203.265  ± 15862.302  ops/s
TextFormatUtilBenchmark.prometheusWriteToNull       thrpt   15     736338.383  ± 44545.929  ops/s
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
