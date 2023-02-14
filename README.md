# Nuxt 3 bazel example

This project aims to provide an example of how to build and package a nuxt 3 project with SSR into a container.

## How to run

Run the following command to build and export the application to your local docker installation.
```sh
bazel run :image
```

Execute the following command to start the container
```sh
docker run -it --rm -p 3000:3000 bazel:image
```

## Problems

### Build errors

When trying to execute `bazel build :build` we get the following error:

```sh
ERROR: /.../nuxt-3-testing/BUILD.bazel:27:5: NpmPackageBin build failed: (Exit 1): nuxt.sh failed: error executing command (from target //:build) bazel-out/k8-opt-exec-2B5CBBC6/bin/external/npm/nuxt/bin/nuxt.sh build '--bazel_node_modules_manifest=bazel-out/k8-fastbuild/bin/_build_NpmPackageBin.module_mappings.json'

Use --sandbox_debug to see verbose messages from the sandbox and retain the sandbox build root for debugging

 ERROR  Error: EACCES: permission denied, open '.../.cache/bazel/_bazel_jw/5a7eed751835ac4c29776d65ec606af8/sandbox/linux-sandbox/2162/execroot/__main__/.output/server/node_modules/iron-webcrypto/package.json'


undefined


 ERROR  EACCES: permission denied, open '.../.cache/bazel/_bazel_jw/5a7eed751835ac4c29776d65ec606af8/sandbox/linux-sandbox/2162/execroot/__main__/.output/server/node_modules/iron-webcrypto/package.json'
```

Because the I cannot get the build command to work we have to build everything in a container using the `container_run_and_commit_layer` utility...

### Hot reload

Haven't added hot reloading then running the `bazel run :dev` command. Use `yarn install` and `yarn dev` for a better experience.
