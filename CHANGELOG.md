# Changelog

<a name="1.0.0"></a>
## 1.0.0

> Released on November 15, 2026

### ✨ Features

- <details><summary><a href="https://github.com/maicol07/igdbclient/commit/3de8948d4dfc96bac8bb37bd0f6fcd8a965a030a"><code>3de8948</code></a> ✨ add wasmJs target</summary>

  > Add the wasmJs target (browser and Node.js) to igdbclient-core,
  > igdbclient-ktor and the test library. wasmJs shares the
  > kotlinx-serialization JSON parsers with native and JS targets.

  </details>
- <details><summary><a href="https://github.com/maicol07/igdbclient/commit/38593553065a3bc231d93a668a292f6f884822e7"><code>3859355</code></a> ✨ update IGDB schema with new endpoints and fields</summary>

  > Sync igdbapi.proto with https://api.igdb.com/v4/igdbapi.proto.
  >
  > New endpoints: age_rating_content_description_types, artwork_types,
  > company_sizes, company_types, company_type_histories, entity_types,
  > executables, image_types, logos, reports, report_types.
  >
  > New fields: AgeRatingContentDescriptionV2.description_type,
  > Artwork.image_type, Artwork.artwork_type (already deprecated upstream),
  > Company.company_size, Company.company_type_histories, Cover.image_type,
  > Game.executables, PlatformWebsite.type, ReleaseDate.d.

  </details>

### 🐛 Bug Fixes

