load('@build_bazel_rules_apple//apple:resources.bzl', 'apple_bundle_import')
load('@build_bazel_rules_apple//apple:apple.bzl', 'apple_static_framework_import')
load(
  "//Vendor/rules_pods/BazelExtensions:extensions.bzl",
  "pch_with_name_hint",
  "acknowledged_target",
  "gen_module_map",
  "gen_includes"
  )
# Add a config setting release for compilation mode
# Assume that people are using `opt` for release mode
# see the bazel user manual for more information
# https://bazel.build/versions/master/docs/bazel-user-manual.html
native.config_setting(
  name = "release",
  values = {
    "compilation_mode": "opt"
  }
  )
filegroup(
  name = "GoogleAppIndexing_hdrs",
  srcs = glob(
    [
      "pod_support/Headers/Public/**/*"
    ],
    exclude_directories = 1
    ) + glob(
    [
      "Changelog/**/*.h",
      "Changelog/**/*.hpp",
      "Changelog/**/*.hxx"
    ],
    exclude_directories = 1
    ) + [

  ],
  visibility = [
    "//visibility:public"
  ]
  )
gen_includes(
  name = "GoogleAppIndexing_includes",
  include = [
    "Vendor/GoogleAppIndexing/pod_support/Headers/Public/"
  ]
  )
gen_module_map(
  "GoogleAppIndexing",
  "GoogleAppIndexing_module_map",
  "GoogleAppIndexing",
  [
    "GoogleAppIndexing_hdrs"
  ]
  )
objc_library(
  name = "GoogleAppIndexing",
  enable_modules = 1,
  hdrs = [
    ":GoogleAppIndexing_hdrs",
    ":GoogleAppIndexing_module_map_module_map_file"
  ],
  pch = pch_with_name_hint(
    "GoogleAppIndexing",
    [

    ]
    ),
  includes = [
    "GoogleAppIndexing_module_map"
  ],
  sdk_frameworks = [
    "CoreText",
    "SafariServices"
  ],
  deps = [
    ":GoogleAppIndexing_Bundle_GoogleAppIndexingResources",
    ":GoogleAppIndexing_VendoredFrameworks"
  ] + [
    ":GoogleAppIndexing_includes"
  ],
  copts = [
    "-Wno-everything",
    "-Wnon-modular-include-in-framework-module",
    "-g",
    "-stdlib=libc++",
    "-DCOCOAPODS=1",
    "-DOBJC_OLD_DISPATCH_PROTOTYPES=0",
    "-fdiagnostics-show-note-include-stack",
    "-fno-common",
    "-fembed-bitcode-marker",
    "-fmessage-length=0",
    "-fpascal-strings",
    "-fstrict-aliasing",
    "-Wno-error=nonportable-include-path"
  ] + select(
    {
      "//conditions:default": [
        "-DPOD_CONFIGURATION_RELEASE=0"
      ],
      ":release": [
        "-DPOD_CONFIGURATION_RELEASE=1",
        "-DNS_BLOCK_ASSERTIONS=1"
      ]
    }
    ) + [
    "-IVendor/GoogleAppIndexing/pod_support/Headers/Public/GoogleAppIndexing/"
  ] + [
    "-fmodule-name=GoogleAppIndexing_pod_module"
  ],
  data = [
    ":GoogleAppIndexing_Bundle_GoogleAppIndexingResources"
  ],
  visibility = [
    "//visibility:public"
  ]
  )
acknowledged_target(
  name = "GoogleAppIndexing_acknowledgement",
  deps = [

  ],
  value = "//Vendor/GoogleAppIndexing/pod_support_buildable:acknowledgement_fragment"
  )
apple_bundle_import(
  name = "GoogleAppIndexing_Bundle_GoogleAppIndexingResources",
  bundle_imports = glob(
    [
      "Resources/GoogleAppIndexingResources.bundle/**"
    ],
    exclude_directories = 1
    )
  )
apple_static_framework_import(
  name = "GoogleAppIndexing_VendoredFrameworks",
  framework_imports = glob(
    [
      "Frameworks/GoogleAppIndexing.framework/**"
    ],
    exclude_directories = 1
    ),
  visibility = [
    "//visibility:public"
  ]
  )