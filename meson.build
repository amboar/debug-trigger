project('debug-trigger', 'c', license: 'Apache-2.0', version: '0.1')
executable('debug-trigger', 'main.c', install: true)

if get_option('systemd')
	systemd = dependency('systemd')
	unitdir = systemd.get_pkgconfig_variable('systemdsystemunitdir')
	configure_file(input: 'systemd/system/debug-trigger@.service',
		       output: 'debug-trigger@.service',
		       copy: true,
		       install_dir: unitdir)
endif

udev = dependency('udev')
udevdir = udev.get_pkgconfig_variable('udevdir')
udevrules = [
	'p10bmc-debug-trigger-kcs1',
	'p10bmc-debug-trigger-kcs2',
	'p10bmc-debug-trigger-kcs3',
	'p10bmc-debug-trigger-kcs4',
]

foreach rule : udevrules
	if get_option(rule)
		src = 'udev/rules.d/' + rule + '.rules'
		dst = rule + '.rules'
		rulesdir = udevdir + '/rules.d'
		configure_file(input: src, output: dst, copy: true, install_dir: rulesdir)
	endif
endforeach