- [`74cacba`](https://github.com/maicol07/igdbclient/commit/74cacbafc84accb56396043915cdb66ea370b4d8) 🐛 avoid function reference crashing Kotlin/Wasm incremental linking

### ♻️ Code Refactoring

- <details><summary><a href="https://github.com/maicol07/igdbclient/commit/a13a29bddb49304e64f9a95d93fd77dcd924f22c"><code>a13a29b</code></a> ♻️ share kotlinx-serialization JSON parsers between native and JS</summary>

  > Move the kotlinx-serialization based parsers from nativeMain to a new
  > "json" source set shared by native and JS targets, and drop the
  > kotlin.js.Json based JS implementation. This leaves one JSON parsing
  > implementation for all non-JVM targets and prepares for targets
  > without kotlin.js.Json (wasmJs).

  </details>

### 📝 Docs changes

- [`e3a026c`](https://github.com/maicol07/igdbclient/commit/e3a026c2a8c47d8a950d771371af4753eb64586a) 📝 document the fork and its Maven coordinates

### 👷 Building scripts changes

- <details><summary><a href="https://github.com/maicol07/igdbclient/commit/9ca9e797437de04f920f64a10a175aef2f02118c"><code>9ca9e79</code></a> ⬆️ bump Gradle, Kotlin and dependencies</summary>

  > - Gradle 9.2.1 -> 9.5.1 (AGP 8.x does not support Gradle 9.6+)
  > - Kotlin 2.2.10 -> 2.4.21; languageVersion/apiVersion 1.9 -> 2.0, the
  >   minimum supported by Kotlin 2.4; -Xjvm-default=all replaced by the
  >   equivalent -jvm-default=no-compatibility
  > - AGP 8.10.1 -> 8.13.2 (latest 8.x)
  > - kotlinx-coroutines 1.11.0, kotlinx-serialization 1.13.0, atomicfu 0.33.0
  > - ktor 3.6.1, okio 3.18.2, Wire 7.2.1, kermit 2.2.0, org.json 20260814
  > - okhttp 5.4.0, mockwebserver3 5.4.0 (from 5.0.0-alpha.17); 5.5.x
  >   requires compileSdk 37, which needs AGP 9
  > - dokka 2.3.0, gradle-maven-publish-plugin 0.37.0, spotless 8.11.0,
  >   binary-compatibility-validator 0.18.2
  > - junit 6.1.3, kotest 6.2.7, kctfork 0.14.0, kotlinpoet 2.4.0,
  >   slf4j 2.0.20, turbine 1.2.1
  > - Dependency verification metadata and keyring regenerated with
  >   --write-verification-metadata pgp,sha256 --export-keys

  </details>
- <details><summary><a href="https://github.com/maicol07/igdbclient/commit/b5af73bcf1d98854d42334ba81091b0f381ab584"><code>b5af73b</code></a> 🔧 update dependency verification and yarn locks for wasmJs on Kotlin 2.4</summary>

  > Combining the wasmJs target with the Kotlin 2.4 bump needs the wasm-only
  > artifacts (Node.js 26 for Kotlin/Wasm, wasm variants of the libraries)
  > in the verification metadata and refreshed yarn lock files.

  </details>
- <details><summary><a href="https://github.com/maicol07/igdbclient/commit/1a7ee92d7eb95f9264449f231e7f3746558db956"><code>1a7ee92</code></a> 🔧 publish the fork as it.maicol07.igdbclient</summary>

  > Maven groupId it.maicol07.igdbclient (the Kotlin package stays at.released.igdbclient), POM pointing to the fork, GitHub Packages repository and 1.0.0-SNAPSHOT as the local fallback version.

  </details>
- <details><summary><a href="https://github.com/maicol07/igdbclient/commit/7f15f75e06363e438cd1f9d1a6aa7c5d9fcbeaa8"><code>7f15f75</code></a> 🔐 trust Gradle&#x27;s new signing key in dependency verification</summary>

  > gradle/actions/setup-gradle injects org.gradle:github-dependency-graph-gradle-plugin 1.5.1 for dependency-graph: generate. It is signed by Gradle Inc.'s new signing subkey E2879931BCA1A42E55F2D64DD9B2DFBD9F3298BA (primary 15D543CA40743FFA47654C16622DE19DC011B9BE, created 2026-08-17), which was not trusted, so every CI job failed during init script evaluation.

  </details>
- <details><summary><a href="https://github.com/maicol07/igdbclient/commit/8801fe31810696db3cef55cfef92fd9c0c32ffba"><code>8801fe3</code></a> 🔐 verify Node.js 24.16.0 on all CI platforms</summary>

  > The verification metadata was generated on Windows and only had the win-x64 Node.js distribution, so Kotlin/JS tests failed on the macOS CI runners. Checksums for darwin-arm64, darwin-x64, linux-x64 and win-x64 come from the GPG-verified SHASUMS256.txt of the release, as for the other Node.js versions.

  </details>
- <details><summary><a href="https://github.com/maicol07/igdbclient/commit/638318e7fe8ffe03a6ef4136147d32aabb648b1a"><code>638318e</code></a> 🔐 verify Node.js 26.2.0 for Kotlin&#x2F;Wasm on all CI platforms</summary>

  > Same as for Node.js 24.16.0: add darwin-arm64, darwin-x64 and linux-x64 from the GPG-verified SHASUMS256.txt of the release.

  </details>
- <details><summary><a href="https://github.com/maicol07/igdbclient/commit/c7cbfa74d394af2ca3ebcf74875449a136ad3257"><code>c7cbfa7</code></a> 🚨 exclude the generated CHANGELOG.md from the Markdown style check</summary>

  > git-cliff writes CHANGELOG.md in the release PR with a trailing blank line, which failed spotlessMarkdownCheck.

  </details>

### 👷 CI changes

- <details><summary><a href="https://github.com/maicol07/igdbclient/commit/1d795f70318f30af3b82a75b7c59f7cd8f9d43d5"><code>1d795f7</code></a> 👷 move CI and releases to the maicol07&#x2F;actions workflows</summary>

  > ci.yml runs the existing Build.yml (now reusable) with the shared security and commit lint checks, publishes a snapshot to GitHub Packages on main, opens the git-cliff release PR and, once merged, publishes the release to Maven Central and GitHub Packages. Replaces Publish.yml.

  </details>

