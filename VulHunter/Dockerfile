# Use the official Python 3.8 base image
FROM python:3.8-bookworm

# Copy the split zip files
COPY ./.solcx.z* /root/

RUN mkdir -p /usr/share/fonts/chinese
COPY ./fonts/MSYH.TTC ./fonts/SimHei.ttf ./fonts/simsun.ttc ./fonts/times.ttf /usr/share/fonts/chinese/
RUN chmod 644 /usr/share/fonts/chinese/*

# Install fontconfig before running fc-cache
RUN apt-get update && apt-get install -y fontconfig zip unzip
RUN fc-cache -f -v

# Create .solcx directory and handle the split zip files
RUN cd /root && \
    zip -F .solcx.zip --out /root/solc_complete.zip && \
    unzip solc_complete.zip -d .solcx && \
    rm solc_complete.zip && \
    rm .solcx.z* && \
    chmod -R 777 /root/.solcx/*

# Install Python dependencies
RUN pip install -v torch==1.10.1
RUN pip install tqdm scikit-learn==1.0.2 pandas numpy==1.21.6 pyevmasm==0.2.3 py-solc-x==0.10.1 evm_cfg_builder==0.3.1 reportlab==3.6.12 seaborn==0.12.2 reportlab==3.6.12 joblib==1.3.2
RUN pip install z3-solver==4.12.1.0
RUN pip install "protobuf~=3.20" pyyaml pysha3 prettytable ply rlp intervaltree "crytic-compile>=0.2.2" wasm "dataclasses; python_version < '3.7'" "pyevmasm>=0.2.3" manticore==0.3.7
RUN pip install manticore[native]

WORKDIR /app

# Copy setup.py and related files for editable install
# COPY ./setup.py ./README.md ./
# Only copy if these files exist; ignore if not present

# Install the package in editable mode with native extras
# RUN pip install -e ".[native]"

# Copy only the files/folders previously allowed by .dockerignore
COPY docs/ ./docs/
COPY contracts_test/ ./contracts_test/
COPY main/ ./main/
COPY models/ ./models/
COPY fonts/ ./fonts/
COPY README.md ./
