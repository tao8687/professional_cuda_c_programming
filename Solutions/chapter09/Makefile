CU_APPS=simpleMultiGPUEvents simpleP2P_PingPong simpleP2P_PingPongDefault \
		simple2DFDModified simpleMultiGPUEvents-initial
C_APPS=simpleP2P_Pageable simpleP2P-async

ARCH= -gencode arch=compute_35,code=sm_35 \
      -gencode arch=compute_50,code=[sm_50,compute_50] \
      -gencode arch=compute_52,code=[sm_52,compute_52] \
	    -gencode arch=compute_61,code=[sm_61,compute_61]
		
# GeForce RTX 3070, 3080, 3090
# ARCH= -gencode arch=compute_86,code=[sm_86,compute_86]

# Kepler GeForce GTX 770, GTX 760, GT 740
# ARCH= -gencode arch=compute_30,code=sm_30

# Tesla A100 (GA100), DGX-A100, RTX 3080
# ARCH= -gencode arch=compute_80,code=[sm_80,compute_80]

# Tesla V100-arch=sm_20
# ARCH= -gencode arch=compute_70,code=[sm_70,compute_70]

# GeForce RTX 2080 Ti, RTX 2080, RTX 2070, Quadro RTX 8000, Quadro RTX 6000, Quadro RTX 5000, Tesla T4, XNOR Tensor Cores
# ARCH= -gencode arch=compute_75,code=[sm_75,compute_75]

# Jetson XAVIER
# ARCH= -gencode arch=compute_72,code=[sm_72,compute_72]

# GTX 1080, GTX 1070, GTX 1060, GTX 1050, GTX 1030, Titan Xp, Tesla P40, Tesla P4
# ARCH= -gencode arch=compute_61,code=sm_61 -gencode arch=compute_61,code=compute_61

# GP100/Tesla P100 - DGX-1
# ARCH= -gencode arch=compute_60,code=sm_60

# For Jetson TX1, Tegra X1, DRIVE CX, DRIVE PX - uncomment:
# ARCH= -gencode arch=compute_53,code=[sm_53,compute_53]

# For Jetson Tx2 or Drive-PX2 uncomment:
# ARCH= -gencode arch=compute_62,code=[sm_62,compute_62]

# For Tesla GA10x cards, RTX 3090, RTX 3080, RTX 3070, RTX A6000, RTX A40 uncomment:
# ARCH= -gencode arch=compute_86,code=[sm_86,compute_86]

all: ${C_APPS} ${CU_APPS}

simpleP2P_Pageable: simpleP2P_Pageable.c
	gcc -O2 -std=c99 -I${MPI_HOME}/include -I${CUDA_HOME}/include -L${MPI_HOME}/lib -L${CUDA_HOME}/lib64 -lcudart -lmpi -o simpleP2P_Pageable simpleP2P_Pageable.c

simpleP2P-async: simpleP2P-async.c
	gcc -O2 -std=c99 -I${MPI_HOME}/include -I${CUDA_HOME}/include -L${MPI_HOME}/lib -L${CUDA_HOME}/lib64 -lcudart -lmpi -o simpleP2P-async simpleP2P-async.c

%: %.cu
	nvcc -O2 ${ARCH} -o $@ $<
%: %.c
	gcc -O2 -std=c99 -lm -o $@ $<
clean:
	rm -f ${CU_APPS} ${C_APPS}
