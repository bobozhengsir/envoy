load(
    "//bazel:envoy_build_system.bzl",
    "envoy_benchmark_test",
    "envoy_cc_benchmark_binary",
    "envoy_cc_fuzz_test",
    "envoy_cc_test",
    "envoy_cc_test_library",
    "envoy_package",
    "envoy_select_google_grpc",
)

licenses(["notice"])  # Apache 2

envoy_package()

envoy_cc_test(
    name = "async_client_impl_test",
    srcs = ["async_client_impl_test.cc"],
    rbe_pool = "6gig",
    deps = [
        "//source/common/event:dispatcher_lib",
        "//source/common/formatter:formatter_extension_lib",
        "//source/common/grpc:async_client_lib",
        "//test/mocks/http:http_mocks",
        "//test/mocks/tracing:tracing_mocks",
        "//test/mocks/upstream:cluster_manager_mocks",
        "//test/proto:helloworld_proto_cc_proto",
        "//test/test_common:test_time_lib",
        "@envoy_api//envoy/config/core/v3:pkg_cc_proto",
    ],
)

envoy_cc_test(
    name = "async_client_manager_impl_test",
    srcs = ["async_client_manager_impl_test.cc"],
    rbe_pool = "6gig",
    deps = [
        "//source/common/api:api_lib",
        "//source/common/grpc:async_client_manager_lib",
        "//test/mocks/server:server_factory_context_mocks",
        "//test/mocks/stats:stats_mocks",
        "//test/mocks/thread_local:thread_local_mocks",
        "//test/mocks/upstream:cluster_manager_mocks",
        "//test/mocks/upstream:cluster_priority_set_mocks",
        "//test/test_common:test_runtime_lib",
        "//test/test_common:utility_lib",
        "@envoy_api//envoy/config/bootstrap/v3:pkg_cc_proto",
        "@envoy_api//envoy/config/core/v3:pkg_cc_proto",
    ],
)

envoy_cc_fuzz_test(
    name = "codec_fuzz_test",
    srcs = ["codec_fuzz_test.cc"],
    corpus = "codec_corpus",
    rbe_pool = "6gig",
    deps = [
        "//source/common/buffer:buffer_lib",
        "//source/common/grpc:codec_lib",
        "//test/fuzz:utility_lib",
        "//test/proto:helloworld_proto_cc_proto",
    ],
)

envoy_cc_test(
    name = "codec_test",
    srcs = ["codec_test.cc"],
    rbe_pool = "6gig",
    deps = [
        "//source/common/buffer:buffer_lib",
        "//source/common/grpc:codec_lib",
        "//test/common/buffer:utility_lib",
        "//test/proto:helloworld_proto_cc_proto",
    ],
)

envoy_cc_test(
    name = "common_test",
    srcs = ["common_test.cc"],
    rbe_pool = "6gig",
    deps = [
        "//source/common/grpc:common_lib",
        "//source/common/http:headers_lib",
        "//test/mocks/stream_info:stream_info_mocks",
        "//test/proto:helloworld_proto_cc_proto",
        "//test/test_common:utility_lib",
    ],
)

envoy_cc_test(
    name = "context_impl_test",
    srcs = ["context_impl_test.cc"],
    rbe_pool = "6gig",
    deps = [
        "//source/common/grpc:common_lib",
        "//source/common/grpc:context_lib",
        "//source/common/http:headers_lib",
        "//test/mocks/upstream:cluster_info_mocks",
        "//test/test_common:global_lib",
    ],
)

envoy_cc_test(
    name = "google_grpc_utils_test",
    srcs = envoy_select_google_grpc(["google_grpc_utils_test.cc"]),
    rbe_pool = "6gig",
    deps = [
        "//source/common/grpc:common_lib",
        "//source/common/http:headers_lib",
        "//test/proto:helloworld_proto_cc_proto",
        "//test/test_common:utility_lib",
    ] + envoy_select_google_grpc(["//source/common/grpc:google_grpc_utils_lib"]),
)

envoy_cc_test(
    name = "google_async_client_impl_test",
    srcs = envoy_select_google_grpc(["google_async_client_impl_test.cc"]),
    rbe_pool = "6gig",
    deps = [
        "//source/common/api:api_lib",
        "//source/common/event:dispatcher_lib",
        "//source/common/formatter:formatter_extension_lib",
        "//source/common/stats:isolated_store_lib",
        "//source/common/stats:stats_lib",
        "//source/common/tracing:http_tracer_lib",
        "//test/mocks/grpc:grpc_mocks",
        "//test/mocks/server:server_factory_context_mocks",
        "//test/mocks/tracing:tracing_mocks",
        "//test/proto:helloworld_proto_cc_proto",
        "//test/test_common:test_time_lib",
        "//test/test_common:utility_lib",
    ] + envoy_select_google_grpc(["//source/common/grpc:google_async_client_lib"]),
)

