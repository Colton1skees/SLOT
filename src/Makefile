CC= g++
LLVM_CONFIG= llvm-config-15
CPPFLAGS= $(shell $(LLVM_CONFIG) --cppflags) -std=c++17 -fno-rtti -D_GNU_SOURCE -D_DEBUG -D_GLIBCXX_ASSERTIONS -D_LIBCPP_ENABLE_ASSERTIONS -g -O3 -fexceptions

# Add z3 library flags
Z3_LDFLAGS=-lz3

# Use llvm-config to get the necessary flags and libraries
LLVM_LDFLAGS=$(shell $(LLVM_CONFIG) --ldflags)
LLVM_LIBS=$(shell $(LLVM_CONFIG) --system-libs --libs core passes)

LDLIBS=$(Z3_LDFLAGS) $(LLVM_LDFLAGS) $(LLVM_LIBS)  -lrt -ldl -lpthread -lm -lz -ltinfo -lxml2

main: main.o SMTFormula.o SMTNode.o LLVMFunction.o LLVMNode.o
	$(CC) $(CPPFLAGS) -o slot main.o SMTFormula.o SMTNode.o LLVMFunction.o LLVMNode.o $(LDLIBS)
 
main.o: main.cpp SMTFormula.h SMTNode.h LLVMNode.h SLOTExceptions.h #LLVMFunction.h 
	$(CC) $(CPPFLAGS) -c main.cpp
 
SMTNode.o: SMTNode.h SLOTExceptions.h
	$(CC) $(CPPFLAGS) -c SMTNode.cpp

LLVMNode.o: LLVMNode.h SLOTExceptions.h
	$(CC) $(CPPFLAGS) -c LLVMNode.cpp
 
SMTFormula.o: SMTFormula.h SLOTExceptions.h
	$(CC) $(CPPFLAGS) -c SMTFormula.cpp

LLVMFunction.o: LLVMNode.h SLOTExceptions.h
	$(CC) $(CPPFLAGS) -c LLVMFunction.cpp

clean:
	rm *.o