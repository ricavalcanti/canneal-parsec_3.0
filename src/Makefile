# Makefile for parallel simulated annealer
GPROFFLAGS = -pg
PREFIX=${PARSECDIR}/pkgs/kernels/canneal/inst/${PARSECPLAT}

TARGET=canneal
LIBS:=$(LIBS) -lm

ifdef version
  ifeq "$(version)" "pthreads"
    CXXFLAGS+=-DENABLE_THREADS -pthread
  endif
endif

all:
	$(CXX) $(CXXFLAGS) annealer_thread.cpp -c -o annealer_thread.o
	$(CXX) $(CXXFLAGS) rng.cpp -c -o rng.o
	$(CXX) $(CXXFLAGS) netlist.cpp -c -o netlist.o
	$(CXX) $(CXXFLAGS) main.cpp -c -o main.o
	$(CXX) $(CXXFLAGS) netlist_elem.cpp -c -o netlist_elem.o
	$(CXX) $(CXXFLAGS) $(LDFLAGS) *.o $(LIBS) -o $(TARGET)
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

