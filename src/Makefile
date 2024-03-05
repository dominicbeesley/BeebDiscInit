BASICTOOL=basictool

BUILD=../build
HOSTFS=~/hostfs/ddinit

BEM=$(shell cygpath 'E:\Users\dominic\GitHub\b-em\b-em.exe')

TARGETS=$(BUILD)/DomDiskInit.tok
SSD=$(BUILD)/DDInit.ssd

$(shell mkdir -p $(BUILD))

all: $(SSD)

deploy: $(SSD)
	$(shell mkdir -p $(HOSTFS))
	dfs read -i -d $(HOSTFS) $(SSD)

bem: all
	$(BEM) $(shell cygpath -w $(SSD)) -m5 


$(SSD):$(TARGETS) _21BOOT
	dfs form -80 $(SSD)
	dfs add $(SSD) $(TARGETS)
	dfs add $(SSD) _21BOOT
	dfs opt4 -3 $(SSD)

$(BUILD)/DomDiskInit.tok:DomDiskInit.bbc
	basictool -t $< $@
	echo '$.DDINIT FFFF8023 FFFF8023' >$@.inf

clean:
	-rm $(BUILD)/*
