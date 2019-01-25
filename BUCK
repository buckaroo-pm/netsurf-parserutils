load('//:buckaroo_macros.bzl', 'buckaroo_deps')
load('//:subdir_glob.bzl', 'subdir_glob')

genrule(
  name = 'aliases-inc',
  out = 'aliases.inc',
  srcs = [
    'build/Aliases',
    'build/make-aliases.pl',
  ],
  cmd = ' && '.join([
    'cp -r $SRCDIR/. $TMP',
    'cd $TMP',
    'mkdir -p src/charset',
    'perl build/make-aliases.pl',
    'cp $TMP/src/charset/aliases.inc $OUT',
  ]),
)

cxx_library(
  name = 'parserutils',
  header_namespace = '',
  exported_headers = subdir_glob([
    ('include', '**/*.h'),
  ]),
  headers = dict(
    subdir_glob([
      ('src', '**/*.h'),
    ]).items() + [
      ('aliases.inc', ':aliases-inc'),
    ]
  ),
  srcs = glob([
    'src/**/*.c',
  ]),
  deps = buckaroo_deps(),
  visibility = [
    'PUBLIC',
  ],
)
