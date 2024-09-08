mkfile_path := $(abspath $(lastword $(MAKEFILE_LIST)))
mkfile_dir := $(dir $(mkfile_path))

source_dir := sdl
handmade_dir := cpp

all = days

days = 	day169 \
	day177 \
	day180 \
	day188 \
	day195 \
	day624 \
	day657

# days that need fixes to compile.
snprintf_days_hd := day195
snprintf_days_h := day177 


# days that require a different SDL library than the provided one.
sdl_days :=  day195

# days that need data dir to run using the assets.
data_v0_days := day195
sources_days :=  day657

const_char_days :=  day177

comment_asset_builder_days :=  day177

# Fixes
define snprintf_fix_hd =
	@echo "[sprintf_fix for handmade_debug.cpp]"
	sed -i -e '16i #define _snprintf_s(a,b,c,...) snprintf(a,b,__VA_ARGS__)\r' $(mkfile_dir)days/$@/cpp/code/handmade_debug.cpp
	sed -i 's/_snprintf_s(TextBuffer, sizeof(TextBuffer),/_snprintf_s(TextBuffer, sizeof(TextBuffer),0,/'  $(mkfile_dir)/days/$@/cpp/code/handmade_debug.cpp
endef

define snprintf_fix_h =
	@echo "[sprintf_fix for handmade.cpp]"
	sed -i -e '16i #define _snprintf_s(a,b,c,...) snprintf(a,b,__VA_ARGS__)\r' $(mkfile_dir)days/$@/cpp/code/handmade.cpp
endef

define sdl_fix =
	@echo "[sdl_fix]"
	sed -i -e 's;`../code/sdl2-64/.*;`sdl2-config --cflags --libs`\";'  $(mkfile_dir)days/$@/code/build.sh
endef

define const_char_fix =
	@echo "[const_char_fix]"  
	sed -i -e 's;char \*FunctionName;const &;'  $(mkfile_dir)days/$@/cpp/code/handmade_debug.h
	sed -i -e 's;debug_record DebugRecordArray.*;extern &;'  $(mkfile_dir)days/$@/cpp/code/handmade_debug.h
endef

define no_werror =
	@echo "[no_error]"  
	sed -i 's/-Werror//'  $(mkfile_dir)days/$@/code/build.sh
endef

define comment_asset_builder =
	@echo "[comment_asset_builder]"  
	sed -i -e 's;c++.*-o test_asset_builder;#&;'  $(mkfile_dir)days/$@/code/build.sh
	sed -i -e 's;.*test_asset_builder;#&;'  $(mkfile_dir)days/$@/code/handmade.sh
	sed -i -e 's;rm.*;#&;'  $(mkfile_dir)days/$@/code/handmade.sh
endef

# Symlink or copy data, sources dir.
define data_v0_ln =
	 @echo "[copy datav0]"  
	 cp -r $(mkfile_dir)data/early_data days/$@/data
	 cp -ra $(mkfile_dir)data/v0_hhas/. days/$@/data
endef

define data_195 =
	 @echo "[copy data created for day195]"  
	 cp -r $(mkfile_dir)data/day195hhas days/$@/data
endef

define sources_ln =
	 @echo "[symlink sources dir]"  
	 ln -s -r $(mkfile_dir)sources days/$@/sources
endef

.PHONY: days

data_195_days := day177


worktree:
	cd $(mkfile_dir)$(source_dir); \
	git worktree add -f ../days/day$(sdlday) day$(sdlday)
	cd $(mkfile_dir)$(handmade_dir); \
	git worktree add -f ../days/day$(sdlday)/cpp day$(day);

$(days):
	cd $(mkfile_dir)$(source_dir); \
	git worktree add -f ../days/$@ $@; \
	cd $(mkfile_dir)$(handmade_dir); \
	git worktree add -f ../days/$@/cpp $@;

	$(if $(filter $@, $(data_v0_days)), $(data_v0_ln))
	$(if $(filter $@, $(data_195_days)), $(data_195))

	$(if $(filter $@, $(sources_days)), $(sources_ln))
	$(if $(filter $@, $(snprintf_days_hd)), $(snprintf_fix_hd))
	$(if $(filter $@, $(snprintf_days_h)), $(snprintf_fix_h))
	$(if $(filter $@, $(comment_asset_builder_days)), $(comment_asset_builder))
	$(if $(filter $@, $(const_char_days)), $(const_char_fix))
	$(if $(filter $@, $(sdl_days)), $(sdl_fix))
	$(no_werror)

rm:
	rm -rf $(mkfile_dir)days/day$(day)	
