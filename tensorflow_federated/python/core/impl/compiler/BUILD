load("//tensorflow_federated/tools:build_defs.bzl", "py_cpu_gpu_test")
load("@rules_python//python:defs.bzl", "py_library", "py_test")

package(default_visibility = [
    ":compiler_packages",
    "//tensorflow_federated/experimental/python/core/impl/jax_context:jax_context_packages",
    "//tensorflow_federated/python/core/impl:impl_visibility",
    "//tensorflow_federated/python/core/impl/computation:computation_packages",
    "//tensorflow_federated/python/core/impl/execution_contexts:execution_contexts_packages",
    "//tensorflow_federated/python/core/impl/executor_stacks:executor_stacks_packages",
    "//tensorflow_federated/python/core/impl/executors:executors_packages",
    "//tensorflow_federated/python/core/impl/federated_context:federated_context_packages",
    "//tensorflow_federated/python/core/impl/wrappers:wrappers_packages",
])

package_group(
    name = "compiler_packages",
    packages = ["//tensorflow_federated/python/core/impl/compiler/..."],
)

licenses(["notice"])

py_library(
    name = "compiler",
    srcs = ["__init__.py"],
    srcs_version = "PY3",
    visibility = ["//tensorflow_federated/tools/python_package:python_package_tool"],
)

py_library(
    name = "building_block_analysis",
    srcs = ["building_block_analysis.py"],
    srcs_version = "PY3",
    deps = [
        ":building_blocks",
        "//tensorflow_federated/python/common_libs:py_typecheck",
        "//tensorflow_federated/python/common_libs:serialization_utils",
    ],
)

py_test(
    name = "building_block_analysis_test",
    size = "small",
    srcs = ["building_block_analysis_test.py"],
    python_version = "PY3",
    srcs_version = "PY3",
    deps = [
        ":building_block_analysis",
        ":building_blocks",
        "//tensorflow_federated/proto/v0:computation_py_pb2",
        "//tensorflow_federated/python/common_libs:serialization_utils",
        "//tensorflow_federated/python/core/api:computations",
        "//tensorflow_federated/python/core/impl/types:computation_types",
        "//tensorflow_federated/python/core/impl/types:type_serialization",
        "//tensorflow_federated/python/core/impl/utils:tensorflow_utils",
        "@absl_py//absl/testing:absltest",
        "@org_tensorflow//tensorflow:tensorflow_py",
    ],
)

py_library(
    name = "building_block_factory",
    srcs = ["building_block_factory.py"],
    srcs_version = "PY3",
    deps = [
        ":building_blocks",
        ":intrinsic_defs",
        ":tensorflow_computation_factory",
        ":transformation_utils",
        "//tensorflow_federated/proto/v0:computation_py_pb2",
        "//tensorflow_federated/python/common_libs:py_typecheck",
        "//tensorflow_federated/python/common_libs:serialization_utils",
        "//tensorflow_federated/python/common_libs:structure",
        "//tensorflow_federated/python/core/impl/types:computation_types",
        "//tensorflow_federated/python/core/impl/types:placements",
        "//tensorflow_federated/python/core/impl/types:type_analysis",
        "//tensorflow_federated/python/core/impl/types:type_conversions",
        "//tensorflow_federated/python/core/impl/types:type_serialization",
        "//tensorflow_federated/python/core/impl/types:type_transformations",
        "//tensorflow_federated/python/core/impl/utils:tensorflow_utils",
        "@org_tensorflow//tensorflow:tensorflow_py",
    ],
)

