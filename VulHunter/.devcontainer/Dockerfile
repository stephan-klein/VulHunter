# Use the official Python 3.9 Bookworm base image.
FROM mcr.microsoft.com/devcontainers/python:1-3.7-bookworm

# Set the working directory to the project root
RUN pip install -v torch==1.10.1 
RUN pip install tqdm scikit-learn==1.0.2 pandas numpy==1.21.6 pyevmasm==0.2.3 py-solc-x==0.10.1 evm_cfg_builder==0.3.1 reportlab==3.6.12 seaborn==0.12.2 reportlab==3.6.12 joblib==1.3.2

# Copy the split zip files
COPY .solcx.z* /home/vscode/

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