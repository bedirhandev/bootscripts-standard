DATE        := 20140710
VERSION		:= 3.0-${DATE}

ETCDIR		:= /etc
SHELL		:= /bin/bash
EXTDIR		:= ${DESTDIR}${ETCDIR}
MODE		:= 754
DIRMODE		:= 755
CONFMODE	:= 644

all:
	@grep "^install" Makefile | cut -d ":" -f 1
	@echo "dist"
	@echo "Select an appropriate install target from the above list" ; exit 1

.PHONY: dist
dist:
	rm -rf "dist/boot-scripts-cross-lfs-$(VERSION)"
	mkdir -p "dist/boot-scripts-cross-lfs-$(VERSION)"
	tar --exclude dist -c * | tar -x -C "dist/boot-scripts-cross-lfs-$(VERSION)"
	(cd dist; tar -cJf "boot-scripts-cross-lfs-$(VERSION).tar.xz" "boot-scripts-cross-lfs-$(VERSION)")
	rm -rf "dist/boot-scripts-cross-lfs-$(VERSION)"

create-dirs:
	install -d -m ${DIRMODE} ${EXTDIR}/rc.d/rc{0,1,2,3,4,5,6,sysinit}.d
	install -d -m ${DIRMODE} ${EXTDIR}/rc.d/init.d
	install -d -m ${DIRMODE} ${EXTDIR}/sysconfig

create-service-dir:
	install -d -m ${DIRMODE} ${EXTDIR}/sysconfig/network-devices/services

install-boot-scripts: create-dirs create-service-dir
	install -m ${MODE} clfs/init.d/checkfs       		${EXTDIR}/rc.d/init.d/
	install -m ${MODE} clfs/init.d/cleanfs       		${EXTDIR}/rc.d/init.d/
	install -m ${CONFMODE} clfs/init.d/functions ${EXTDIR}/rc.d/init.d/functions
	install -m ${MODE} clfs/init.d/halt          		${EXTDIR}/rc.d/init.d/
	install -m ${MODE} clfs/init.d/localnet      		${EXTDIR}/rc.d/init.d/
	install -m ${MODE} clfs/init.d/mountfs       		${EXTDIR}/rc.d/init.d/
	install -m ${MODE} clfs/init.d/mountkernfs   		${EXTDIR}/rc.d/init.d/
	install -m ${MODE} clfs/init.d/rc            		${EXTDIR}/rc.d/init.d/
	install -m ${MODE} clfs/init.d/reboot        		${EXTDIR}/rc.d/init.d/
	install -m ${MODE} clfs/init.d/sendsignals   		${EXTDIR}/rc.d/init.d/
	install -m ${MODE} clfs/init.d/setclock      		${EXTDIR}/rc.d/init.d/
	install -m ${MODE} clfs/init.d/swap          		${EXTDIR}/rc.d/init.d/
	install -m ${MODE} clfs/init.d/udev          		${EXTDIR}/rc.d/init.d/
	ln -sf ../init.d/sendsignals ${EXTDIR}/rc.d/rc0.d/S60sendsignals
	ln -sf ../init.d/mountfs     ${EXTDIR}/rc.d/rc0.d/S70mountfs
	ln -sf ../init.d/swap        ${EXTDIR}/rc.d/rc0.d/S80swap
	ln -sf ../init.d/halt        ${EXTDIR}/rc.d/rc0.d/S99halt
	ln -sf ../init.d/sendsignals ${EXTDIR}/rc.d/rc6.d/S60sendsignals
	ln -sf ../init.d/mountfs     ${EXTDIR}/rc.d/rc6.d/S70mountfs
	ln -sf ../init.d/swap        ${EXTDIR}/rc.d/rc6.d/S80swap
	ln -sf ../init.d/reboot      ${EXTDIR}/rc.d/rc6.d/S99reboot
	ln -sf ../init.d/mountkernfs ${EXTDIR}/rc.d/rcsysinit.d/S00mountkernfs
	ln -sf ../init.d/udev        ${EXTDIR}/rc.d/rcsysinit.d/S10udev
	ln -sf ../init.d/checkfs     ${EXTDIR}/rc.d/rcsysinit.d/S20checkfs
	ln -sf ../init.d/mountfs     ${EXTDIR}/rc.d/rcsysinit.d/S30mountfs
	ln -sf ../init.d/swap        ${EXTDIR}/rc.d/rcsysinit.d/S40swap
	ln -sf ../init.d/cleanfs     ${EXTDIR}/rc.d/rcsysinit.d/S50cleanfs
	ln -sf ../init.d/setclock    ${EXTDIR}/rc.d/rcsysinit.d/S60setclock
	if [ ! -f ${EXTDIR}/sysconfig/rc          ]; then install -m ${CONFMODE} clfs/sysconfig/rc          ${EXTDIR}/sysconfig/; fi
	if [ ! -f ${EXTDIR}/sysconfig/createfiles ]; then install -m ${CONFMODE} clfs/sysconfig/createfiles ${EXTDIR}/sysconfig/; fi

