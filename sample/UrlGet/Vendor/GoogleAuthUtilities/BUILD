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
  name = "GoogleAuthUtilities_hdrs",
  srcs = glob(
    [
      "pod_support/Headers/Public/**/*"
    ],
    exclude_directories = 1
    ) + [

  ] + [

  ],
  visibility = [
    "//visibility:public"
  ]
  )
gen_includes(
  name = "GoogleAuthUtilities_includes",
  include = [
    "Vendor/GoogleAuthUtilities/pod_support/Headers/Public/"
  ]
  )
gen_module_map(
  "GoogleAuthUtilities",
  "GoogleAuthUtilities_module_map",
  "GoogleAuthUtilities",
  [
    "GoogleAuthUtilities_hdrs"
  ]
  )
objc_library(
  name = "GoogleAuthUtilities",
  enable_modules = 1,
  hdrs = [
    ":GoogleAuthUtilities_hdrs",
    ":GoogleAuthUtilities_module_map_module_map_file"
  ],
  pch = pch_with_name_hint(
    "GoogleAuthUtilities",
    [

    ]
    ),
  includes = [
    "GoogleAuthUtilities_module_map"
  ],
  sdk_frameworks = [
    "Security",
    "SystemConfiguration"
  ],
  deps = [
    "//Vendor/GoogleNetworkingUtilities:GoogleNetworkingUtilities",
    "//Vendor/GoogleSymbolUtilities:GoogleSymbolUtilities",
    ":GoogleAuthUtilities_VendoredFrameworks"
  ] + [
    ":GoogleAuthUtilities_includes"
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
    "-IVendor/GoogleAuthUtilities/pod_support/Headers/Public/GoogleAuthUtilities/"
  ] + [
    "-fmodule-name=GoogleAuthUtilities_pod_module"
  ],
  data = glob(
    [
      "Frameworks/frameworks/GoogleAuthUtilities.framework/Resources/GTMOAuth2ViewTouch.xib"
    ],
    exclude_directories = 1
    ),
  visibility = [
    "//visibility:public"
  ]
  )
acknowledged_target(
  name = "GoogleAuthUtilities_acknowledgement",
  deps = [
    "//Vendor/GoogleNetworkingUtilities:GoogleNetworkingUtilities_acknowledgement",
    "//Vendor/GoogleSymbolUtilities:GoogleSymbolUtilities_acknowledgement"
  ],
  value = "//Vendor/GoogleAuthUtilities/pod_support_buildable:acknowledgement_fragment"
  )
apple_static_framework_import(
  name = "GoogleAuthUtilities_VendoredFrameworks",
  framework_imports = glob(
    [
      "Frameworks/frameworks/GoogleAuthUtilities.framework/**"
    ],
    exclude_directories = 1
    ),
  visibility = [
    "//visibility:public"
  ]
  )