# vize-imports-template-ref-repro

Minimal reproduction: the Vize content mapper does not infer the type of `useTemplateRef("key")` when the function is imported from `#imports` (the Nuxt import alias).

## Steps

```bash
pnpm install
pnpm check
```

## Actual

```
src/FromImports.vue(7,22): error TS2339: Property 'reportValidity' does not exist on type '{}'.
```

## Expected

No errors. `src/FromImports.vue` and `src/FromVue.vue` are the same, except for the import source:

| File | Import | Result |
|---|---|---|
| `src/FromVue.vue` | `import { useTemplateRef } from "vue"` | `form` is `HTMLFormElement \| null` |
| `src/FromImports.vue` | `import { useTemplateRef } from "#imports"` | `form` is `{}` |

`#imports` resolves to `imports.d.ts`, which re-exports `useTemplateRef` from `vue`. Nuxt generates the same file as `.nuxt/imports.d.ts`.
