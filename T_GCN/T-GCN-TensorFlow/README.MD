<!--
 * @Author: lzy
 * @Date: 2023-04-18 02:44:36
 * @LastEditors: lzy
 * @LastEditTime: 2023-04-18 03:04:57
 * @FilePath: 
 * @Description: 
 * 
-->
# Fast Start
This is a TensorFlow implementation of T-GCN: A Temporal Graph Convolutional Network for Traffic Prediction.
## OS
```
Ubuntu：20.04 Server
(Linux version 5.4.0-146-generic (buildd@lcy02-amd64-026) (gcc version 9.4.0 (Ubuntu 9.4.0-1ubuntu1~20.04.1)))
```
## Python Version
```
Python 3.7.15
```
## Create a virtual environment
```
python3 -m venv venv
```
## Activate venv
```
source venv/bin/activate
 ```
## Installation requirements
```
pip install -r requirements.txt
```
## Run
```
python main.py
```

# T-GCN
The GCN and GRU models were in gcn.py and gru.py respective.


The T-GCN model was in the tgcn.py


In order to use the model, we need
* A N by N adjacency matrix, which describes the connection relationships between nodes
* A N by D feature matrix, which describes the attribute values of nodes
