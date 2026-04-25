# Prometheus Java Client Benchmarks

## Run Information

- **Date:** 2026-04-25T05:50:02Z
- **Commit:** [`4b69f40`](https://github.com/psantamaria/client_java/commit/4b69f40bd4e616d69468ce99dc4323162287a577)
- **JDK:** 25.0.2 (OpenJDK 64-Bit Server VM)
- **Benchmark config:** 3 fork(s), 3 warmup, 5 measurement, 4 threads
- **Hardware:** AMD EPYC 7763 64-Core Processor, 4 cores, 16 GB RAM
- **OS:** Linux 6.17.0-1010-azure

## Results

### CounterBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusInc | 65.71K | ± 1.73K | ops/s | **fastest** |
| prometheusNoLabelsInc | 56.59K | ± 213.89 | ops/s | 1.2x slower |
| prometheusAdd | 50.47K | ± 591.71 | ops/s | 1.3x slower |
| codahaleIncNoLabels | 48.12K | ± 1.63K | ops/s | 1.4x slower |
| simpleclientInc | 6.54K | ± 206.00 | ops/s | 10x slower |
| simpleclientNoLabelsInc | 6.38K | ± 215.49 | ops/s | 10x slower |
| simpleclientAdd | 6.11K | ± 300.52 | ops/s | 11x slower |
| openTelemetryAdd | 1.46K | ± 171.79 | ops/s | 45x slower |
| openTelemetryInc | 1.41K | ± 175.63 | ops/s | 47x slower |
| openTelemetryIncNoLabels | 1.31K | ± 134.56 | ops/s | 50x slower |

### HistogramBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusClassic | 5.80K | ± 1.11K | ops/s | **fastest** |
| simpleclient | 4.40K | ± 64.17 | ops/s | 1.3x slower |
| prometheusNative | 2.94K | ± 325.62 | ops/s | 2.0x slower |
| openTelemetryClassic | 690.81 | ± 25.00 | ops/s | 8.4x slower |
| openTelemetryExponential | 552.95 | ± 3.19 | ops/s | 10x slower |

### TextFormatUtilBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusWriteToNull | 487.06K | ± 7.32K | ops/s | **fastest** |
| prometheusWriteToByteArray | 483.52K | ± 2.77K | ops/s | 1.0x slower |
| openMetricsWriteToNull | 475.09K | ± 13.81K | ops/s | 1.0x slower |
| openMetricsWriteToByteArray | 472.69K | ± 5.51K | ops/s | 1.0x slower |

### Raw Results

```
Benchmark                                            Mode  Cnt          Score        Error  Units
CounterBenchmark.codahaleIncNoLabels                thrpt   15      48121.967   ± 1630.907  ops/s
CounterBenchmark.openTelemetryAdd                   thrpt   15       1463.050    ± 171.786  ops/s
CounterBenchmark.openTelemetryInc                   thrpt   15       1405.078    ± 175.629  ops/s
CounterBenchmark.openTelemetryIncNoLabels           thrpt   15       1314.832    ± 134.556  ops/s
CounterBenchmark.prometheusAdd                      thrpt   15      50469.924    ± 591.712  ops/s
CounterBenchmark.prometheusInc                      thrpt   15      65705.481   ± 1728.676  ops/s
CounterBenchmark.prometheusNoLabelsInc              thrpt   15      56587.768    ± 213.895  ops/s
CounterBenchmark.simpleclientAdd                    thrpt   15       6111.444    ± 300.521  ops/s
CounterBenchmark.simpleclientInc                    thrpt   15       6535.243    ± 206.000  ops/s
CounterBenchmark.simpleclientNoLabelsInc            thrpt   15       6378.775    ± 215.490  ops/s
HistogramBenchmark.openTelemetryClassic             thrpt   15        690.813     ± 25.003  ops/s
HistogramBenchmark.openTelemetryExponential         thrpt   15        552.951      ± 3.192  ops/s
HistogramBenchmark.prometheusClassic                thrpt   15       5799.169   ± 1106.574  ops/s
HistogramBenchmark.prometheusNative                 thrpt   15       2935.867    ± 325.619  ops/s
HistogramBenchmark.simpleclient                     thrpt   15       4396.012     ± 64.169  ops/s
TextFormatUtilBenchmark.openMetricsWriteToByteArray  thrpt   15     472694.997   ± 5509.928  ops/s
TextFormatUtilBenchmark.openMetricsWriteToNull      thrpt   15     475094.046  ± 13811.076  ops/s
TextFormatUtilBenchmark.prometheusWriteToByteArray  thrpt   15     483515.130   ± 2770.318  ops/s
TextFormatUtilBenchmark.prometheusWriteToNull       thrpt   15     487063.452   ± 7319.224  ops/s
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
