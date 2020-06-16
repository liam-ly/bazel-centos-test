workspace(name="TestProject")
load("@bazel_tools//tools/build_defs/repo:git.bzl", "git_repository")
load("@bazel_tools//tools/build_defs/repo:http.bzl", "http_archive")
git_repository(
    name="rules_haskell",
    remote="https://github.com/tweag/rules_haskell.git",
    commit="ea3f13165dae68d5c0291ef258fb1cd51ea0372d",  # 0.12 works
    # commit="57081449c34c0a3de429759837f61a0b70a8f3e2",  # latest master doesn't
)
load("@rules_haskell//haskell:repositories.bzl", "rules_haskell_dependencies")
rules_haskell_dependencies()
load("@rules_haskell//haskell:toolchain.bzl", "rules_haskell_toolchains")
rules_haskell_toolchains(
    version="8.6.5",
    compiler_flags=["-optc-std=c99"],
    locale = "en_US.UTF-8",
)
http_archive(
    name="alex",
    build_file_content="""
load("@rules_haskell//haskell:cabal.bzl", "haskell_cabal_binary")
haskell_cabal_binary(
    name="alex",
    srcs=glob(["**"]),
    visibility=["//visibility:public"],
    compiler_flags=["-optc-std=c99"],
    verbose=False,
)
""",
    strip_prefix="alex-3.2.4",
    urls=["https://hackage.haskell.org/package/alex-3.2.4/alex-3.2.4.tar.gz"],
    sha256="d58e4d708b14ff332a8a8edad4fa8989cb6a9f518a7c6834e96281ac5f8ff232",
)
load("@rules_haskell//haskell:cabal.bzl", "stack_snapshot")
stack_snapshot(
    name="stackage",
    tools=["@alex"],
    snapshot="lts-14.27",
    haddock=False,
    visibility=["//visibility:public"],
    packages=[
        "zlib",
    ]
)