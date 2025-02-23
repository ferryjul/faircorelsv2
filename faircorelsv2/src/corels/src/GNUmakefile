CFLAGS := -g -W -Wall -Wno-unused-parameter -I. -O2 -fno-omit-frame-pointer
LIBS := 
ifndef NGMP
    CFLAGS += -I/usr/local/include -DGMP
    LIBS += -L/usr/local/lib -lgmp
endif

CXXFLAGS := $(CFLAGS)
CPLEX_DIR = /opt/ibm/ILOG/CPLEX_Studio201/cplex/
CXXFLAGS += -I$(CPLEX_DIR)/include

CXX := g++ -std=c++11

DEPSDIR := .deps

CLEAN := corels *~ *.o *.so

all: corels

corels: run.o main.o corels.o pmap.o cache.o rulelib.o utils.o
	$(CXX) $(CXXFLAGS) $^ -o $@ $(LIBS)

main.o: main.cc $(DEPSDIR)/stamp
	$(CXX) $(CXXFLAGS) $(DEPCFLAGS) -c $< -o $@

corels.o: corels.cpp $(DEPSDIR)/stamp
	$(CXX) $(CXXFLAGS) $(DEPCFLAGS) -c $< -o $@

pmap.o: pmap.cpp $(DEPSDIR)/stamp
	$(CXX) $(CXXFLAGS) $(DEPCFLAGS) -c $< -o $@

utils.o: utils.cpp $(DEPSDIR)/stamp
	$(CXX) $(CXXFLAGS) $(DEPCFLAGS) -c $< -o $@

cache.o: cache.cpp $(DEPSDIR)/stamp
	$(CXX) $(CXXFLAGS) $(DEPCFLAGS) -c $< -o $@

rulelib.o: rulelib.cpp $(DEPSDIR)/stamp
	$(CXX) $(CXXFLAGS) $(DEPCFLAGS) -c $< -o $@

run.o: run.cpp $(DEPSDIR)/stamp
	$(CXX) $(CXXFLAGS) $(DEPCFLAGS) -c $< -o $@

$(DEPSDIR)/stamp:
	mkdir -p $(dir $@)
	touch $@

clean:
	$(RM) $(wildcard $(CLEAN))
	$(RM) -r $(DEPSDIR)

DEPFILES := $(wildcard $(DEPSDIR)/*.d)
ifneq ($(DEPFILES),)
include $(DEPFILES)
endif

.PHONY: all clean
.SUFFIXES:
