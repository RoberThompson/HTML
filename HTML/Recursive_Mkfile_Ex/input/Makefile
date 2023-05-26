#
#These are the options that may need tweaking.

OTHERS =
OTHERDEPS =
DIRS =

#You can modify the below as well, but probably
#won't need to.
#

#CC is for the name of the C compiler. CPPFLAGS denotes
#preprocessor flags, such as -I options. CFLAGS denotes flags
#for the C compiler.
#CXXFLAGS denotes flags for the C++ comppiler. You may add
#additional settings here, such a PFLAGS,
#if you are using other languages such as Pascal.

SRCS := $(wildcard *.c) $(wildcard *.cc) $(wildcard *.C)
OBJS := $(patsubst %.c,%.o,$(wildcard *.c)) \
	$(patsubst %.cc,%.o,$(wildcard *.cc)) \
	$(patsubst %.C,%.o,$(wildcard *.C))
DEPS := $(patsubst %.o,%.d,$(OBJS)) $(OTHERDEPS)

#"all" is the default target. Simply make it point to myprogram.

all: $(OBJS) $(OTHERS) $(DIRS)

#$(DIRS):
#	$(MAKE) -C $<

#Define the components of the program, and how to link them
#together. These components are defined as dependencies; that
#is, they must be made up-to-date before the code is linked.

#Specify that the dependency files depend on the c source files.

%.d: %.c
	$(CC) -M $(CPPFLAGS) $< > $@
	$(CC) -M $(CPPFLAGS) $< | sed s/\\.o/.d/ > $@

%.d: %.cc
	$(CXX) -M $(CPPFLAGS) $< > $@
	$(CXX) -M $(CPPFLAGS) $< | sed s/\\.o/.d/ > $@

%.d: %.C
	$(CXX) -M $(CPPFLAGS) $< > $@
	$(CXX) -M $(CPPFLAGS) $< | sed s/\\.o/.d/ > $@

%.d: %.mac
	cpp -M $< | sed s/\\.mac\\.o/.html/ > $@
	cpp -M $< | sed s/\\.mac\\.o/.d/ > $@

%html: %.mac
	cpp -P < $< > $@

clean:
	-rm $(OBJS) $(EXECUTABLE) $(DEPS) $(OTHERS) *~

explain:
	@echo "The following information represents your program:"
	@echo "Other generated files: $(OTHERS)"
	@echo "Source files: $(SRCS)"
	@echo "Object files: $(OBJS)"
	@echo "Dependency files: $(DEPS)"

depend: $(DEPS)

-include $(DEPS)
