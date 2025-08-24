# WORKSPACE
load("@bazel_tools//tools/build_defs/repo:http.bzl", "http_archive")

http_archive(
    name = "rules_python",
    sha256 = "0a1cefefb4a7b550fb0b43f54df67d6da95b7ba352637669e46c987f69986f6a",
    strip_prefix = "rules_python-1.5.3",
    url = "https://github.com/bazel-contrib/rules_python/releases/download/1.5.3/rules_python-1.5.3.tar.gz",
)

load("@rules_python//python:repositories.bzl", "py_repositories", "python_register_toolchains")

py_repositories()

# Register Python toolchain
python_register_toolchains(
    name = "python3_10",
    python_version = "3.10",  # Match your existing Python environment
)

load("@rules_python//python:pip.bzl", "pip_parse")

pip_parse(
    # (Optional) You can set an environment in the pip process to control its
    # behavior. Note that pip is run in "isolated" mode so no PIP_<VAR>_<NAME>
    # style env vars are read, but env vars that control requests and urllib3
    # can be passed
    # environment = {"HTTPS_PROXY": "http://my.proxy.fun/"},
    name = "pypi",

    # (Optional) You can set quiet to False if you want to see pip output.
    #quiet = False,
    requirements_lock = "//:requirements_lock.txt",
)

load("@pypi//:requirements.bzl", "install_deps")

# Initialize repositories for all packages in requirements_lock.txt.
install_deps()
