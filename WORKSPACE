# Copyright 2016 Google Inc. All Rights Reserved.
#
# Licensed under the Apache License, Version 2.0 (the "License");
# you may not use this file except in compliance with the License.
# You may obtain a copy of the License at
#
#    http://www.apache.org/licenses/LICENSE-2.0
#
# Unless required by applicable law or agreed to in writing, software
# distributed under the License is distributed on an "AS IS" BASIS,
# WITHOUT WARRANTIES OR CONDITIONS OF ANY KIND, either express or implied.
# See the License for the specific language governing permissions and
# limitations under the License.
#
################################################################################
#

load(
    "//src/envoy/mixer:repositories.bzl",
    "mixer_client_repositories",
)

mixer_client_repositories()

load(
    "@mixerclient_git//:repositories.bzl",
    "googleapis_repositories",
    "mixerapi_repositories",
)

googleapis_repositories()

mixerapi_repositories()

bind(
    name = "boringssl_crypto",
    actual = "//external:ssl",
)

ENVOY_SHA = "2c7ee712a0795e79732546de8b01e1e7319d809c"  # Sep 20, 2017 (bugfix for envoy crash w/ HTTP2 promise frames)

http_archive(
    name = "envoy",
    strip_prefix = "envoy-" + ENVOY_SHA,
    url = "https://github.com/envoyproxy/envoy/archive/" + ENVOY_SHA + ".zip",
)

load("@envoy//bazel:repositories.bzl", "envoy_dependencies")

envoy_dependencies()

load("@envoy//bazel:cc_configure.bzl", "cc_configure")

cc_configure()

load("@envoy_api//bazel:repositories.bzl", "api_dependencies")

api_dependencies()

# Following go repositories are for building go integration test for mixer filter.
git_repository(
    name = "io_bazel_rules_go",
    commit = "7991b6353e468ba5e8403af382241d9ce031e571",  # Aug 1, 2017 (gazelle fixes)
    remote = "https://github.com/bazelbuild/rules_go.git",
)

git_repository(
    name = "org_pubref_rules_protobuf",
    commit = "9ede1dbc38f0b89ae6cd8e206a22dd93cc1d5637",
    remote = "https://github.com/pubref/rules_protobuf",
)

MIXER = "4235a86c20cf7667dd8b9f96a926a46f37e99c1c"

git_repository(
    name = "com_github_istio_mixer",
    commit = MIXER,
    remote = "https://github.com/istio/mixer",
)

load("@com_github_istio_mixer//test:repositories.bzl", "mixer_test_repositories")

mixer_test_repositories()
