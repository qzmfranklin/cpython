licenses(['notice'])

package(default_visibility=['//visibility:public'])

cpython_copts = [
    '-DNDEBUG',
    '-DPy_BUILD_CORE',
    '-O3',
    '-Wall',
    #'-Werror=implicit-function-declaration'
    '-Wextra',
    '-Wno-missing-field-initializers',
    '-Wno-unused-parameter',
    '-Wno-unused-result',
    '-Wno-unused-result',
    '-Wsign-compare',
    '-Wstrict-prototypes',
    '-Wunreachable-code',
    '-fwrapv',
    '-g',
    '-pthread',
    '-std=c99',

    # Required for compiling Python/dynload_shlib.c:
	"-DSOABI='\"cpython-37m-x86_64-linux-gnu\"'",

    # Required for compiling Modules/getpath.c:
    "-DPYTHONPATH='\":\"'",
	"-DPREFIX='\"/usr/local\"'",
	"-DEXEC_PREFIX='\"/usr/local\"'",
	"-DVERSION='\"3.7\"'",
	"-DVPATH='\"\"'",

    #
    r'-DGITVERSION="\"`LC_ALL=C git -C . rev-parse --short HEAD`\""',
    r'-DGITTAG="\"`LC_ALL=C git -C . describe --all --always --dirty`\""',
    r'-DGITBRANCH="\"`LC_ALL=C git -C . name-rev --name-only HEAD`\""',

    # Suppress known warnings.
    '-Wno-unreachable-code',
    '-Wno-sign-compare',
]

# NOTE:
#   Do not run the generated binary, bazel-bin/python, with `bazel run`.  The
#   python program loads a few basic modules such as encoding at startup.  You
#   must set PYTHONPATH to a directory that has those modules.  Usually, the
#   Lib/ directory is good enough.  So you can start running the
#   bazel-bin/python program with
#       PYTHONPATH=Lib bazel-bin/python
cc_binary(
    name = 'python',
    srcs = [
        'Programs/python.c',
    ],
    deps = [
        ':cpython',
    ],
    copts = cpython_copts,
    linkopts = [
        '-lm',
        '-pthread',
        '-ldl',
        '-lutil',
    ],
)

