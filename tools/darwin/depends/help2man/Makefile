include ../Makefile.include

# lib name, version
APPNAME=help2man
VERSION=1.38.2
SOURCE=$(APPNAME)-$(VERSION)
ARCHIVE=$(SOURCE).tar.gz

# configuration settings
export PATH:=$(TOOLCHAIN)/bin:$(PATH)
CONFIGURE=./configure --prefix=$(TOOLCHAIN)

APP=$(SOURCE)/$(APPNAME)

all: $(APP) .installed

$(TARBALLS_LOCATION)/$(ARCHIVE):
	$(RETRIEVE_TOOL) $(RETRIEVE_TOOL_FLAGS) $(BASE_URL)/$(ARCHIVE)

$(SOURCE): $(TARBALLS_LOCATION)/$(ARCHIVE)
	rm -rf $(SOURCE)
	$(ARCHIVE_TOOL) $(ARCHIVE_TOOL_FLAGS) $(TARBALLS_LOCATION)/$(ARCHIVE)
	echo $(SOURCE) > .gitignore
	sed -ie "s/-shared/-dynamiclib/g" "$(SOURCE)/Makefile.in"
	cd $(SOURCE); $(CONFIGURE)

$(APP): $(SOURCE)
	make -C $(SOURCE)

.installed:
	make -C $(SOURCE) install
	touch $@

clean:
	make -C $(SOURCE) clean
	rm -f .installed

distclean::
	rm -rf $(SOURCE) .installed
