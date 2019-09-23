# Makefile for parallel simulated annealer
GPROFFLAGS = -pg
VECTORIZEFLAGS=  -ftree-vectorize -ftree-vectorizer-verbose=1
#VECTORIZEFLAGS=  -ftree-vectorize -fopt-info-vec-missed -O2
PREFIX=${PARSECDIR}/pkgs/kernels/canneal/inst/${PARSECPLAT}

TARGET=canneal
LIBS:=$(LIBS) -lm

ifdef version
  ifeq "$(version)" "pthreads"
    CXXFLAGS+=-DENABLE_THREADS -pthread
  endif
endif

all:
	$(CXX) $(CXXFLAGS) $(VECTORIZEFLAGS) annealer_thread.cpp -c -o annealer_thread.o
	$(CXX) $(CXXFLAGS) $(VECTORIZEFLAGS) rng.cpp -c -o rng.o
	$(CXX) $(CXXFLAGS) $(VECTORIZEFLAGS) netlist.cpp -c -o netlist.o
	$(CXX) $(CXXFLAGS) $(VECTORIZEFLAGS) main.cpp -c -o main.o
	$(CXX) $(CXXFLAGS) $(VECTORIZEFLAGS) netlist_elem.cpp -c -o netlist_elem.o
	$(CXX) $(CXXFLAGS) $(LDFLAGS) $(VECTORIZEFLAGS) *.o $(LIBS) -o $(TARGET)
prof:
	$(CXX) $(CXXFLAGS) $(GPROFFLAGS) annealer_thread.cpp -c -o annealer_thread.o
	$(CXX) $(CXXFLAGS) $(GPROFFLAGS) rng.cpp -c -o rng.o
	$(CXX) $(CXXFLAGS) $(GPROFFLAGS) netlist.cpp -c -o netlist.o
	$(CXX) $(CXXFLAGS) $(GPROFFLAGS) main.cpp -c -o main.o
	$(CXX) $(CXXFLAGS) $(GPROFFLAGS) netlist_elem.cpp -c -o netlist_elem.o
	$(CXX) $(CXXFLAGS) $(LDFLAGS) $(GPROFFLAGS) *.o $(LIBS) -o prof.out
clean:
	rm -f *.o $(TARGET)

install:
	mkdir -p $(PREFIX)/bin
	cp -f $(TARGET) $(PREFIX)/bin/$(TARGET)

