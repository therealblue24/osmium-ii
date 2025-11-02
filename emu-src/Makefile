# set this to 'yes' for release mode
RELEASE = no
CC ?= cc
# binary directory
BINDIR = bin
# app name
APP = osmium-ii-emu

CFLAGS = -std=c11 -Wall -Wextra -Isrc -Iinclude -Ilib -g3
CFLAGS += -MMD -MP
LDFLAGS = 

# Optimize code (-O2)
RELEASE ?= no
# -Weverything but sane
CODE_REVIEW ?= no
# debug mode
SANITIZERS ?= no

ifeq ($(RELEASE), yes)
	CFLAGS += -O2
endif

ifeq ($(CODE_REVIEW), yes)
	# Enable EVERYTHING.
    CFLAGS += -Weverything
    # We are using C
    CFLAGS += -Wno-unsafe-buffer-usage
    # We don't care about trailing ;
    CFLAGS += -Wno-extra-semi-stmt
    # We are using C11
    CFLAGS += -Wno-declaration-after-statement
    # I honestly don't care right know
    CFLAGS += -Wno-padded
    # I don't care
    CFLAGS += -Wno-date-time
    # I don't care
    CFLAGS += -Wno-float-equal
endif

ifeq ($(SANITIZERS), yes)
	CFLAGS += -fsanitize=undefined,address,leak
	LDFLAGS += -fsanitize=undefined,address,leak
endif

# src files
SRC = $(shell find src -name "*.c")
# src/*.c -> bin/*.c
OBJ = $(SRC:src/%.c=$(BINDIR)/%.o)
# dependencies
DEP = $(OBJ:.o=.d)

# arguments to pass to program w/ `make test`
TESTARGS =

FMTFILES = $(SRC) $(shell find src -name "*.h") $(shell find include -name "*.h")

.PHONY: dirs build test link test

all: dirs build link

dirs:
	@# Create bin dir
	@mkdir -p $(BINDIR)

# compile each single file
$(BINDIR)/%.o: src/%.c
	@echo "compiling $<"
	@$(CC) -o $@ -c $< $(CFLAGS)

# include deps
-include $(DEP)

build: dirs $(OBJ)

$(BINDIR)/$(APP): link
	
link: build
	@echo "linking $(APP)"
	@$(CC) -o $(BINDIR)/$(APP) $(LDFLAGS) $(OBJ)
	@echo "made $(APP)"

clean:
	@echo "cleaning"
	rm -rf $(BINDIR)
	@echo "cleaned"

test: $(BINDIR)/$(APP)
	@$(BINDIR)/$(APP) $(TESTARGS)