py_test(
    name = "building_block_factory_test",
    size = "small",
    srcs = ["building_block_factory_test.py"],
    args = [
        "--golden",
        "$(location building_block_factory_test_goldens/constructs_correct_computation_clients.expected)",
        "--golden",
        "$(location building_block_factory_test_goldens/constructs_correct_computation_server.expected)",
        "--golden",
        "$(location building_block_factory_test_goldens/replaces_single_element.expected)",
        "--golden",
        "$(location building_block_factory_test_goldens/skips_unnamed_element.expected)",
        "--golden",
        "$(location building_block_factory_test_goldens/tuple_federated_map_with_two_values_unnamed.expected)",
        "--golden",
        "$(location building_block_factory_test_goldens/tuple_federated_map_with_two_values_named.expected)",
        "--golden",
        "$(location building_block_factory_test_goldens/tuple_federated_map_with_two_values_different_typed.expected)",
        "--golden",
        "$(location building_block_factory_test_goldens/tuple_federated_apply_with_two_values_unnamed.expected)",
        "--golden",
        "$(location building_block_factory_test_goldens/tuple_federated_apply_with_two_values_named.expected)",
        "--golden",
        "$(location building_block_factory_test_goldens/tuple_federated_apply_with_two_values_different_typed.expected)",
        "--golden",
        "$(location building_block_factory_test_goldens/zips_tuple_unnamed.expected)",
        "--golden",
        "$(location building_block_factory_test_goldens/zips_tuple_named.expected)",
        "--golden",
        "$(location building_block_factory_test_goldens/zips_reference.expected)",
    ],
    data = [
        "building_block_factory_test_goldens/constructs_correct_computation_clients.expected",
        "building_block_factory_test_goldens/constructs_correct_computation_server.expected",
        "building_block_factory_test_goldens/replaces_single_element.expected",
        "building_block_factory_test_goldens/skips_unnamed_element.expected",
        "building_block_factory_test_goldens/tuple_federated_apply_with_two_values_different_typed.expected",
        "building_block_factory_test_goldens/tuple_federated_apply_with_two_values_named.expected",
        "building_block_factory_test_goldens/tuple_federated_apply_with_two_values_unnamed.expected",
        "building_block_factory_test_goldens/tuple_federated_map_with_two_values_different_typed.expected",
        "building_block_factory_test_goldens/tuple_federated_map_with_two_values_named.expected",
        "building_block_factory_test_goldens/tuple_federated_map_with_two_values_unnamed.expected",
        "building_block_factory_test_goldens/zips_reference.expected",
        "building_block_factory_test_goldens/zips_tuple_named.expected",
        "building_block_factory_test_goldens/zips_tuple_unnamed.expected",
    ],
    python_version = "PY3",
    srcs_version = "PY3",
    deps = [
        ":building_block_factory",
        ":building_blocks",
        ":intrinsic_defs",
        ":test_utils",
        "//tensorflow_federated/python/common_libs:golden",
        "//tensorflow_federated/python/common_libs:structure",
        "//tensorflow_federated/python/core/api:test_case",
        "//tensorflow_federated/python/core/impl/types:computation_types",
        "//tensorflow_federated/python/core/impl/types:placements",
        "//tensorflow_federated/python/core/impl/types:type_analysis",
        "@absl_py//absl/testing:parameterized",
        "@org_tensorflow//tensorflow:tensorflow_py",
    ],
)

py_library(
    name = "building_blocks",
    srcs = ["building_blocks.py"],
    srcs_version = "PY3",
    deps = [
        ":intrinsic_defs",
        "//tensorflow_federated/proto/v0:computation_py_pb2",
        "//tensorflow_federated/python/common_libs:py_typecheck",
        "//tensorflow_federated/python/common_libs:structure",
        "//tensorflow_federated/python/core/impl/types:computation_types",
        "//tensorflow_federated/python/core/impl/types:placements",
        "//tensorflow_federated/python/core/impl/types:type_analysis",
        "//tensorflow_federated/python/core/impl/types:type_serialization",
        "//tensorflow_federated/python/core/impl/types:typed_object",
    ],
)

