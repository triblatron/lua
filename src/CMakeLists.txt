ADD_LIBRARY( lua54 SHARED lapi.c lcode.c lctype.c ldebug.c ldo.c ldump.c lfunc.c lgc.c llex.c lmem.c lobject.c lopcodes.c lparser.c lstate.c lstring.c ltable.c ltm.c lundump.c lvm.c lzio.c lauxlib.c lbaselib.c lcorolib.c ldblib.c liolib.c lmathlib.c loadlib.c loslib.c lstrlib.c ltablib.c lutf8lib.c linit.c )

IF (CMAKE_SYSTEM MATCHES "Windows")
set_target_properties( lua54 PROPERTIES DEFINE_SYMBOL LUA_BUILD_AS_DLL )
ENDIF()
ADD_EXECUTABLE( lua lua.c )
SET( LIBS lua54 )
IF (CMAKE_SYSTEM MATCHES "Linux")
LIST(APPEND LIBS "m;dl")
ENDIF()
TARGET_LINK_LIBRARIES( lua ${LIBS})

INSTALL( FILES lua.h luaconf.h lualib.h lauxlib.h lua.hpp DESTINATION include/lua5.4 )
INSTALL( TARGETS lua LIBRARY DESTINATION lib RUNTIME DESTINATION bin )
# Windows import libraries are of type ARCHIVE.
INSTALL( TARGETS lua54 LIBRARY DESTINATION lib RUNTIME DESTINATION bin ARCHIVE DESTINATION lib)