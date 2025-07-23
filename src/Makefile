# Stockfish 1.0 Makefile
# Updated for compatibility with legacy code

### Configuration ###
EXE     := stockfish
SRC_DIR := .
CXX     ?= g++

### Files ###
SRCS := bitboard.cpp color.cpp pawns.cpp material.cpp endgame.cpp evaluate.cpp \
        main.cpp misc.cpp move.cpp movegen.cpp history.cpp movepick.cpp search.cpp \
        piece.cpp position.cpp square.cpp direction.cpp tt.cpp value.cpp uci.cpp \
        ucioption.cpp mersenne.cpp book.cpp bitbase.cpp san.cpp benchmark.cpp

OBJS := $(addprefix $(SRC_DIR)/, $(SRCS:.cpp=.o))
DEPFILES := $(OBJS:.o=.d)

### Build Flags ###
RELEASE_FLAGS := -O3 -DNDEBUG -flto
DEBUG_FLAGS   := -O0 -g -DDEBUG
# Reduced warnings for legacy code compatibility
WARN_FLAGS    := -Wall -Wno-unused-parameter -Wno-parentheses -Wno-shadow -Wno-misleading-indentation
COMMON_FLAGS  := -fno-exceptions -fno-rtti -fno-strict-aliasing -MMD -MP

# Force-include <cstring> for all files
EXTRA_FLAGS   := -include cstring

CXXFLAGS += $(WARN_FLAGS) $(COMMON_FLAGS) $(EXTRA_FLAGS)
LDFLAGS  += -lm -lpthread

### Targets ###
.PHONY: all debug clean

all: OPTIMIZE = $(RELEASE_FLAGS)
all: $(EXE)

debug: OPTIMIZE = $(DEBUG_FLAGS)
debug: $(EXE)

$(EXE): $(OBJS)
	$(CXX) $(OPTIMIZE) $(LDFLAGS) -o $@ $^ 

%.o: %.cpp
	$(CXX) $(CXXFLAGS) $(OPTIMIZE) -c $< -o $@

clean:
	$(RM) $(EXE) $(OBJS) $(DEPFILES)

### Dependencies ###
-include $(DEPFILES)