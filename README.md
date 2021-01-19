## Generate Protofile Type Definition For Typescript

### Install Make GNU

- MacOs
 ```sh
  brew install make
 ```

- Linux
 ```sh
  apt-get install make
 ```
 
 - Windows
 ```sh
  choco install make
 ```

### Run Command

```sh
make grpcwin | make grpclinmac | make protocgen 
```
 
### Script Runner (@grpc/grpc-js)

before you use this script is required to install `npm i protoc-gen-grpc && npm i grpc-tools -D` in local development first, and then create a folder with the name **protos** to save the file `.proto` and then create a folder with the name **typedefs** to save the result of `.proto` that has been generated, after successfully creating the **typedefs**, then create a **Makefile** and copy and paste this script.
 
 #### Windows
 
 ```bash
INPUT_DIR := ${realpath protos}
OUTPUT_DIR := ${realpath typedefs}
FIND_FILE := ${wildcard ${OUTPUT_DIR}/*.ts}
GRPC_TOOLS = grpc_tools_node_protoc
PROTOC_GEN_TS_PATH_WINDOWS := ${realpath node_modules/.bin/protoc-gen-ts.cmd}
PROTOC_GEN_TS_PATH_LINMAC := ${realpath node_modules/.bin/protoc-gen-ts}

#################################################################################
##===============================================================================
## GENERATE PROTO FILE FOR WINDOWS USING grpc_tools_node_protoc FOR @grpc/grpc-js
##===============================================================================
#################################################################################

grpcwin:
ifneq (${FIND_FILE}, )
	#remove old all file typedefs
	rm ${OUTPUT_DIR}/**.{ts,js}
	
	#generate protofile typedefs
	${shell exec} ${GRPC_TOOLS} \
	--plugin=protoc-gen-ts=${PROTOC_GEN_TS_PATH_WINDOWS} \
	--grpc_out=grpc_js:${OUTPUT_DIR} \
	--js_out=import_style=commonjs,binary:${OUTPUT_DIR} \
	--ts_out=grpc_js:${OUTPUT_DIR} \
	--proto_path ${INPUT_DIR} ${INPUT_DIR}/*.proto
else	
	#generate protofile typedefs if file not exist
	${shell exec} ${GRPC_TOOLS} \
	--plugin=protoc-gen-ts=${PROTOC_GEN_TS_PATH_WINDOWS} \
	--grpc_out=grpc_js:${OUTPUT_DIR} \
	--js_out=import_style=commonjs,binary:${OUTPUT_DIR} \
	--ts_out=grpc_js:${OUTPUT_DIR} \
	--proto_path ${INPUT_DIR} ${INPUT_DIR}/*.proto
endif
 ```

#### Linux/MacOS
 
```bash
INPUT_DIR := ${realpath protos}
OUTPUT_DIR := ${realpath typedefs}
FIND_FILE := ${wildcard ${OUTPUT_DIR}/*.ts}
GRPC_TOOLS = grpc_tools_node_protoc
PROTOC_GEN_TS_PATH_WINDOWS := ${realpath node_modules/.bin/protoc-gen-ts.cmd}
PROTOC_GEN_TS_PATH_LINMAC := ${realpath node_modules/.bin/protoc-gen-ts}

####################################################################################
##==================================================================================
## GENERATE PROTO FILE FOR LINUX/MAC USING grpc_tools_node_protoc FOR @grpc/grpc-js
##==================================================================================
####################################################################################

grpclinmac:
ifneq (${FIND_FILE}, )
	#remove old all file typedefs
	rm ${OUTPUT_DIR}/**.{ts,js}

	#generate protofile typedefs
	${shell exec} ${GRPC_TOOLS} \
	--plugin=protoc-gen-ts=${PROTOC_GEN_TS_PATH_LINMAC} \
	--grpc_out=grpc_js:${OUTPUT_DIR} \
	--js_out=import_style=commonjs,binary:${OUTPUT_DIR} \
	--ts_out=grpc_js:${OUTPUT_DIR} \
	--proto_path ${INPUT_DIR} ${INPUT_DIR}/*.proto
else
	#generate protofile typedefs if file not exist
	${shell exec} ${GRPC_TOOLS} \
	--plugin=protoc-gen-ts=${PROTOC_GEN_TS_PATH_LINMAC} \
	--grpc_out=grpc_js:${OUTPUT_DIR} \
	--js_out=import_style=commonjs,binary:${OUTPUT_DIR} \
	--ts_out=grpc_js:${OUTPUT_DIR} \
	--proto_path ${INPUT_DIR} ${INPUT_DIR}/*.proto
endif
```
 
### Script Runner (grpc)
 
before you use this script you are required to install `protoc-gen-grpc -D` in local development first, and then create a folder named **protos** to save the `.proto` file and then create a folder named **typedefs** to save the results of the `.proto` that has been generated, after successfully creating the **typedefs**, then create a **Makefile** and copy and paste this script.

 ```bash
INPUT_DIR := ${realpath protos}
OUTPUT_DIR := ${realpath typedefs}
FIND_FILE := ${wildcard ${OUTPUT_DIR}/*.ts}
PROTOC_GEN_GRPC := protoc-gen-grpc

###########################################################
####=======================================================
#### GENERATE PROTO FILE FOR LINUX/MAC OR WINDOWS FOR grpc
####=======================================================
###########################################################

protocgen:
ifneq (${FIND_FILE}, )
	#remove old all files typedefs
	rm ${OUTPUT_DIR}/**.{ts,js}

	#generate protofile typedefs if file not exist
	${PROTOC_GEN_GRPC} \
	--js_out=import_style=commonjs,binary:${OUTPUT_DIR} \
	--grpc_out=${OUTPUT_DIR} \
	--ts_out=protoc-gen-grpc-ts:${OUTPUT_DIR} \
	--proto_path ${INPUT_DIR} ${INPUT_DIR}/*.proto

else
	#generate protofile typedefs if file not exist
	${PROTOC_GEN_GRPC} \
	--js_out=import_style=commonjs,binary:${OUTPUT_DIR} \
	--grpc_out=${OUTPUT_DIR} \
	--ts_out=protoc-gen-grpc-ts:${OUTPUT_DIR} \
	--proto_path ${INPUT_DIR} ${INPUT_DIR}/*.proto
endif
 ```
 
 ### Author
 
 -  **[Restu Wahyu Saputra](https://github.com/restuwahyu13)**
