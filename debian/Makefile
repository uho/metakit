
.PHONY: all
all: tcl-metakit_2.4.9.8_amd64.deb tcl-metakit_2.4.9.8_armhf.deb tcl-metakit_2.4.9.8_armv7.deb

tcl-metakit_2.4.9.8_amd64.deb: qemu-arm-static Dockerfile makeDeb
	./makeDeb amd64

tcl-metakit_2.4.9.8_armhf.deb: qemu-arm-static Dockerfile makeDeb
	./makeDeb armhf

tcl-metakit_2.4.9.8_armv7.deb: qemu-arm-static Dockerfile makeDeb
	./makeDeb armv7

qemu-arm-static:
	docker run --name qemu-user-static --privileged multiarch/qemu-user-static --reset -p yes
	docker cp qemu-user-static:/usr/bin/qemu-arm-static qemu-arm-static
	docker rm qemu-user-static
	touch qemu-arm-static

.PHONY: clean
clean: 
	rm -f tcl-metakit_*.deb
	rm -f qemu-arm-static
