BUILDDIR = ../build
EXE = $(BUILDDIR)/osmium-ii-emu
INCLUDE = ./inc

SRC = $(wildcard *.c)
HEADERS = $(INCLUDE)/$(wildcard *.h)

.PHONY: all run clean

all: $(EXE)

$(EXE): $(SRC) $(HEADERS) $(BUILDDIR)
	$(CC) $(CFLAGS) $(SRC) -o $@

$(BUILDDIR):
	mkdir $@

run: $(EXE)
	$<

clean:
	rm -rf $(BUILDDIR)
