# Use the official Python 3.9 Bookworm base image.
FROM mcr.microsoft.com/devcontainers/python:1-3.8-bookworm

# Copy the split zip files
COPY VulHunter/.solcx.z* /home/vscode/

RUN mkdir -p /usr/share/fonts/chinese
COPY .devcontainer/MSYH.TTC .devcontainer/SimHei.ttf .devcontainer/simsun.ttc .devcontainer/times.ttf /usr/share/fonts/chinese/
RUN chmod 644 /usr/share/fonts/chinese/*

# Install fontconfig before running fc-cache
RUN apt-get update && apt-get install -y fontconfig
RUN fc-cache -f -v

# Create .solcx directory and handle the split zip files
RUN cd /home/vscode && \
    zip -F .solcx.zip --out /home/vscode/solc_complete.zip && \
    unzip solc_complete.zip && \
    rm solc_complete.zip && \
    rm .solcx.z* && \
    chmod -R 777 /home/vscode/.solcx/*

# Set the working directory to the project root
RUN pip install -v torch==1.10.1
RUN pip install tqdm scikit-learn==1.0.2 pandas numpy==1.21.6 pyevmasm==0.2.3 py-solc-x==0.10.1 evm_cfg_builder==0.3.1 reportlab==3.6.12 seaborn==0.12.2 reportlab==3.6.12 joblib==1.3.2

# My own dependencies
RUN pip install ipykernel

# Install Ethereum repository and solc compiler
RUN curl -L https://github.com/ethereum/solidity/releases/download/v0.8.21/solc-static-linux \
    -o /usr/local/bin/solc && \
    chmod +x /usr/local/bin/solc