This is a bug repro for `rules_go#3906`. To reproduce the bug, run `bazel build //:lib`. You 
should get output like:

```
ERROR: /private/var/tmp/_bazel_ekohlwey/ba2d0a12d7f9a968440f6fa17ec9ba60/external/gazelle~~go_deps~org_golang_google_protobuf/cmd/protoc-gen-go/BUILD.bazel:15:10: in go_binary rule @@gazelle~~go_deps~org_golang_google_protobuf//cmd/protoc-gen-go:protoc-gen-go: cycle in dependency graph:
    //:lib (e086b79b00bd50f8db6723fe69c656dab90c2872096c0470ec594fb9ee81941b)
    //:lib (5b0980b6343c3346cce9ffb7dc840cb65d51d2bf0c3b09071b8321018db8d21a)
    @@gazelle~~go_deps~com_google_cloud_go_storage//:storage (5b0980b6343c3346cce9ffb7dc840cb65d51d2bf0c3b09071b8321018db8d21a)
    @@gazelle~~go_deps~org_golang_google_grpc//status:status (5b0980b6343c3346cce9ffb7dc840cb65d51d2bf0c3b09071b8321018db8d21a)
    @@gazelle~~go_deps~org_golang_google_grpc//internal/status:status (5b0980b6343c3346cce9ffb7dc840cb65d51d2bf0c3b09071b8321018db8d21a)
    @@gazelle~~go_deps~org_golang_google_grpc//codes:codes (5b0980b6343c3346cce9ffb7dc840cb65d51d2bf0c3b09071b8321018db8d21a)
    @@gazelle~~go_deps~org_golang_google_grpc//internal:internal (5b0980b6343c3346cce9ffb7dc840cb65d51d2bf0c3b09071b8321018db8d21a)
    @@gazelle~~go_deps~org_golang_google_grpc//resolver:resolver (5b0980b6343c3346cce9ffb7dc840cb65d51d2bf0c3b09071b8321018db8d21a)
    @@gazelle~~go_deps~org_golang_google_grpc//credentials:credentials (5b0980b6343c3346cce9ffb7dc840cb65d51d2bf0c3b09071b8321018db8d21a)
    @@gazelle~~go_deps~com_github_golang_protobuf//proto:go_default_library (5b0980b6343c3346cce9ffb7dc840cb65d51d2bf0c3b09071b8321018db8d21a)
    @@gazelle~~go_deps~com_github_golang_protobuf//proto:proto (5b0980b6343c3346cce9ffb7dc840cb65d51d2bf0c3b09071b8321018db8d21a)
    @@gazelle~~go_deps~org_golang_google_protobuf//reflect/protodesc:protodesc (5b0980b6343c3346cce9ffb7dc840cb65d51d2bf0c3b09071b8321018db8d21a)
    @@gazelle~~go_deps~org_golang_google_protobuf//types/gofeaturespb:gofeaturespb (5b0980b6343c3346cce9ffb7dc840cb65d51d2bf0c3b09071b8321018db8d21a)
    @@gazelle~~go_deps~org_golang_google_protobuf//types/gofeaturespb:gofeaturespb_go_proto (5b0980b6343c3346cce9ffb7dc840cb65d51d2bf0c3b09071b8321018db8d21a)
    @@rules_go~//proto:go_proto (5b0980b6343c3346cce9ffb7dc840cb65d51d2bf0c3b09071b8321018db8d21a)
    @@rules_go~//proto:go_proto_reset_plugin_ (f0f11f9aa5edb12bea15e484f1f24988480676527949682b707eb275031dc7a4)
.-> @@gazelle~~go_deps~org_golang_google_protobuf//cmd/protoc-gen-go:protoc-gen-go (c4338806291c4bdb6b5af173c84c3e00bdb87e23b9098acb2922758467a8b46d)
|   @@gazelle~~go_deps~org_golang_google_protobuf//cmd/protoc-gen-go:protoc-gen-go_lib (c4338806291c4bdb6b5af173c84c3e00bdb87e23b9098acb2922758467a8b46d)
|   @@gazelle~~go_deps~org_golang_google_protobuf//compiler/protogen:protogen (c4338806291c4bdb6b5af173c84c3e00bdb87e23b9098acb2922758467a8b46d)
|   @@gazelle~~go_deps~org_golang_google_protobuf//reflect/protodesc:protodesc (c4338806291c4bdb6b5af173c84c3e00bdb87e23b9098acb2922758467a8b46d)
|   @@gazelle~~go_deps~org_golang_google_protobuf//types/gofeaturespb:gofeaturespb (c4338806291c4bdb6b5af173c84c3e00bdb87e23b9098acb2922758467a8b46d)
|   @@gazelle~~go_deps~org_golang_google_protobuf//types/gofeaturespb:gofeaturespb_go_proto (c4338806291c4bdb6b5af173c84c3e00bdb87e23b9098acb2922758467a8b46d)
|   @@rules_go~//proto:go_proto (c4338806291c4bdb6b5af173c84c3e00bdb87e23b9098acb2922758467a8b46d)
|   @@rules_go~//proto:go_proto_reset_plugin_ (c4338806291c4bdb6b5af173c84c3e00bdb87e23b9098acb2922758467a8b46d)
`-- @@gazelle~~go_deps~org_golang_google_protobuf//cmd/protoc-gen-go:protoc-gen-go (c4338806291c4bdb6b5af173c84c3e00bdb87e23b9098acb2922758467a8b46d)
ERROR: Analysis of target '//:lib' failed; build aborted
INFO: Elapsed time: 16.666s, Critical Path: 0.00s
INFO: 1 process: 1 internal.
ERROR: Build did NOT complete successfully
```
