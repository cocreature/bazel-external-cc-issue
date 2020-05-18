workspace(name = "bazel_dcc_external")

load(
    "@bazel_tools//tools/build_defs/repo:http.bzl",
    "http_archive"
)

http_archive(
    name = "rules_haskell",
    strip_prefix = "rules_haskell-a9930c7856d251718613cca7a75f83aa911bf725",
    urls = ["https://github.com/tweag/rules_haskell/archive/a9930c7856d251718613cca7a75f83aa911bf725.tar.gz"],
    sha256 = "f23deee19fabd8317cd66ac531169e2f332bb9420676de4d1429384ebfd5d74a",
    patches = ["@bazel_dcc_external//:cc.patch"],
    patch_args = ["-p1"],
)

load(
    "@rules_haskell//haskell:repositories.bzl",
    "rules_haskell_dependencies",
)

rules_haskell_dependencies()

load(
    "@rules_haskell//haskell:ghc_bindist.bzl",
    "haskell_register_ghc_bindists",
)

haskell_register_ghc_bindists(
    version = "8.6.5",
)