py_test(
    name = "building_blocks_test",
    size = "small",
    srcs = ["building_blocks_test.py"],
    python_version = "PY3",
    srcs_version = "PY3",
    deps = [
        ":building_block_factory",
        ":building_blocks",
        ":intrinsic_defs",
        ":test_utils",
        "//tensorflow_federated/proto/v0:computation_py_pb2",
        "//tensorflow_federated/python/common_libs:structure",
        "//tensorflow_federated/python/core/impl/types:computation_types",
        "//tensorflow_federated/python/core/impl/types:placements",
        "//tensorflow_federated/python/core/impl/types:type_serialization",
        "@absl_py//absl/testing:absltest",
        "@org_tensorflow//tensorflow:tensorflow_py",
    ],
)

py_library(
    name = "compiled_computation_transforms",
    srcs = ["compiled_computation_transforms.py"],
    srcs_version = "PY3",
    deps = [
        ":building_blocks",
        ":tensorflow_computation_transformations",
        ":transformation_utils",
        "//tensorflow_federated/proto/v0:computation_py_pb2",
        "//tensorflow_federated/python/common_libs:py_typecheck",
        "//tensorflow_federated/python/common_libs:serialization_utils",
        "//tensorflow_federated/python/core/impl/utils:tensorflow_utils",
        "//tensorflow_federated/python/tensorflow_libs:graph_optimizations",
        "//tensorflow_federated/python/tensorflow_libs:graph_spec",
        "@org_tensorflow//tensorflow:tensorflow_py",
    ],
)

py_test(
    name = "compiled_computation_transforms_test",
    size = "small",
    srcs = ["compiled_computation_transforms_test.py"],
    python_version = "PY3",
    srcs_version = "PY3",
    deps = [
        ":building_block_factory",
        ":building_blocks",
        ":compiled_computation_transforms",
        ":tensorflow_computation_factory",
        ":test_utils",
        "//tensorflow_federated/python/core/api:test_case",
        "//tensorflow_federated/python/core/impl/types:computation_types",
        "@org_tensorflow//tensorflow:tensorflow_py",
    ],
)

py_library(
    name = "computation_factory",
    srcs = ["computation_factory.py"],
    srcs_version = "PY3",
    deps = [
        "//tensorflow_federated/proto/v0:computation_py_pb2",
        "//tensorflow_federated/python/core/impl/types:computation_types",
        "//tensorflow_federated/python/core/impl/types:type_factory",
        "//tensorflow_federated/python/core/impl/types:type_serialization",
    ],
)

py_test(
    name = "computation_factory_test",
    srcs = ["computation_factory_test.py"],
    python_version = "PY3",
    srcs_version = "PY3",
    deps = [
        ":computation_factory",
        "//tensorflow_federated/proto/v0:computation_py_pb2",
        "//tensorflow_federated/python/core/impl/types:computation_types",
        "//tensorflow_federated/python/core/impl/types:type_factory",
        "//tensorflow_federated/python/core/impl/types:type_serialization",
        "@absl_py//absl/testing:absltest",
        "@org_tensorflow//tensorflow:tensorflow_py",
    ],
)

py_library(
    name = "intrinsic_defs",
    srcs = ["intrinsic_defs.py"],
    srcs_version = "PY3",
    deps = [
        "//tensorflow_federated/python/common_libs:py_typecheck",
        "//tensorflow_federated/python/core/impl/types:computation_types",
        "//tensorflow_federated/python/core/impl/types:type_factory",
        "@org_tensorflow//tensorflow:tensorflow_py",
    ],
)

py_library(
    name = "intrinsic_reductions",
    srcs = ["intrinsic_reductions.py"],
    srcs_version = "PY3",
    deps = [
        ":building_block_factory",
        ":building_blocks",
        ":intrinsic_defs",
        ":transformation_utils",
        "//tensorflow_federated/python/common_libs:py_typecheck",
        "//tensorflow_federated/python/common_libs:structure",
        "//tensorflow_federated/python/core/impl/types:computation_types",
        "//tensorflow_federated/python/core/impl/types:placements",
        "//tensorflow_federated/python/core/impl/types:type_analysis",
        "//tensorflow_federated/python/core/impl/types:type_conversions",
        "@org_tensorflow//tensorflow:tensorflow_py",
    ],
)

