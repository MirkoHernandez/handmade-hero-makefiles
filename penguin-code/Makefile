source_dir=penguin
mkfile_path := $(abspath $(lastword $(MAKEFILE_LIST)))
mkfile_dir := $(dir $(mkfile_path))

days = 	day002 \
	day003 \
	day004 \
	day005 \
	day006 \
	day007 \
	day008 \
	day009 \
	day010 \
	day011 \
	day012 \
	day013 \
	day014 \
	day015 \
	day016 \
	day017 \
	day018 \
	day019

.PHONY: days

$(days):
	cd $(mkfile_dir)/$(source_dir); \
	git worktree add -f  ../days/$@ $@; \
        sed -i -e 's;../../build;../build;' $(mkfile_dir)days/$@/code/build.sh
	sed -i -e 's;../handmade/;../;' $(mkfile_dir)days/$@/code/build.sh
