CXX=g++
CXXFLAGS=-lOpenCL -DCL_HPP_MINIMUM_OPENCL_VERSION=110 -I./

BINARIES=platform tiny_clinfo my_first_kernel verbose read_cl read_bincl read_elfcl buffer event_unorder event_order profiling
all: $(BINARIES)

run: $(addprefix run_, $(BINARIES))

clean:
	rm -f -- $(BINARIES)
	rm -f -- hwv.bin *.o dump_bin
	
platform: platform.cpp
	$(CXX) $@.cpp $(CXXFLAGS) -o $@

run_platform: platform
	./$<


tiny_clinfo: tiny_clinfo.cpp
	    $(CXX) $@.cpp $(CXXFLAGS) -o $@

run_tiny_clinfo: tiny_clinfo
	    ./$<


my_first_kernel: my_first_kernel.cpp
	$(CXX) $@.cpp $(CXXFLAGS) -o $@

run_my_first_kernel: my_first_kernel
	./$< 0 0 10 1


verbose: verbose.cpp
	$(CXX) $@.cpp $(CXXFLAGS) -o $@

run_verbose: verbose
	./$< 0 0 10 1


read_cl: hwv.cl read_cl.cpp
	$(CXX) $@.cpp $(CXXFLAGS) -o $@

run_read_cl: read_cl
	./$< 0 0 10 1


hwv.bin: hwv.cl dump_bin
	./dump_bin 0 0 hwv.cl hwv.bin

read_bincl: read_bincl.cpp
	$(CXX) $@.cpp $(CXXFLAGS) -o $@

run_read_bincl: read_bincl hwv.bin
	./$< 0 0 10 1

dump_bin: dump_bin.cpp
	$(CXX) $@.cpp $(CXXFLAGS) -o $@

hwv.bin.o: hwv.bin
	objcopy --input binary --output elf64-x86-64 --binary-architecture i386 --rename-section .data=.rodata,CONTENTS,ALLOC,LOAD,READONLY,DATA hwv.bin hwv.bin.o

read_elfcl: read_elfcl.cpp hwv.bin.o
	$(CXX) $^ $(CXXFLAGS) -o $@

run_read_elfcl: read_elfcl
	./$< 0 0 10 1



buffer: buffer.cpp
	    $(CXX) $@.cpp $(CXXFLAGS) -o $@

run_buffer: buffer
	    ./$< 0 0 10 1



event_unorder: event_unorder.cpp
	$(CXX) $@.cpp $(CXXFLAGS) -o $@

run_event_unorder: event_unorder
	./$< 0 0 1 1 10


event_order: event_order.cpp
	$(CXX) $@.cpp $(CXXFLAGS) -o $@

run_event_order: event_order
	./$< 0 0 1 1 10




profiling: profiling.cpp
	    $(CXX) $@.cpp $(CXXFLAGS) -o $@

run_profiling: profiling
	    ./$< 0 0 1 1 10

