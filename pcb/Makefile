all: fabrication/backplane.kicad_pcb fabrication/jumper.kicad_pcb

fabrication:
	mkdir -p fabrication

fabrication/backplane.kicad_pcb: pdu.kicad_pcb fabrication
	kikit separate --source 'annotation; ref: B1' $< $@

fabrication/jumper.kicad_pcb: pdu.kicad_pcb fabrication
	kikit separate --source 'annotation; ref: B2' $< $@
