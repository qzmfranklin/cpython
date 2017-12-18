licenses(['notice'])

package(default_visibility=['//visibility:public'])

load(':bazel/python_data.bzl', 'CPYTHON_SRCS', 'CPYTHON_COPTS')

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
    copts = CPYTHON_COPTS,
    linkopts = [
        '-lm',
        '-pthread',
        '-ldl',
        '-lutil',
    ],
)

GENERATED_SRCS = [
    'Modules/config.c',
    'pyconfig.h',
]

cc_library(
    name = 'cpython',
    srcs = CPYTHON_SRCS + glob([
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
    copts = CPYTHON_COPTS + [
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
        'cd - &> /dev/null',
    ] + [
        'mv ./%s/%s $(location %s)' % (package_name(), f, f) \
                for f in GENERATED_SRCS
    ]),
)
