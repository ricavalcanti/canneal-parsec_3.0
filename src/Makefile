# Makefile for parallel simulated annealer
GPROFFLAGS = -pg
OPENMPFLAG = -fopenmp
PREFIX=${PARSECDIR}/pkgs/kernels/canneal/inst/${PARSECPLAT}

TARGET=canneal
LIBS:=$(LIBS) -lm

ifdef version
  ifeq "$(version)" "pthreads"
    CXXFLAGS+=-DENABLE_THREADS -pthread
  endif
endif

all:
	$(CXX) $(OPENMPFLAG) $(CXXFLAGS) annealer_thread.cpp -c -o annealer_thread.o
	$(CXX) $(OPENMPFLAG) $(CXXFLAGS) rng.cpp -c -o rng.o
	$(CXX) $(OPENMPFLAG) $(CXXFLAGS) netlist.cpp -c -o netlist.o
	$(CXX) $(OPENMPFLAG) $(CXXFLAGS) main.cpp -c -o main.o
	$(CXX) $(OPENMPFLAG) $(CXXFLAGS) netlist_elem.cpp -c -o netlist_elem.o
	$(CXX) $(OPENMPFLAG) $(CXXFLAGS) $(LDFLAGS) *.o $(LIBS) -o $(TARGET)
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

