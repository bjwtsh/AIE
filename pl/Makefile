# Copyright (C) 2023 Advanced Micro Devices, Inc
#
# SPDX-License-Identifier: MIT

PLATFORM := xilinx_vck5000_gen4x8_qdma_2_202220_1
TARGET := hw
FREQ := 250

XSA = $(strip $(patsubst %.xpfm, % , $(shell basename $(PLATFORM))))

BUILD_DIR = build.$(XSA).$(TARGET)
VPP_FLAGS = -t $(TARGET) --platform $(PLATFORM)# --save-temps
VPP_FLAGS += --kernel_frequency $(FREQ)

kernel_list = pl_mm2s pl_s2mm
#list of .xo files
BINARY_OBJS = $(addprefix $(BUILD_DIR)/, $(addsuffix .xo, $(kernel_list)))

all: $(BINARY_OBJS)

$(BUILD_DIR)/pl_mm2s.xo: src/pl_mm2s.cpp
	#-c|--compile 	编译模式必须选项
	#-g		生成代码用于在软件仿真期间进行内核调试。该选项可用于添加相应的功能特性，以促进内核编辑时的调试。
	#-o|--output	指定 v++ 命令所生成的输出文件的名称。
	#$@		规则的目标文件名
	#$^		所有依赖文件列表
	
	v++ $(VPP_FLAGS) -k $(subst $(BUILD_DIR)/,,$(subst .xo,,$@)) -c -g -o $@ $^

$(BUILD_DIR)/pl_s2mm.xo: src/pl_s2mm.cpp
	v++ $(VPP_FLAGS) -k $(subst $(BUILD_DIR)/,,$(subst .xo,,$@)) -c -g -o $@ $^

clean:
	rm -rf $(BUILD_DIR) *.log *.jou .Xil/
