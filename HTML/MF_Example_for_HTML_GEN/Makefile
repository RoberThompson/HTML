#Lines starting with the pund sign are commented out.
#
#These are te options that may need tweaking.

EXECUTABLE = myprogram
LINKCC = $(CC)
OTHERS = page1.html page2.html
OTHERDEPS = page1.d page2.d

#you can modify the below as well, but probably
#won't need to.
#

#CC is for the name of the C compiler. CPPFLAGS denotes pre-processor
#flags, such as -I options. CFLAGS denotes flags for the c
#compiler.
#CXXFLAGS denotes flags for the C++ compiler.
#you may add additional settings here, such as PFLAGS, if you are
#using other languages such as Pascal.

CPPFLAGS =

LDFLAGS=

CC = gcc
CLFAGS = -Wall -O2

CXX = g++
CXXFLAGS = $(CFLAGS)


SRCS := $(wildcard *.c) $(wildcard *.cc) $(wildcard *.C)
OBJS := $(patsubst %.c,%.o,$(wildcard *.c)) \
	$(patsubst %.cc,%.o,$(wildcard *.cc)) \
	$(patsubst %.C,%.o,$(wildcard *.C))
DEPS := $(patsubst %.o,%.d,$(OBJS)) $(OTHERDEPS)

#"all" is the default target. Simly make it point to myprogram.

all: $(EXECUTABLE) $(OTHERS)

#define the components of the program, and how to link them together.
#These components are efined as dependencies; that is,
# they must be made up-to-date before the code is linked.

$(EXECUTABLE): $(DEPS) $(OBJS)
	$(LINKCC) $(LDFLAGS) -o $(EXECUTABLE) $(OBJS)

#Specify that the dependency files depend on the C source files.

%.d: %.c
	$(CC) -M $(CPPFLAGS) $< > $@
	$(CC) -M $(CPPFLAGS) $< | sed s/\\.0/.d/ > $@

%.d: %.cc
	$(CXX) -M $(CPPFLAGS) $< > $@
	$(CXX) -M $(CPPFLAGS) $< | sed s/\\.o/.d/ > $@

%.d: %.C
	$(CXX) -M $(CPPFLAGS) $< > $@
	$(CXX) -M $(CPPFLAGS) $< | sed s/\\.o/.d/ > $@

%.d: %.mac
	cpp -M $< |sed s/\\.mac\\.o/.html/ > $@
	cpp -M $< | sed s/\\.mac\\.o/.d/ > $@

%.html: %.mac
	cpp -P < $< > $@

clean:
	-rm $(OBJS) $(EXECUTABLE) $(DEPS) $(OTHERS) *~

explain:
	@echo "The folloeing information represents your program"
	@echo "Final executable name: $(EXECUTABLE)"
	@echo "Other generated files: $(OTHERS)"
	@echo "Source files: $(SRCS)"
	@echo "Object files: $(OBJS)"
	@echo "Dependency files: $(DEPS)"

depend: $(DEPS)
	@echo "Dependencies are now up-to-date."

-include $(DEPS)
