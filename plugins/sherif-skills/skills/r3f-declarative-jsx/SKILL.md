---
name: "r3f-declarative-jsx"
description: "Use when writing or reviewing React Three Fiber (r3f) code: keep every scene object, material and geometry as declarative r3f JSX, never scene.add, primitive, or new THREE.* materials."
---

# Declarative r3f JSX only

In any React Three Fiber project, the scene graph is written as JSX. Treat this as a hard rule.

## Do
- Build objects as JSX: `<mesh>`, `<group>`, `<instancedMesh>`, lights, cameras.
- Declare geometry and materials as children with props: `<boxGeometry args={[w, h, d]} />`, `<meshStandardMaterial color={c} map={tex} roughness={0.6} />`.
- Load assets with hooks (`useTexture`, `useGLTF`, `useLoader`) inside `<Suspense>` with a fallback, so materials are created with their maps already present.
- Use drei components (`<Text>`, `<Line>`, `<Edges>`, `<Environment>`, etc.) before writing anything imperative.
- Express changes as props/state; for per-frame animation use `useFrame` with a ref to mutate transforms, not to create objects.
- Share a material or geometry by declaring it once and passing it via `attach` or by reusing a component, not by constructing it in TypeScript.

## Don't
- `scene.add(...)` / `object.add(...)` / `scene.remove(...)`.
- `<primitive object={...} />` for objects you construct yourself.
- `new THREE.MeshStandardMaterial(...)`, `new THREE.BoxGeometry(...)`, `new THREE.Mesh(...)` in TS/TSX to then hand to the scene.
- Hand-rolled texture loaders that return null until loaded (a material first compiled without a map won't pick it up later).

## Exceptions
Only when r3f JSX genuinely cannot express it (e.g. rendering a loaded GLTF scene with `<primitive object={gltf.scene} />`, or a library that only returns a THREE object). Keep the exception small, comment why, and call it out to the user in the PR or reply rather than adding it silently.

## When reviewing or refactoring
1. Search for `scene.add`, `.add(`, `<primitive`, `new THREE.` and list each hit.
2. Convert each to JSX, keeping visuals identical; verify in the running app.
3. If the project has a CLAUDE.md, make sure this rule is written there too.