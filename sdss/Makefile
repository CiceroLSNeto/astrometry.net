all:

BASEDIR := ..
COMMON := $(BASEDIR)/util
include $(COMMON)/makefile.common

SO=$(SHAREDLIB_SUFFIX)

.PHONY: all
all: try_lib

try_lib:
	-$(MAKE) lib
.PHONY: try_lib

lib: _cutils$(PYTHON_SO_EXT) cutils.py
.PHONY: lib

MY_DIR := $(PY_BASE_INSTALL_DIR)/sdss

_cutils$(PYTHON_SO_EXT) cutils.py: cutils.i
	python setup.py build_ext -v --inplace --build-temp .

INSTALL_PY := __init__.py common.py dr7.py dr8.py runList-dr8.par \
	dr9.py fields.py runList-dr9.par dr10.py runList-dr10.par

INSTALL_LIB := cutils.py _cutils$(PYTHON_SO_EXT)


install-lib:
	mkdir -p '$(MY_DIR)'
	@for x in $(INSTALL_LIB); do \
		echo cp $$x '$(MY_DIR)'; \
		cp $$x '$(MY_DIR)'; \
	done

.PHONY: install-lib

#install: _cutils$(PYTHON_SO_EXT) cutils.py
# cutils are supposed to be optional, so try but don't fail to build
install:
	@echo Installing in directory '$(MY_DIR)'
	mkdir -p '$(MY_DIR)'
	@for x in $(INSTALL_PY); do \
		echo cp $$x '$(MY_DIR)'; \
		cp $$x '$(MY_DIR)'; \
	done
	@echo "Trying to build (optional) python module..."
	-$(MAKE) lib && $(MAKE) install-lib

.PHONY: install

.PHONY: clean
clean:
	rm -f _cutils$(PYTHON_SO_EXT) cutils_wrap.c cutils.py

