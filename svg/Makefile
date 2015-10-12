
default_precision=0.2
svg2mod=../../svg2mod/svg2mod.py
module=../modules/mtl.mod

explicit_targets=\
	amoeba-round

THIS_FILE := $(lastword $(MAKEFILE_LIST))
.PHONY: all $(explicit_targets)

svg2mod_opts=-o $(module) --format legacy

all: $(module)

$(module): \
	amoeba-round.svg \
	amoeba-vertical.svg \
	dt-logo.svg \
	dt-logo-d.svg \
	dt-logo-t.svg \
	labels-melvang-moz.svg \
	mtl-braille.svg
	$(foreach svg,$?,$(call make_mod,$(svg)))

# If there's an explicit phony target, recursively call make on that target.
# Otherwise, use default parameters to convert the SVG.
make_mod=$(if \
	$(filter $(basename $(1)),$(explicit_targets)), \
	$(MAKE) -f $(THIS_FILE) $(basename $(1));, \
	$(call do_svg2mod,$(1),$(default_precision)) \
)

# Convert an SVG using the given precision:
do_svg2mod=$(svg2mod) $(svg2mod_opts) \
	-i $(1) --module-name $(basename $(1)) --precision $(2);


.SECONDEXPANSION:

# Custom precision for this SVG to make KiCad 3D renderer happy:
amoeba-round: $$@.svg
	$(call do_svg2mod,$<,0.075)


# vi: set sts=4 sw=4 ts=4: