load("//third_party/mlir:tblgen.bzl", "gentbl")

package(
    default_visibility = [":friends"],
    licenses = ["notice"],  # Apache 2.0
)

package_group(
    name = "friends",
    includes = ["//third_party/mlir:subpackages"],
    packages = ["//tensorflow/compiler/mlir/..."],
)

gentbl(
    name = "tf_framework_ops_inc_gen",
    tbl_outs = [
        ("-gen-op-decls", "tf_framework_ops.h.inc"),
        ("-gen-op-defs", "tf_framework_ops.cc.inc"),
        ("-gen-struct-attr-decls", "tf_framework_structs.h.inc"),
        ("-gen-struct-attr-defs", "tf_framework_structs.cc.inc"),
        ("-gen-dialect-decls", "tf_framework_dialect.h.inc"),
    ],
    tblgen = "@llvm-project//mlir:mlir-tblgen",
    td_file = "tf_framework_ops.td",
    td_srcs = [
        "tf_framework_ops.td",
        "@llvm-project//mlir:OpBaseTdFiles",
        "@llvm-project//mlir:include/mlir/Interfaces/SideEffectInterfaces.td",
    ],
)

cc_library(
    name = "tf_framework_ops",
    srcs = [
        "tf_framework_ops.cc",
        "tf_framework_ops.cc.inc",
        "tf_framework_ops.h.inc",
    ],
    hdrs = ["tf_framework_ops.h"],
    deps = [
        ":tf_framework_ops_inc_gen",
        "@llvm-project//mlir:IR",
        "@llvm-project//mlir:SideEffects",
    ],
)

cc_library(
    name = "tf_framework_dialect_registration",
    srcs = ["dialect_registration.cc"],
    deps = [
        ":tf_framework_ops",
        "@llvm-project//mlir:IR",
    ],
    alwayslink = 1,
)
