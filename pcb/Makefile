KICAD_CLI := kicad-cli
ifeq ($(shell uname -s),Darwin)
	KICAD_CLI := /Applications/KiCad/KiCad.app/Contents/MacOS/kicad-cli
endif

SCHEMATIC  := pdu.kicad_sch
PCB        := pdu.kicad_pcb
BOARDS_DIR := boards
FAB_DIR    := fabrication
BOARD_REFS := backplane:B1 jumper:B2

.PHONY: erc
erc:
	$(KICAD_CLI) sch erc --exit-code-violations $(SCHEMATIC)

.PHONY: drc
drc:
	$(KICAD_CLI) pcb drc --exit-code-violations $(PCB)

.PHONY: boards
boards:
	mkdir -p $@

$(BOARDS_DIR)/%.kicad_pcb: boards
	@ref=$$(echo $(BOARD_REFS) | tr ' ' '\n' | grep "^$*" | cut -d: -f2); \
	kikit separate --source "annotation; ref: $$ref" $(PCB) $@

$(FAB_DIR)/jlcpcb/%: $(BOARDS_DIR)/%.kicad_pcb
	mkdir -p $@
	kikit fab jlcpcb --assembly --schematic $(SCHEMATIC) $< $@

$(FAB_DIR)/pcbway/%: $(BOARDS_DIR)/%.kicad_pcb
	mkdir -p $@
	kikit fab pcbway --assembly --schematic $(SCHEMATIC) $< $@