envoy_cc_test(
    name = "google_grpc_creds_test",
    srcs = envoy_select_google_grpc(["google_grpc_creds_test.cc"]),
    data = [":service_key.json"],
    rbe_pool = "6gig",
    deps = [
        ":utility_lib",
        "//test/mocks/stats:stats_mocks",
        "//test/test_common:utility_lib",
    ] + envoy_select_google_grpc(["//source/common/grpc:google_grpc_creds_lib"]),
)

envoy_cc_test_library(
    name = "grpc_client_integration_lib",
    hdrs = ["grpc_client_integration.h"],
    deps = [
        "//source/common/common:assert_lib",
        "//test/mocks/secret:secret_mocks",
        "//test/test_common:environment_lib",
        "//test/test_common:utility_lib",
        "@envoy_api//envoy/config/core/v3:pkg_cc_proto",
    ],
)

envoy_cc_test_library(
    name = "grpc_client_integration_test_harness_lib",
    hdrs = ["grpc_client_integration_test_harness.h"],
    deps = [
        ":grpc_client_integration_lib",
        ":utility_lib",
        "//source/common/api:api_lib",
        "//source/common/event:dispatcher_lib",
        "//source/common/grpc:context_lib",
        "//source/common/http:context_lib",
        "//source/common/http/http2:conn_pool_lib",
        "//source/common/router:context_lib",
        "//test/integration:integration_lib",
        "//test/mocks/local_info:local_info_mocks",
        "//test/mocks/server:factory_context_mocks",
        "//test/mocks/upstream:cluster_info_mocks",
        "//test/mocks/upstream:cluster_manager_mocks",
        "//test/mocks/upstream:host_mocks",
        "//test/mocks/upstream:thread_local_cluster_mocks",
        "//test/proto:helloworld_proto_cc_proto",
        "//test/test_common:global_lib",
        "//test/test_common:test_time_lib",
        "//test/test_common:utility_lib",
        "@envoy_api//envoy/config/core/v3:pkg_cc_proto",
        "@envoy_api//envoy/extensions/transport_sockets/tls/v3:pkg_cc_proto",
    ],
)

envoy_cc_test(
    name = "grpc_client_integration_test",
    size = "large",
    srcs = ["grpc_client_integration_test.cc"],
    rbe_pool = "6gig",
    deps = [
        ":grpc_client_integration_test_harness_lib",
        "//source/common/grpc:async_client_lib",
        "//source/extensions/grpc_credentials/example:config",
        "//test/test_common:test_runtime_lib",
    ] + envoy_select_google_grpc(["//source/common/grpc:google_async_client_lib"]),
)

envoy_cc_test_library(
    name = "utility_lib",
    hdrs = ["utility.h"],
    data = ["//test/config/integration/certs"],
    deps = [
        "//test/test_common:environment_lib",
        "@envoy_api//envoy/config/core/v3:pkg_cc_proto",
    ],
)

envoy_cc_test(
    name = "buffered_async_client_test",
    srcs = ["buffered_async_client_test.cc"],
    rbe_pool = "6gig",
    deps = [
        "//source/common/grpc:async_client_lib",
        "//source/common/grpc:buffered_async_client_lib",
        "//test/mocks/http:http_mocks",
        "//test/mocks/tracing:tracing_mocks",
        "//test/mocks/upstream:cluster_manager_mocks",
        "//test/proto:helloworld_proto_cc_proto",
        "//test/test_common:test_time_lib",
        "@envoy_api//envoy/config/core/v3:pkg_cc_proto",
    ],
)

envoy_cc_test(
    name = "buffered_message_ttl_manager_test",
    srcs = ["buffered_message_ttl_manager_test.cc"],
    rbe_pool = "6gig",
    deps = [
        "//source/common/event:dispatcher_lib",
        "//source/common/grpc:buffered_message_ttl_manager_lib",
        "//test/test_common:utility_lib",
    ],
)

envoy_cc_benchmark_binary(
    name = "async_client_manager_benchmark",
    srcs = ["async_client_manager_benchmark.cc"],
    rbe_pool = "6gig",
    deps = [
        "//source/common/api:api_lib",
        "//source/common/grpc:async_client_manager_lib",
        "//test/mocks/server:server_factory_context_mocks",
        "//test/mocks/stats:stats_mocks",
        "//test/mocks/thread_local:thread_local_mocks",
        "//test/mocks/upstream:cluster_manager_mocks",
        "//test/mocks/upstream:cluster_priority_set_mocks",
        "//test/test_common:test_runtime_lib",
        "//test/test_common:utility_lib",
        "@com_github_google_benchmark//:benchmark",
        "@envoy_api//envoy/config/bootstrap/v3:pkg_cc_proto",
        "@envoy_api//envoy/config/core/v3:pkg_cc_proto",
    ],
)

envoy_benchmark_test(
    name = "async_client_manager_benchmark_test",
    timeout = "long",
    benchmark_binary = "async_client_manager_benchmark",
)
