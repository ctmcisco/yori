
BINARIES=ypath.exe

!INCLUDE "..\config\common.mk"

!IF $(PDB)==1
LINKPDB=/Pdb:ypath.pdb
!ENDIF

CFLAGS=$(CFLAGS) -DPATH_VER_MAJOR=$(PATH_VER_MAJOR) -DPATH_VER_MINOR=$(PATH_VER_MINOR)

BIN_OBJS=\
	 path.obj        \

MOD_OBJS=\
	 mod_path.obj    \

compile: $(BIN_OBJS) builtins.lib

ypath.exe: $(BIN_OBJS) ..\lib\yorilib.lib ..\crt\yoricrt.lib
	@echo $@
	@$(LINK) $(LDFLAGS) -entry:$(YENTRY) $(BIN_OBJS) $(LIBS) $(CRTLIB) ..\lib\yorilib.lib -version:$(PATH_VER_MAJOR).$(PATH_VER_MINOR) $(LINKPDB) -out:$@

mod_path.obj: path.c
	@echo $@
	@$(CC) -c -DYORI_BUILTIN=1 $(CFLAGS) -Fo$@ path.c

builtins.lib: $(MOD_OBJS)
	@echo $@
	@$(LIB32) $(LIBFLAGS) $(MOD_OBJS) -out:$@