py_test(
    name = "intrinsic_reductions_test",
    size = "small",
    srcs = ["intrinsic_reductions_test.py"],
    python_version = "PY3",
    srcs_version = "PY3",
    deps = [
        ":building_blocks",
        ":intrinsic_defs",
        ":intrinsic_reductions",
        ":tree_analysis",
        "//tensorflow_federated/python/core/api:test_case",
        "//tensorflow_federated/python/core/impl/types:computation_types",
        "@absl_py//absl/testing:absltest",
        "@absl_py//absl/testing:parameterized",
        "@org_tensorflow//tensorflow:tensorflow_py",
    ],
)

py_test(
    name = "intrinsic_defs_test",
    size = "small",
    srcs = ["intrinsic_defs_test.py"],
    python_version = "PY3",
    srcs_version = "PY3",
    deps = [
        ":intrinsic_defs",
        "@absl_py//absl/testing:absltest",
        "@absl_py//absl/testing:parameterized",
    ],
)

py_library(
    name = "compiler_pipeline",
    srcs = ["compiler_pipeline.py"],
    srcs_version = "PY3",
    deps = [
        "//tensorflow_federated/python/common_libs:py_typecheck",
        "//tensorflow_federated/python/core/api:computation_base",
    ],
)

py_test(
    name = "compiler_pipeline_test",
    size = "small",
    srcs = ["compiler_pipeline_test.py"],
    python_version = "PY3",
    srcs_version = "PY3",
    deps = [
        ":compiler_pipeline",
        "//tensorflow_federated/python/core/api:computation_base",
        "//tensorflow_federated/python/core/api:test_case",
    ],
)

py_library(
    name = "local_computation_factory_base",
    srcs = ["local_computation_factory_base.py"],
    srcs_version = "PY3",
    deps = [
        "//tensorflow_federated/proto/v0:computation_py_pb2",
        "//tensorflow_federated/python/core/impl/types:computation_types",
    ],
)

py_library(
    name = "tensorflow_computation_factory",
    srcs = ["tensorflow_computation_factory.py"],
    srcs_version = "PY3",
    deps = [
        ":local_computation_factory_base",
        "//tensorflow_federated/proto/v0:computation_py_pb2",
        "//tensorflow_federated/python/common_libs:py_typecheck",
        "//tensorflow_federated/python/common_libs:serialization_utils",
        "//tensorflow_federated/python/common_libs:structure",
        "//tensorflow_federated/python/core/impl/types:computation_types",
        "//tensorflow_federated/python/core/impl/types:type_analysis",
        "//tensorflow_federated/python/core/impl/types:type_conversions",
        "//tensorflow_federated/python/core/impl/types:type_serialization",
        "//tensorflow_federated/python/core/impl/types:type_transformations",
        "//tensorflow_federated/python/core/impl/utils:tensorflow_utils",
        "@org_tensorflow//tensorflow:tensorflow_py",
    ],
)

py_cpu_gpu_test(
    name = "tensorflow_computation_factory_test",
    srcs = ["tensorflow_computation_factory_test.py"],
    python_version = "PY3",
    srcs_version = "PY3",
    deps = [
        ":tensorflow_computation_factory",
        ":test_utils",
        "//tensorflow_federated/proto/v0:computation_py_pb2",
        "//tensorflow_federated/python/common_libs:structure",
        "//tensorflow_federated/python/core/api:test_case",
        "//tensorflow_federated/python/core/impl/types:computation_types",
        "//tensorflow_federated/python/core/impl/types:type_factory",
        "//tensorflow_federated/python/core/impl/types:type_serialization",
        "@absl_py//absl/testing:parameterized",
        "@org_tensorflow//tensorflow:tensorflow_py",
    ],
)

