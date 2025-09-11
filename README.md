# About the Fork
This project was forked from [VulHunter](https://github.com/Secbrain/VulHunter) for independent evaluation as part of master thesis "Machine Learning for Vulnerability Detection in Smart Contracts A Comparison of Approaches".

It provides the following infrastructural changes for integration into [SmartBugs](https://github.com/smartbugs/smartbugs):
- Added [devcontainer](https://containers.dev/) configuration installing all dependencies and also solc
- We install python dependencies from scratch, because the provided venv is corrupted
- Replaced the included solc binaries, some of which were corrupted and produced segmentation faults on execution
- Provided a Dockerfile
- Added missing fonts, which prevented the PDF report from being printed
- Added logging of exceptions in case of solc compilation errors
- Added writing of the JSON vulnerability report to a file additionally to stdout

Docker Image published at `deet0x/vulhunter:0.1`

Build Instructions for SmartBugs container:
1. `cd VulHunter`
2. `docker build . -t smartbugs/vulhunter:0.1`

Vulhunter can be started via `python VulHunter/main/main.py`

```
usage: main.py contract.sol/bin/evm [flag]

VulHunter. For usage information, run --help

optional arguments:
  -h, --help            show this help message and exit
  --contract CONTRACT   contract.sol
  --version             Displays the current version

Detectors:
  --detectors DETECTORS
                        Comma-separated list of detectors, defaults to all, available detectors: reentrancy-eth, controlled-array-length,
                        suicidal, controlled-delegatecall, arbitrary-send, incorrect-equality, integer-overflow, unchecked-lowlevel, tx-origin,
                        locked-ether, unchecked-send, costly-loop, erc721-interface, erc20-interface, timestamp, block-other-parameters, calls-
                        loop, low-level-calls, erc20-indexed, erc20-throw, hardcoded, array-instead-bytes, unused-state, costly-operations-loop,
                        external-function, send-transfer, boolean-equal, boolean-cst, uninitialized-state, tod
  --list-detectors      List available detectors

Miscs:
  --filetype FILETYPE   Input the file type of the contract [solidity (default), bytecode, and opcode]
  --solc-version SOLC_VERSION
                        Input the solc version of compling contract 0.4.24 (default)
  --ifmap IFMAP         Input the retult mapping item: map (default), nomap
  --map-number MAP_NUMBER
                        Set the number of mapping positions in instances (default 3)
  --instance-len INSTANCE_LEN
                        Input the number of extracting instances (default 10)
  --report REPORT       Export the audit report as a pdf file ("--report -" to export to stdout)
  --report-main REPORT_MAIN
                        Export the main audit report as a pdf file ("--report-main -" to export to main stdout)
  --tmp-dir TMP_DIR     Set the tmp dir (default .)
  --model-dir MODEL_DIR
                        Set the model dir (default ./models)

Tranning:
  --train-contracts TRAIN_CONTRACTS
                        Input the trainning contract files
  --train-solcversions TRAIN_SOLCVERSIONS
                        Input the solc versions of contracts
  --instance-dir INSTANCE_DIR
                        Input the dir path of generating contract instances
  --train-labels TRAIN_LABELS
                        Input the trainning labels of contracts
  --contract-instances CONTRACT_INSTANCES
                        Input the trainning instances of contracts
  --epoch EPOCH         Set the trainning epoch (default 50)
  --data-len DATA_LEN   Set the instance length (default 512)
  --batchsize BATCHSIZE
                        Set the batchsize (default 512)

Verifying:
  --verify              Set the batchsize (default False)
  --solver SOLVER       Set the batchsize (default Z3), and select multiple solver by using commas to separate, e.g., Z3,Yices,CVC4. Also, this
                        is equivalent to ALL.

```
# 🏹 TSE_VulHunter
This project is the supporting material of the paper titled "VulHunter: Hunting Vulnerable Smart Contracts at EVM bytecode-level via Multiple Instance Learning", including: dataset, detection results, source code, etc.

# Folder introduction

## Dataset1

The folder "Dataset1" includes 38,600 smart contract source codes in Dataset_1, and the detection results of each method.

## Dataset2

The folder "Dataset2" includes 579 Ethereum smart contract bytecodes in Dataset_2, and the detection results of each method.

## Dataset3

The folder "Dataset3" includes 13,413 Ethereum smart contract source codes in Dataset_3, and the detection results of each method.

## Dataset4

The folder "Dataset4" includes 183,710 Ethereum smart contract bytecodes in Dataset_4, and the detection results of each method.

## Dataset5

The folder "Dataset5" includes 29 smart contract source codes of well-known vulnerability events in Dataset_5, and the detection results of each method.

## Dataset_vul_num

The folder "Dataset_vul_num" includes two .xlsx files, which illustrates the number of each vulnerability in Dataset_1 and Dataset_2, respectively.

## VulHunter

The folder "VulHunter" includes part of the source code of VulHunter and its installation and usage tutorials. Also, it provides the pre-trained models on Benign:Malicious=2:1 contracts in Dataset_1.

## VulnerabilityMapping

The folder "VulnerabilityMapping" includes the mapping of vulnerabilities detected by methods.

## Opcodes

The folder "Opcodes" describes the Ethereum opcodes in detail.

## Severity_assessment

The folder "Severity_assessment" details contract vulnerability assessment method and its judgment basis.

## Vulnerability_examples

The folder "Vulnerability_examples" depicts the 30 kinds of vulnerabilities involved in the paper, and combines the contract code to explain the vulnerability examples excepting the paper in terms of occurrence principle, severity, repair countermeasures, and insights at bytecode level.

## Reports_examples

The folder "Reports_examples" contains the security analysis reports automatically generated by VulHunter.

## Learner_models

The folder "Learner_models" includes the detection results of VulHunter with ten baseline models (i.e., Deep Learning and traditional Machine Learning models) on Dataset_1.

## Rationality

The folder "Rationality" includes the detection results of VulHunter with and without the Bag-instance hybrid attention mechanism on Dataset_1.
