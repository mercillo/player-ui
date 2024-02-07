load("@aspect_rules_js//js:defs.bzl", "js_library", "js_test")
load("@aspect_rules_ts//ts:defs.bzl", "ts_config")
load("@bazel_skylib//rules:build_test.bzl", "build_test")
load("@npm//:defs.bzl", "npm_link_all_packages")
load("@npm//next.js:next/package_json.bzl", next_bin = "bin")
# load("@rules_player//javascript/next:next_build.bzl", "next_export")
load("@npm//next:index.bzl", "next")
load("//site:defs.bzl","next")
npm_link_all_packages(name = "node_modules")

next_bin.next_binary(
    name = "next_js_binary",
    visibility = ["//visibility:public"],
)

ts_config(
    name = "tsconfig",
    src = "tsconfig.json",
    visibility = ["//visibility:public"],
)
srcs = glob([
  "public/**/*",
  "pages/**/*",
  "styles/*",
  "components/**/*",
  "plugins/*",
  "utils/*",
  "config/*",
]) + [
  "next.config.mjs",
  "next-env.d.ts",
  "tsconfig.json"
]

data = [
  "//react/player:@player-ui/react",
  "//plugins/reference-assets/react:@player-ui/reference-assets-plugin-react",
  "@npm//typescript",
  "@npm//@types/react",
  "@npm//@types/node",
  "@npm//@chakra-ui/react",
  "@npm//@chakra-ui/skip-nav",
  "@npm//@chakra-ui/icons",
  "@npm//@docsearch/react",
  "@npm//lunr",
  "@npm//globby",
  "@npm//react-icons",
  "@npm//fs-extra",
  "@npm//@mdx-js/loader",
  "@npm//@mdx-js/react",
  "@npm//react-syntax-highlighter",
  "@npm//remark",
  "@npm//remark-html",
  "@npm//remark-smartypants",
  "@npm//rehype-slug",
  "@npm//rehype-autolink-headings",
  "@npm//remove-markdown",
  "@npm//github-slugger",
  "@npm//gray-matter",
  "@npm//nextjs-google-analytics"
]

next(
    name = "next",
    srcs = srcs,
    data = data,
    next_bin = "./node_modules/next/dist/bin/next",
    next_js_binary = ":next_js_binary",
)

# next_export(
#   name = "site",
#   data = data,
#   srcs = srcs,
#   env = {
#     "NODE_ENV": "production",
#     # Need this b/c next will pull from env directly 
#     # This just maps to a value we can stamp w/ later on
#     "NEXT_PUBLIC_GA_MEASUREMENT_ID": "NEXT_PUBLIC_GA_MEASUREMENT_ID",
#   },
# )

# A smoke test on the artifact produced by the :next target
# js_test(
#     name = "build_smoke_test",
#     chdir = package_name(),
#     data = [":next"],
#     entry_point = "build_smoke_test.js",
# )

# js_library(
#     name = "package_json",
#     srcs = ["package.json"],
#     visibility = ["//visibility:public"],
# )

# js_library(
#     name = "jest_config",
#     srcs = ["jest.config.js"],
#     visibility = ["//visibility:public"],
#     deps = [":node_modules/next"],
# )

# js_library(
#     name = "eslintrc",
#     srcs = [".eslintrc.js"],
#     visibility = ["//:__subpackages__"],
#     deps = [
#         ":node_modules/@next/eslint-plugin-next",
#         ":node_modules/eslint-config-next",
#     ],
# )

# build_test(
#     name = "build_test",
#     targets = [
#         ":next",
#         # Not build testing the `:next_export` target since this `next export` writes back to the `.next` directory which
#         # causes issues with trying to write to an input. See https://github.com/vercel/next.js/issues/43344.
#         # TODO: fix in Next.js (https://github.com/vercel/next.js/issues/43344) or find work-around.
#         # ":next_export",
#     ],
# )