py_library(
    name = "tensorflow_computation_transformations",
    srcs = ["tensorflow_computation_transformations.py"],
    srcs_version = "PY3",
    deps = [
        "//tensorflow_federated/proto/v0:computation_py_pb2",
        "//tensorflow_federated/python/common_libs:py_typecheck",
        "//tensorflow_federated/python/common_libs:serialization_utils",
        "@org_tensorflow//tensorflow:tensorflow_py",
    ],
)

py_test(
    name = "tensorflow_computation_transformations_test",
    size = "small",
    srcs = ["tensorflow_computation_transformations_test.py"],
    python_version = "PY3",
    srcs_version = "PY3",
    deps = [
        ":building_block_factory",
        ":tensorflow_computation_transformations",
        "//tensorflow_federated/proto/v0:computation_py_pb2",
        "//tensorflow_federated/python/common_libs:serialization_utils",
        "//tensorflow_federated/python/core/impl/types:computation_types",
        "//tensorflow_federated/python/core/impl/types:type_serialization",
        "//tensorflow_federated/python/core/impl/utils:tensorflow_utils",
        "@absl_py//absl/testing:absltest",
        "@org_tensorflow//tensorflow:tensorflow_py",
    ],
)

py_library(
    name = "test_utils",
    testonly = True,
    srcs = ["test_utils.py"],
    srcs_version = "PY3",
    deps = [
        ":building_block_factory",
        ":building_blocks",
        "//tensorflow_federated/python/common_libs:py_typecheck",
        "//tensorflow_federated/python/common_libs:structure",
        "//tensorflow_federated/python/core/impl/types:computation_types",
        "//tensorflow_federated/python/core/impl/types:placements",
        "//tensorflow_federated/python/core/impl/types:type_serialization",
        "//tensorflow_federated/python/core/impl/utils:tensorflow_utils",
        "@org_tensorflow//tensorflow:tensorflow_py",
    ],
)

py_library(
    name = "transformations",
    srcs = ["transformations.py"],
    srcs_version = "PY3",
    deps = [
        ":building_block_factory",
        ":building_blocks",
        ":compiled_computation_transforms",
        ":transformation_utils",
        ":tree_analysis",
        ":tree_transformations",
        "//tensorflow_federated/python/common_libs:py_typecheck",
        "//tensorflow_federated/python/common_libs:structure",
        "//tensorflow_federated/python/core/impl/computation:computation_impl",
        "//tensorflow_federated/python/core/impl/context_stack:context_stack_impl",
        "//tensorflow_federated/python/core/impl/types:computation_types",
        "//tensorflow_federated/python/core/impl/types:type_analysis",
        "//tensorflow_federated/python/core/impl/wrappers:computation_wrapper_instances",
    ],
)

py_test(
    name = "transformations_test",
    srcs = ["transformations_test.py"],
    python_version = "PY3",
    srcs_version = "PY3",
    deps = [
        ":building_block_analysis",
        ":building_block_factory",
        ":building_blocks",
        ":intrinsic_defs",
        ":test_utils",
        ":transformations",
        ":tree_analysis",
        "//tensorflow_federated/proto/v0:computation_py_pb2",
        "//tensorflow_federated/python/core/api:test_case",
        "//tensorflow_federated/python/core/impl/types:computation_types",
        "//tensorflow_federated/python/core/impl/types:placements",
        "//tensorflow_federated/python/core/impl/types:type_analysis",
        "//tensorflow_federated/python/core/impl/types:type_serialization",
        "@org_tensorflow//tensorflow:tensorflow_py",
    ],
)

py_library(
    name = "transformation_utils",
    srcs = ["transformation_utils.py"],
    srcs_version = "PY3",
    deps = [
        ":building_blocks",
        "//tensorflow_federated/python/common_libs:py_typecheck",
        "//tensorflow_federated/python/common_libs:structure",
    ],
)

