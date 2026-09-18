# Upstream bump ritual (AvalonEdit)

Normative for **AI-Guiders/AvalonEdit** (mirror) + this repo (product).

## 1. Sync mirror (no federation patches)

```bash
cd ../AvalonEdit   # or clone AI-Guiders/AvalonEdit
git fetch upstream
git checkout master
git merge upstream/master
git push origin master
git tag -l 'v6.*'   # note new release tag
```

## 2. Bump submodule in federation-text-surface

```bash
cd vendor/AvalonEdit
git fetch --tags
git checkout vX.Y.Z
cd ../..
git add vendor/AvalonEdit
git commit -m "chore(upstream): bump AvalonEdit submodule to vX.Y.Z"
```

## 3. Verify

```bash
dotnet build FederationTextSurface.slnx -c Release
```

## 4. Downstream

- `guiders-wpf` TextEngine peel already references `AIGuiders.TextSurface.Substrate` — rebuild CodeCenter + WPF tests after bump
- Studio smoke (document zone completion + structural `/` insert)
- Living matrix `ship-avalonedit-phase4` note + `FederationPhase4ChecklistTests` gate

**Rule:** never commit federation customization into `AI-Guiders/AvalonEdit` — only here (`src/`, `patches/` if added later).
