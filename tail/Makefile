
BINARIES=tail.exe

!INCLUDE "..\config\common.mk"

!IF $(PDB)==1
LINKPDB=/Pdb:tail.pdb
!ENDIF

CFLAGS=$(CFLAGS) -DTAIL_VER_MAJOR=$(TAIL_VER_MAJOR) -DTAIL_VER_MINOR=$(TAIL_VER_MINOR)

BIN_OBJS=\
	 tail.obj         \

MOD_OBJS=\
	 mod_tail.obj     \

compile: $(BIN_OBJS) builtins.lib

tail.exe: $(BIN_OBJS) ..\lib\yorilib.lib ..\crt\yoricrt.lib
	@echo $@
	@$(LINK) $(LDFLAGS) -entry:$(YENTRY) $(BIN_OBJS) $(LIBS) $(CRTLIB) ..\lib\yorilib.lib -version:$(TAIL_VER_MAJOR).$(TAIL_VER_MINOR) $(LINKPDB) -out:$@

mod_tail.obj: tail.c
	@echo $@
	@$(CC) -c -DYORI_BUILTIN=1 $(CFLAGS) -Fo$@ tail.c

builtins.lib: $(MOD_OBJS)
	@echo $@
	@$(LIB32) $(LIBFLAGS) $(MOD_OBJS) -out:$@
