
# Multimodal Data Pipeline Demo

This project demonstrates a data processing pipeline for multimodal data using PySpark.

## 1. Installation

These instructions are for macOS with Homebrew.

### Install Homebrew

If you don't have Homebrew installed, run this command:
```bash
/bin/bash -c "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/HEAD/install.sh)"
```

### Install Java (OpenJDK 17)

PySpark requires a Java runtime.
```bash
brew install openjdk@17
brew link --force --overwrite openjdk@17
```

### Install Python Dependencies

It is recommended to use a virtual environment. These instructions use `uv`.
```bash
uv pip install boto3
uv pip install pyspark
uv pip install opencv-python-headless librosa
uv pip install tensorflow-data-validation
uv pip install ray

# Pin numpy version if required
pip install --force-reinstall -v "numpy==1.25.2"
```

## 2. Configuration

### PySpark Environment Setup

For PySpark to find Java, you need to set the `JAVA_HOME` environment variable.

To set it for your current terminal session:
```bash
export JAVA_HOME="/opt/homebrew/opt/openjdk@17"
export PATH="$JAVA_HOME/bin:$PATH"
```

To make this setting permanent within a Conda environment, follow these steps:

1.  **Create an activation script:**
    ```bash
    mkdir -p $CONDA_PREFIX/etc/conda/activate.d
    nano $CONDA_PREFIX/etc/conda/activate.d/java_home.sh
    ```

2.  **Add the following lines to `java_home.sh`:**
    ```sh
    export JAVA_HOME="/opt/homebrew/opt/openjdk@17"
    export PATH="$JAVA_HOME/bin:$PATH"
    ```

3.  **Create a deactivation script to clean up:**
    ```bash
    mkdir -p $CONDA_PREFIX/etc/conda/deactivate.d
    nano $CONDA_PREFIX/etc/conda/deactivate.d/java_home.sh
    ```

4.  **Add the following line to the deactivate script:**
    ```sh
    unset JAVA_HOME
    ```

## 3. Data Sources

-   **ISMIR Datasets**: https://ismir.net/resources/datasets/
-   **ACM MIRUM Dataset**: https://github.com/audiocontentanalysis/dataset-acm_mirum

## 4. Storage Options

### Cloudflare R2

Cloudflare R2 is an S3-compatible object storage solution.

### Local Development (MinIO)

For local development, you can run an S3-compatible server using MinIO with Docker.

```bash
docker run -p 9000:9000 -p 9001:9001 minio/minio server /data --console-address ":9001"
```

-   **Endpoint**: `http://127.0.0.1:9000`
-   **Console**: `http://127.0.0.1:9001`
-   **Default Access Key**: `minioadmin`
-   **Default Secret Key**: `minioadmin`

## 5. Reference

