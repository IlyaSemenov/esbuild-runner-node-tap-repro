## Prepare

```
yarn
```

## Test with `@swc-node/register`

Everything works as expected, it shows source code fully:

```
yarn tap --node-arg '-r' --node-arg '@swc-node/register' test.ts
```

emits:

```
 FAIL  test.ts
 ✖ should be equivalent

  test.ts
  1 | import tap from "tap"
  2 |
> 3 | tap.same("a", "b")
    | ----^

  --- expected
  +++ actual
  @@ -1,1 +1,1 @@
  -"b"
  +"a"
```

## Test with `esbuild-register`

It fails to parse sourcemap and show source code with proper line numbers:

```
yarn tap --node-arg '-r' --node-arg 'esbuild-register' test.ts
```

emits:

```
 FAIL  test.ts
 ✖ should be equivalent

  --- expected
  +++ actual
  @@ -1,1 +1,1 @@
  -"b"
  +"a"

  test: test.ts
  at:
    line: 20
    column: 20
    file: test.ts
  stack: |
    Object.<anonymous> (test.ts:20:20)
    Module.replacementCompile (node_modules/append-transform/index.js:60:13)
    Module._compile (node_modules/esbuild-register/dist/node.js:2258:26)
    module.exports (node_modules/default-require-extensions/js.js:7:9)
    node_modules/append-transform/index.js:64:4
    newLoader (node_modules/esbuild-register/dist/node.js:2262:9)
    Object.<anonymous> (node_modules/append-transform/index.js:64:4)
```
