package(licenses = ["notice"])

cc_library(
    name = "allreduce_interface",
    srcs = [
        "allreduce_translator.cc",
    ],
    hdrs = [
        "allreduce_translator.h",
    ],
    deps = [
        "//paragraph/translation:translator",
        "@com_google_absl//absl/memory:memory",
        "@libfactory//:factory",
        "@nlohmann_json//:nlohmann_json",
    ],
    visibility = [
        "//paragraph/translation:__subpackages__",
    ],
    alwayslink = 1,
)

cc_library(
    name = "allreduce",
    srcs = [
        "unidir_ring_allreduce_translator.cc",
    ],
    hdrs = [
        "unidir_ring_allreduce_translator.h",
    ],
    deps = [
        ":allreduce_interface",
        "//paragraph/translation:factory",
        "//paragraph/translation/allgather:allgather",
        "//paragraph/translation/allgather:allgather_interface",
        "//paragraph/translation/barrier:barrier",
        "//paragraph/translation/barrier:barrier_interface",
        "//paragraph/translation/reducescatter:reducescatter",
        "//paragraph/translation/reducescatter:reducescatter_interface",
        "@libfactory//:factory",
        "@nlohmann_json//:nlohmann_json",
    ],
    visibility = [
        "//paragraph/translation:__subpackages__",
    ],
    alwayslink = 1,
)

cc_test(
    name = "allreduce_test",
    size = "small",
    srcs = [
        "unidir_ring_allreduce_translator_test.cc",
    ],
    deps = [
        ":allreduce",
        "//paragraph/shim:test_macros",
        "//paragraph/translation:factory",
        "@com_google_protobuf//:protobuf",
        "@googletest//:gtest_main",
    ],
    visibility = [
        "//paragraph/translation:__subpackages__",
    ],
)

genrule(
    name = "lint_cc",
    srcs = glob([
        "*.cc",
        "*.h",
        "*.tcc",
    ]),
    outs = ["linted"],
    cmd = """
        python $(location @cpplint//:cpplint) \
          --root=$$(pwd) \
          --headers=h,tcc \
          --extensions=cc,h,tcc \
          --quiet $(SRCS) > $@
        echo // $$(date) > $@
        """,
    tools = [
        "@cpplint",
    ],
)