install-raq2: create-dirs
	install -m ${MODE} clfs/init.d/paneld        ${EXTDIR}/rc.d/init.d/
	ln -sf ../init.d/paneld      ${EXTDIR}/rc.d/rc0.d/K01paneld
	ln -sf ../init.d/paneld      ${EXTDIR}/rc.d/rc1.d/S99paneld
	ln -sf ../init.d/paneld      ${EXTDIR}/rc.d/rc2.d/S99paneld
	ln -sf ../init.d/paneld      ${EXTDIR}/rc.d/rc3.d/S99paneld
	ln -sf ../init.d/paneld      ${EXTDIR}/rc.d/rc4.d/S99paneld
	ln -sf ../init.d/paneld      ${EXTDIR}/rc.d/rc5.d/S99paneld
	ln -sf ../init.d/paneld      ${EXTDIR}/rc.d/rc6.d/K01paneld
	if [ ! -f ${EXTDIR}/sysconfig/lcd          ]; then install -m ${CONFMODE} clfs/sysconfig/lcd-raq2   ${EXTDIR}/sysconfig/lcd; fi

install-raq3: create-dirs
	install -m ${MODE} clfs/init.d/setlcd        ${EXTDIR}/rc.d/init.d/
	ln -sf ../init.d/setlcd      ${EXTDIR}/rc.d/rc0.d/K01setlcd
	ln -sf ../init.d/setlcd      ${EXTDIR}/rc.d/rc1.d/S99setlcd
	ln -sf ../init.d/setlcd      ${EXTDIR}/rc.d/rc2.d/S99setlcd
	ln -sf ../init.d/setlcd      ${EXTDIR}/rc.d/rc3.d/S99setlcd
	ln -sf ../init.d/setlcd      ${EXTDIR}/rc.d/rc4.d/S99setlcd
	ln -sf ../init.d/setlcd      ${EXTDIR}/rc.d/rc5.d/S99setlcd
	ln -sf ../init.d/setlcd      ${EXTDIR}/rc.d/rc6.d/K01setlcd
	if [ ! -f ${EXTDIR}/sysconfig/lcd          ]; then install -m ${CONFMODE} clfs/sysconfig/lcd-raq3   ${EXTDIR}/sysconfig/lcd; fi

install-lcd: create-dirs
	if [ ! -f ${EXTDIR}/sysconfig/lcd          ]; then install -m ${CONFMODE} clfs/sysconfig/lcd        ${EXTDIR}/sysconfig/lcd; fi

install-netboot: create-dirs create-service-dir
	rm -rf ${EXTDIR}/rc.d
	install -d -m ${DIRMODE} ${EXTDIR}/rc.d
	install -m ${MODE} netboot/rc.0         ${EXTDIR}/rc.d/
	install -m ${MODE} netboot/rc.1         ${EXTDIR}/rc.d/
	install -m ${MODE} netboot/rc.sysinit ${EXTDIR}/rc.d/
	if [ ! -f ${EXTDIR}/inittab ]; then install -m ${CONFMODE} netboot/inittab ${EXTDIR}/inittab; fi
	ln -sf ../rc.d/rc.0 ${EXTDIR}/rc.d/rc.6
	ln -sf ../rc.d/rc.1 ${EXTDIR}/rc.d/rc.2
	ln -sf ../rc.d/rc.1 ${EXTDIR}/rc.d/rc.3
	ln -sf ../rc.d/rc.1 ${EXTDIR}/rc.d/rc.4
	ln -sf ../rc.d/rc.1 ${EXTDIR}/rc.d/rc.5

.PHONY: all create-dirs create-service-dir \
	install \
	boot-scripts \
	install-lcd \
	install-raq2 \
	install-raq3
