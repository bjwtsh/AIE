# Copyright (C) 2023 Advanced Micro Devices, Inc
#
# SPDX-License-Identifier: MIT

#the vitis dir in server
VITIS_DIR := /proj/xbuilds/2023.1_released/installs/lin64/Vitis/2023.1
GCC_DIR := ${VITIS_DIR}/aietools/tps/lnx64/gcc/bin

FLAGS := -Wall -c -g -fmessage-length=0
FLAGS += -std=c++17 -Wno-unknown-pragmas -Wno-unused-label
FLAGS += -Wno-int-to-pointer-cast


INCLUDES +=	-I$(XILINX_VITIS)/aietools/include
INCLUDES +=	-I$(XILINX_VITIS)/include
INCLUDES +=	-I$(XILINX_XRT)/include

LIBS := -lxaiengine -ladf_api_xrt -lxrt_core -lxrt_coreutil -lgcc -lc
LIBS += -lxilinxopencl -lpthread -lrt -ldl -lcrypt -lstdc++ -lOpenCL
LIBS += -Wno-unused-label -Wno-narrowing -DVERBOSE
LIBS += -L$(XILINX_VITIS)/aietools/lib/lnx64.o
LIBS += -L$(XILINX_XRT)/lib/

# =========================================================
# BUILD PRODUCTS
# =========================================================
BUILD_DIR = build
EXECUTABLE = template.exe
# ################ TARGET: make all ################
all: host

# ################ TARGET: make host ################
.PHONY: host
host: $(BUILD_DIR) $(EXECUTABLE)

$(BUILD_DIR): 
	mkdir -p $(BUILD_DIR);

$(EXECUTABLE): $(BUILD_DIR)/host.o
	${GCC_DIR}/g++ $^ $(LIBS) -std=c++17 -o $@
	@echo "COMPLETE: Host application $@ created."

# Create object files
$(BUILD_DIR)/host.o: host.cpp
	${GCC_DIR}/g++ $(FLAGS) $(INCLUDES) -o $@ $^

# ################ TARGET: make clean ################
clean:
	rm -rf $(BUILD_DIR)
	rm -rf *~
	rm -rf .run/
	rm -rf *.csv
	rm -rf *.run_summary
	rm -rf .Xil/
	rm -rf *.log *.jou
	rm -rf $(EXECUTABLE)
