
# QuickJS SQLite3 binding
add_library(quickjs_sqlite3 SHARED sqlite3.c)
target_compile_definitions(quickjs_sqlite3 PUBLIC JS_SHARED_LIBRARY)
target_include_directories(quickjs_sqlite3 PRIVATE
    ${quickjs_SOURCE_DIR}                       
)

if(TARGET SQLite::SQLite3)
    set(SQLITE3_TARGET SQLite::SQLite3)
else()
    set(SQLITE3_TARGET SQLite3)
endif()

if(MSVC)
    target_compile_options(quickjs_sqlite3 PRIVATE /utf-8)
endif()

target_link_libraries(quickjs_sqlite3
    ${SQLITE3_TARGET}
    qjs
)