cpython_srcs = [
    'Modules/_codecsmodule.c',
    'Modules/_collectionsmodule.c',
    'Modules/_functoolsmodule.c',
    'Modules/_io/_iomodule.c',
    'Modules/_io/bufferedio.c',
    'Modules/_io/bytesio.c',
    'Modules/_io/fileio.c',
    'Modules/_io/iobase.c',
    'Modules/_io/stringio.c',
    'Modules/_io/textio.c',
    'Modules/_localemodule.c',
    'Modules/_math.c',
    'Modules/_operator.c',
    'Modules/_sre.c',
    'Modules/_stat.c',
    'Modules/_threadmodule.c',
    'Modules/_tracemalloc.c',
    'Modules/_weakref.c',
    'Modules/atexitmodule.c',
    # This file is generated.
    #'Modules/config.c',
    'Modules/errnomodule.c',
    'Modules/faulthandler.c',
    'Modules/gcmodule.c',
    'Modules/getbuildinfo.c',
    'Modules/getpath.c',
    'Modules/hashtable.c',
    'Modules/itertoolsmodule.c',
    'Modules/main.c',
    'Modules/posixmodule.c',
    'Modules/pwdmodule.c',
    'Modules/signalmodule.c',
    'Modules/symtablemodule.c',
    'Modules/timemodule.c',
    'Modules/xxsubtype.c',
    'Modules/zipimport.c',
    'Objects/abstract.c',
    'Objects/accu.c',
    'Objects/boolobject.c',
    'Objects/bytearrayobject.c',
    'Objects/bytes_methods.c',
    'Objects/bytesobject.c',
    'Objects/call.c',
    'Objects/capsule.c',
    'Objects/cellobject.c',
    'Objects/classobject.c',
    'Objects/codeobject.c',
    'Objects/complexobject.c',
    'Objects/descrobject.c',
    'Objects/dictobject.c',
    'Objects/enumobject.c',
    'Objects/exceptions.c',
    'Objects/fileobject.c',
    'Objects/floatobject.c',
    'Objects/frameobject.c',
    'Objects/funcobject.c',
    'Objects/genobject.c',
    'Objects/iterobject.c',
    'Objects/listobject.c',
    'Objects/longobject.c',
    'Objects/memoryobject.c',
    'Objects/methodobject.c',
    'Objects/moduleobject.c',
    'Objects/namespaceobject.c',
    'Objects/object.c',
    'Objects/obmalloc.c',
    'Objects/odictobject.c',
    'Objects/rangeobject.c',
    'Objects/setobject.c',
    'Objects/sliceobject.c',
    'Objects/structseq.c',
    'Objects/tupleobject.c',
    'Objects/typeobject.c',
    'Objects/unicodectype.c',
    'Objects/unicodeobject.c',
    'Objects/weakrefobject.c',
    'Parser/acceler.c',
    'Parser/bitset.c',
    'Parser/firstsets.c',
    'Parser/grammar.c',
    'Parser/grammar1.c',
    'Parser/listnode.c',
    'Parser/metagrammar.c',
    'Parser/myreadline.c',
    'Parser/node.c',
    'Parser/parser.c',
    'Parser/parsetok.c',
    'Parser/pgen.c',
    'Parser/tokenizer.c',
    'Python/Python-ast.c',
    'Python/_warnings.c',
    'Python/asdl.c',
    'Python/ast.c',
    'Python/ast_opt.c',
    'Python/bltinmodule.c',
    'Python/bootstrap_hash.c',
    'Python/ceval.c',
    'Python/codecs.c',
    'Python/compile.c',
    'Python/dtoa.c',
    'Python/dynamic_annotations.c',
    'Python/dynload_shlib.c',
    'Python/errors.c',
    'Python/fileutils.c',
    'Python/formatter_unicode.c',
    'Python/frozen.c',
    'Python/frozenmain.c',
    'Python/future.c',
    'Python/getargs.c',
    'Python/getcompiler.c',
    'Python/getcopyright.c',
    'Python/getopt.c',
    'Python/getplatform.c',
    'Python/getversion.c',
    'Python/graminit.c',
    'Python/import.c',
    'Python/importdl.c',
    'Python/marshal.c',
    'Python/modsupport.c',
    'Python/mysnprintf.c',
    'Python/mystrtoul.c',
    'Python/pathconfig.c',
    'Python/peephole.c',
    'Python/pyarena.c',
    'Python/pyctype.c',
    'Python/pyfpe.c',
    'Python/pyhash.c',
    'Python/pylifecycle.c',
    'Python/pymath.c',
    'Python/pystate.c',
    'Python/pystrcmp.c',
    'Python/pystrhex.c',
    'Python/pystrtod.c',
    'Python/pythonrun.c',
    'Python/pytime.c',
    'Python/structmember.c',
    'Python/symtable.c',
    'Python/sysmodule.c',
    'Python/thread.c',
    'Python/traceback.c',
]

GENERATED_SRCS = [
    'Modules/config.c',
    'pyconfig.h',
]

cc_library(
    name = 'cpython',
    srcs = cpython_srcs + glob([
        'Modules/**/*.h',
        'Objects/*.h',
        'Objects/*/*.h',
        'Parser/*.h',
        'Python/*.h',
        'Python/clinic/*.h',
    ]) + GENERATED_SRCS,
    hdrs = glob([
        'Include/Python.h',
        '*.h',
    ]),
    textual_hdrs = glob([
        'Objects/typeslots.inc',
        'Include/**/*.h',
        'Modules/_io/_iomodule.c',
    ], exclude = [
        'Include/Python.h'
    ]),
    includes = [
        'Include',
    ] + ([ '.' ] if package_name() else []),
    copts = cpython_copts + [
        '-I$(GENDIR)',
    ],
)

genrule(
    name = 'generated_srcs',
    srcs = glob([
        '**/*.in',
        'Include/object.h',
        'Modules/Setup.dist',
        'Modules/makesetup',
        'aclocal.m4',
        'config.guess',
        'config.sub',
        'configure.ac',
        'install-sh',
        'pyconfig.h.in',
    ]),
    tools = [
        'configure',
    ],
    outs = GENERATED_SRCS,
    cmd = ' && '.join([
        'cd ./%s' % package_name(),
        './configure &> /dev/null',
        'cd -',
    ] + [
        'mv ./%s/%s $(location %s)' % (package_name(), f, f) \
                for f in GENERATED_SRCS
    ]),
)
