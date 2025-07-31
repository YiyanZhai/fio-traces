# CloudPhysics FIO Traces

This dataset contains fio I/O logs derived from [CloudPhysics](https://ftp.pdl.cmu.edu/pub/datasets/twemcacheWorkload/cacheDatasets/cloudphysics/). The traces have been transformed into formats described in [FIO Trace file format](https://fio.readthedocs.io/en/latest/fio_doc.html#trace-file-format-v2).

## Content
In `cloudphysics_fio_traces_compressed`, there are the compressed `w01.fio` to `w106.fio` trace files (v2 format).

## How the Conversion Was Done

The original traces followed this format:

```c
struct {
  uint32_t real_time;
  uint64_t obj_id;
  uint32_t obj_size;
  int64_t next_access_vtime;
};
```

We converted these for FIO using:

```cpp
offset = obj_id * 4096;
size = obj_size;
```

to simulate logical block access with 4KB alignment.

## Decompress

To decompress the traces, use the following command under `./cloudphysics_fio_traces_compressed`:

```bash
xz -d w76.fio.xz
```