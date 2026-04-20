# Ascend Index SDK

> English | [中文](./OVERVIEW.zh.md)

## Supported Tags and Dockerfile Links

### Tag Naming Convention

Tags follow this pattern:

```bash
<cann_version>-<chip_series>-<os>-<python_version>
```

| Field            | Example Values                  | Description               |
| ---------------- | ------------------------------- | ------------------------- |
| `cann_version`   | `9.0.0`   | CANN version              |
| `chip_series`    | `910b`, `a3`, `310p`            | Target Ascend chip family |
| `os`             | `ubuntu22.04`, `openeuler24.03` | Base operating system     |
| `python_version` | `py3.11`    | Python version            |

- CANN is maintained by 

  [CANN community](https://www.hiascend.com/cann)

### CANN 9.0.0 Base Image

| Tag                                | Dockerfile                                                   | Image Content        |
| ---------------------------------- | ------------------------------------------------------------ | --------------- |
| `9.0.0-910b-ubuntu22.04-py3.11`    | [Dockerfile](https://github.com/Ascend/cann-container-image/blob/main/cann/9.0.0-beta.2-910b-ubuntu22.04-py3.11/Dockerfile) | toolkit |
| `9.0.0-310p-ubuntu22.04-py3.11`    | [Dockerfile](https://github.com/Ascend/cann-container-image/blob/main/cann/9.0.0-beta.2-310p-ubuntu22.04-py3.11/Dockerfile)      | toolkit |
| `9.0.0-a3-ubuntu22.04-py3.11` | [Dockerfile](https://github.com/Ascend/cann-container-image/blob/main/cann/9.0.0-beta.2-a3-ubuntu22.04-py3.11/Dockerfile)         | toolkit |

---

## Quick Start

### Prerequisites (optional)

#### Install Driver

An Ascend NPU driver compatible with the container's CANN version must be installed on the host. See the [CANN Compatibility Matrix](https://www.hiascend.com/document) for driver ↔ CANN version mapping.

---

### Running a Index Container

```bash
docker run \
    --name index_container \
    --device /dev/davinci1 \
    --device /dev/davinci_manager \
    --device /dev/devmm_svm \
    --device /dev/hisi_hdc \
    -v /usr/local/dcmi:/usr/local/dcmi \
    -v /usr/local/bin/npu-smi:/usr/local/bin/npu-smi \
    -v /usr/local/Ascend/driver/lib64/:/usr/local/Ascend/driver/lib64/ \
    -v /usr/local/Ascend/driver/version.info:/usr/local/Ascend/driver/version.info \
    -v /etc/ascend_install.info:/etc/ascend_install.info \
    -it ascend/index:tag bash
```

### How to build

```bash
docker buildx build -t {your_repo}/index:latest -f Dockerfile .
```

### Development

```bash
# Add required software by developer
FROM swr.cn-south-1.myhuaweicloud.com/ascendhub/cann:9.0.0-beta.1-910b-ubuntu22.04-py3.11

RUN apt update -y && \
    apt install gcc ...

...
```

---

## Supported Hardware

| Chip Series | Product Examples                | Architecture   |
| ----------- | ------------------------------- | -------------- |
| Ascend 910B | Atlas 800I A2                   | ARM64 / x86_64 |
| Ascend A3   | Atlas 800I A3                   | ARM64 / x86_64 |
| Ascend 310P | Atlas 300I Pro, Atlas 300V Pro  | ARM64 / x86_64 |

---

## License

View the [license information](https://github.com/Ascend/cann-container-image/blob/main/LICENSE) for CANN and MindSeries software included in these images.

As with all container images, the pre-installed packages (Python, system libraries, etc.) may be subject to their own licenses.
