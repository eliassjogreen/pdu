all: fabrication/backplane.kicad_pcb fabrication/jumper.kicad_pcb

KICAD_CLI := kicad-cli
ifeq ($(shell uname -s),Darwin)
	KICAD_CLI := /Applications/KiCad/KiCad.app/Contents/MacOS/kicad-cli
endif

.PHONY: erc
erc: pdu.kicad_sch
	$(KICAD_CLI) sch erc --exit-code-violations $<

.PHONY: drc
drc: pdu.kicad_pcb
	$(KICAD_CLI) pcb drc --exit-code-violations $<

fabrication:
	mkdir -p fabrication

fabrication/backplane.kicad_pcb: pdu.kicad_pcb fabrication
	kikit separate --source 'annotation; ref: B1' $< $@

fabrication/jumper.kicad_pcb: pdu.kicad_pcb fabrication
	kikit separate --source 'annotation; ref: B2' $< $@
