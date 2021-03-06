package(default_visibility = [
    "//visibility:public",
])

licenses(["notice"])  # Apache 2.0

cc_binary(
    name = "option_writer_generator",
    srcs = ["option_writer_generator.cc"],
    deps = [
        "//tensorflow/contrib/lite/schema:schema_fbs_with_reflection",
        "@flatbuffers",
    ],
)

cc_library(
    name = "writer_lib",
    srcs = [
        "enum_mapping.h",
        "writer_lib.cc",
    ],
    hdrs = [
        "writer_lib.h",
    ],
    data = [
        ":option_writer_gen",
    ],
    textual_hdrs = ["option_writer_generated.h"],
    deps = [
        "//tensorflow/contrib/lite:builtin_op_data",
        "//tensorflow/contrib/lite:framework",
        "//tensorflow/contrib/lite:schema_fbs_version",
        "//tensorflow/contrib/lite/kernels:builtin_ops",
        "//tensorflow/contrib/lite/schema:schema_fbs_with_reflection",
    ],
)

cc_binary(
    name = "writer",
    srcs = ["writer.cc"],
    deps = [
        ":writer_lib",
        "//tensorflow/contrib/lite:framework",
        "//tensorflow/contrib/lite/kernels:builtin_ops",
    ],
)

cc_test(
    name = "writer_lib_test",
    size = "small",
    srcs = ["writer_lib_test.cc"],
    deps = [
        ":writer_lib",
        "//tensorflow/contrib/lite:framework",
        "//tensorflow/contrib/lite/kernels:builtin_ops",
        "//tensorflow/contrib/lite/testing:util",
        "@com_google_googletest//:gtest",
    ],
)

genrule(
    name = "option_writer_gen",
    outs = ["option_writer_generated.h"],
    cmd = "$(location :option_writer_generator) $(@)",
    tools = [":option_writer_generator"],
)
