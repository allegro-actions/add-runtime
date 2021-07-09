# allegro-actions/add-runtime

This action downloads popular runtime binaries for your packaging process.

## Basic usage:

```yaml
steps:
  - uses: allegro-actions/add-runtime/node@v1
    with:
      version: 16.0.0
      os: linux-x64
      target: runtime
```

```yaml
steps:
  - uses: allegro-actions/add-runtime/deno@v1
    with:
      version: 1.11.5
      os: linux-x64
      target: runtime
```

## Supported operating systems

- linux 64bit

Feel free to add more!

## Supported runtimes

- nodejs
- deno

Feel free to add more!

## Use cases

When you're combining your sourcecode with runtime binaries to be later executed in a runner:

```yaml
steps:
  - uses: actions/checkout@v2

  - name: download node to "runtime" directory
    uses: allegro-actions/add-runtime/node@v1
    with:
      version: 16.0.0
      os: linux-x64
      target: runtime

  - name: package app with runtime and create an artifact
    uses: allegro-actions/artifactory-publish@v1
    with:
      host: company.artifactory.allegro
      username: ${{ secrets.ARTIFACTORY_USERNAME }}
      password: ${{ secrets.ARTIFACTORY_PASSWORD }}
      name: opbox-web
      group: pl.allegro.opbox
      buildDir: ./build-web
      version: 2.0.0
  ```

Then the application can be run started using your own runtime: `./runtime/node index.js`