include_defs('//BUCKAROO_DEPS')

def merge_dicts(x, y):
  z = x.copy()
  z.update(y)
  return z

genrule(
  name = 'config',
  out = 'config.h',
  cmd = 'touch $OUT',
)

macos_preprocessor_flags = [
  '-DVERSION="1.3.3"',
  '-DHAVE_DLFCN_H=1',
  '-DHAVE_GETTIMEOFDAY=1',
  '-DHAVE_INTTYPES_H=1',
  '-DHAVE_MALLOC=1',
  '-DHAVE_MEMORY_H=1',
  '-DHAVE_MEMSET=1',
  '-DHAVE_REALLOC=1',
  '-DHAVE_STDBOOL_H=1',
  '-DHAVE_STDINT_H=1',
  '-DHAVE_STDLIB_H=1',
  '-DHAVE_STRCHR=1',
  '-DHAVE_STRDUP=1',
  '-DHAVE_STRINGS_H=1',
  '-DHAVE_STRING_H=1',
  '-DHAVE_STRNDUP=1',
  '-DHAVE_STRSTR=1',
  '-DHAVE_SYS_STAT_H=1',
  '-DHAVE_SYS_TIME_H=1',
  '-DHAVE_SYS_TYPES_H=1',
  '-DHAVE_UNISTD_H=1',
  '-DHAVE__BOOL=1',
  '-DUSE_JEMALLOC=1',
]

cxx_library(
  name = 'r3',
  header_namespace = '',
  exported_headers = subdir_glob([
    ('include', '**/*.h'),
    ('include', '**/*.hpp'),
  ]),
  headers = merge_dicts(subdir_glob([
    ('src', '**/*.h'),
  ]), {
    'config.h': ':config',
  }),
  platform_preprocessor_flags = [
    ('default', macos_preprocessor_flags),
    ('^macos.*', macos_preprocessor_flags),
  ],
  srcs = glob([
    'src/**/*.c',
  ], excludes = [
    'src/gvc.c',
    'src/json.c',
  ]),
  deps = BUCKAROO_DEPS,
  visibility = [
    'PUBLIC',
  ],
)

cxx_library(
  name = 'zmalloc',
  header_namespace = '',
  exported_headers = {
    'zmalloc.h': '3rdparty/zmalloc.h',
  },
  headers = {
    'config.h': ':config',
  },
  platform_preprocessor_flags = [
    ('default', macos_preprocessor_flags),
    ('^macos.*', macos_preprocessor_flags),
  ],
  srcs = [
    '3rdparty/zmalloc.c',
  ],
  visibility = [
    'PUBLIC',
  ],
)
