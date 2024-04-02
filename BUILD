load("@rules_go//go:def.bzl", "go_library")

go_library(
    name = "lib",
    srcs = ["lib.go"],
    importpath = "gitlab.com/ed-irl/rules-go-cycle-repro/",
    visibility = ["//visibility:public"],
    deps = [
        "@com_github_hashicorp_terraform_plugin_sdk_v2//diag",
        "@com_github_hashicorp_terraform_plugin_sdk_v2//helper/schema",
        "@com_google_cloud_go_storage//:storage",
        "@org_golang_google_api//iterator",
    ],
)