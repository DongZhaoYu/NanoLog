#####################################################################
#
# This is a sample makefile on how to compile with C++17 NanoLog
# (i.e. Non-preprocessor version of NanoLog).
#
# The main requirements are
#  (a) include the NanoLog runtime directory with -I when compiling
#  (b) link the NanoLog runtime library (-lNanoLog) and external
#      libraries (-lpthread -lrt) into the final executable
#
#####################################################################

# -DNDEBUG and -O3 should always be passed for high performance
CXXFLAGS= -std=c++17 -DNDEBUG -O3 -g
CXX=g++

NANOLOG_RUNTIME_DIR=../runtime

all: sampleApplication decompressor

# (a) Make the user object files include the NanoLog header (-I)
%.o: %.cc
	$(CXX) -I $(NANOLOG_RUNTIME_DIR) -c -o $@ $< $(CXXFLAGS)

# Make the final application linking NanoLog, pthreads, and POSIX aio
sampleApplication: main.o libNanoLog.a
	$(CXX) $(CXXFLAGS) -o sampleApplication main.o -L. -lNanoLog -lpthread -lrt

clean:
	@rm -f *.o sampleApplication /tmp/logFile compressedLog




# These (optional) rules copy in the NanoLog library and decompressor.
# An alternative is to run "make" in the runtime directory and copy out
# the library and decompressor executable.
libNanoLog.a:
	$(MAKE) libNanoLog.a -C $(NANOLOG_RUNTIME_DIR)
	cp $(NANOLOG_RUNTIME_DIR)/libNanoLog.a .

decompressor:
	$(MAKE) decompressor -C $(NANOLOG_RUNTIME_DIR)
	cp $(NANOLOG_RUNTIME_DIR)/decompressor .

# Cleans up the NanoLog files as well
clean-all: clean
	@rm -f $(NANOLOG_RUNTIME_DIR)/*.o $(NANOLOG_RUNTIME_DIR)/libNanoLog.a libNanoLog.a decompressor