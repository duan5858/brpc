BRPC_PATH = ../../
include $(BRPC_PATH)/config.mk
CXXFLAGS = $(CPPFLAGS) -std=c++0x -g -DNDEBUG -O2 -D__const__= -pipe -W -Wall -Werror -fPIC -fno-omit-frame-pointer -Wno-unused-parameter
HDRPATHS = -I$(BRPC_PATH)/output/include $(addprefix -I, $(HDRS))
LIBPATHS = -L$(BRPC_PATH)/output/lib $(addprefix -L, $(LIBS))
STATIC_LINKINGS += -lbrpc

SOURCES = $(wildcard *.cpp)
OBJS = $(addsuffix .o, $(basename $(SOURCES))) 

.PHONY:all
all: rpc_replay

.PHONY:clean
clean:
	@echo "Cleaning"
	@rm -rf rpc_replay $(OBJS)

rpc_replay:$(OBJS)
	@echo "Linking $@"
	@$(CXX) $(LIBPATHS) -Xlinker "-(" $^ -Wl,-Bstatic $(STATIC_LINKINGS) -Wl,-Bdynamic -Xlinker "-)" $(DYNAMIC_LINKINGS) -o $@

%.o:%.cpp
	@echo "Compiling $@"
	@$(CXX) -c $(HDRPATHS) $(CXXFLAGS) $< -o $@

%.o:%.cc
	@echo "Compiling $@"
	@$(CXX) -c $(HDRPATHS) $(CXXFLAGS) $< -o $@
