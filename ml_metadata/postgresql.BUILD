load("@rules_foreign_cc//foreign_cc:defs.bzl", "configure_make")

filegroup(
    name = "all_srcs",
    srcs = glob(
        include = ["**"],
        exclude = ["*.bazel"],
    ),
)

alias(
    name = "postgresql",
    actual = "postgresql_default",
    visibility = ["//visibility:public"],
)

configure_make(
    name = "postgresql_default",
    lib_source = ":all_srcs",
    lib_name = "postgresql",
    env = select({
        # Workaround for libtool no output files specified on MacOS.
        # https://github.com/bazelbuild/rules_foreign_cc/issues/338
        # https://github.com/bazelbuild/rules_foreign_cc/issues/254
        "@platforms//os:macos": {
            # Necessary to create a fully static linked library.
            "CXXFLAGS": "-fPIC",
            "CFLAGS": "-fPIC",
            # OSX crosstools specific flags
            "LDFLAGS": "-undefined error",
            "AR": "",
        },
        "//conditions:default": {
            # Necessary to create a fully static linked library.
            "CXXFLAGS": "-fPIC",
            "CFLAGS": "-fPIC",
        },
    }),
    configure_options = [
        "--with-openssl",
        # "--with-libraries=$EXT_BUILD_DEPS/openssl/lib",
        # "--with-includes=$EXT_BUILD_DEPS/openssl/include",
          # See: https://github.com/bazelbuild/rules_foreign_cc/pull/362
        "CFLAGS='-Dredacted=\\\"redacted\\\"'",
    ],
    out_shared_libs = select({
        # Workaround for libtool no output files specified on MacOS.
        # https://github.com/bazelbuild/rules_foreign_cc/issues/338
        # https://github.com/bazelbuild/rules_foreign_cc/issues/254
        "@platforms//os:macos": [
            "libpq.dylib",
            "libpgtypes.dylib",
        ],
        "//conditions:default": [
            "libpq.so",
            "libpgtypes.so",
            "libpq.so.5",
            "libpgtypes.so.3",
        ],
    }),
    out_binaries = [
        "clusterdb",
        "createdb",
        "createuser",
        "dropdb",
        "dropuser",
        "initdb",
        "pg_archivecleanup",
        "pg_basebackup",
        "pg_checksums",
        "pg_config",
        "pg_controldata",
        "pg_ctl",
        "pg_dump",
        "pg_dumpall",
        "pg_isready",
        "pg_receivewal",
        "pg_recvlogical",
        "pg_resetwal",
        "pg_restore",
        "pg_rewind",
        "pg_test_fsync",
        "pg_test_timing",
        "pg_upgrade",
        "pg_waldump",
        "pgbench",
        "postgres",
        "psql",
        "reindexdb",
        "vacuumdb",
    ],
)