py_test(
    name = "transformation_utils_test",
    size = "small",
    srcs = ["transformation_utils_test.py"],
    python_version = "PY3",
    srcs_version = "PY3",
    deps = [
        ":building_block_factory",
        ":building_blocks",
        ":test_utils",
        ":transformation_utils",
        "//tensorflow_federated/python/common_libs:py_typecheck",
        "//tensorflow_federated/python/core/impl/types:computation_types",
        "//tensorflow_federated/python/core/impl/types:placements",
        "@absl_py//absl/testing:absltest",
        "@absl_py//absl/testing:parameterized",
        "@org_tensorflow//tensorflow:tensorflow_py",
    ],
)

py_library(
    name = "tree_analysis",
    srcs = ["tree_analysis.py"],
    srcs_version = "PY3",
    deps = [
        ":building_block_analysis",
        ":building_blocks",
        ":intrinsic_defs",
        ":transformation_utils",
        "//tensorflow_federated/python/common_libs:py_typecheck",
        "//tensorflow_federated/python/common_libs:serialization_utils",
        "//tensorflow_federated/python/core/impl/types:placements",
        "//tensorflow_federated/python/core/impl/types:type_analysis",
        "@org_tensorflow//tensorflow:tensorflow_py",
    ],
)

py_test(
    name = "tree_analysis_test",
    srcs = ["tree_analysis_test.py"],
    python_version = "PY3",
    srcs_version = "PY3",
    deps = [
        ":building_block_analysis",
        ":building_block_factory",
        ":building_blocks",
        ":intrinsic_defs",
        ":test_utils",
        ":tree_analysis",
        "//tensorflow_federated/proto/v0:computation_py_pb2",
        "//tensorflow_federated/python/common_libs:serialization_utils",
        "//tensorflow_federated/python/core/impl/types:computation_types",
        "//tensorflow_federated/python/core/impl/types:placements",
        "//tensorflow_federated/python/core/impl/types:type_serialization",
        "//tensorflow_federated/python/core/impl/utils:tensorflow_utils",
        "@absl_py//absl/testing:absltest",
        "@absl_py//absl/testing:parameterized",
        "@org_tensorflow//tensorflow:tensorflow_py",
    ],
)

py_library(
    name = "tree_transformations",
    srcs = ["tree_transformations.py"],
    srcs_version = "PY3",
    deps = [
        ":building_block_analysis",
        ":building_block_factory",
        ":building_blocks",
        ":compiled_computation_transforms",
        ":intrinsic_defs",
        ":transformation_utils",
        ":tree_analysis",
        "//tensorflow_federated/python/common_libs:py_typecheck",
        "//tensorflow_federated/python/core/impl/types:type_transformations",
    ],
)

py_test(
    name = "tree_transformations_test",
    size = "small",
    srcs = ["tree_transformations_test.py"],
    args = [
        "--golden",
        "$(location tree_transformations_test_goldens/remove_duplicate_federated_aggregate.expected)",
        "--golden",
        "$(location tree_transformations_test_goldens/remove_duplicate_federated_broadcast.expected)",
        "--golden",
        "$(location tree_transformations_test_goldens/remove_duplicate_complex_comp.expected)",
    ],
    data = [
        "tree_transformations_test_goldens/remove_duplicate_complex_comp.expected",
        "tree_transformations_test_goldens/remove_duplicate_federated_aggregate.expected",
        "tree_transformations_test_goldens/remove_duplicate_federated_broadcast.expected",
    ],
    python_version = "PY3",
    srcs_version = "PY3",
    deps = [
        ":building_block_factory",
        ":building_blocks",
        ":intrinsic_defs",
        ":test_utils",
        ":tree_analysis",
        ":tree_transformations",
        "//tensorflow_federated/python/common_libs:golden",
        "//tensorflow_federated/python/common_libs:py_typecheck",
        "//tensorflow_federated/python/core/api:test_case",
        "//tensorflow_federated/python/core/impl/types:computation_types",
        "//tensorflow_federated/python/core/impl/types:placements",
        "@absl_py//absl/testing:parameterized",
        "@org_tensorflow//tensorflow:tensorflow_py",
    ],
)
