# federation-text-surface

Federation **TextSurface substrate** — AvalonEdit mirror submodule + customization layer ([GUIDERS-ADR-0066 §4.1](https://github.com/AI-Guiders/guiders-platform/blob/main/docs/adr/GUIDERS-ADR-0066-code-center-federation-product.md)).

## Two-repo model

| Repo | Role |
|------|------|
| [AI-Guiders/AvalonEdit](https://github.com/AI-Guiders/AvalonEdit) | **Mirror-fork** of [icsharpcode/AvalonEdit](https://github.com/icsharpcode/AvalonEdit) — upstream sync only, no federation patches |
| **This repo** | Product substrate — submodule pin + federation peel types |

Planets and `guiders-wpf` **must not** reference AvalonEdit NuGet directly; consume `AIGuiders.TextSurface.Substrate` (then `Surface.Wpf.TextEngine` / Code Center).

## Layout

```text
vendor/AvalonEdit/          git submodule → AI-Guiders/AvalonEdit @ tag (see .gitmodules)
src/AIGuiders.TextSurface.Substrate/   LanguageTextEditor peel + ProjectReference to vendor
docs/UPSTREAM-BUMP.md       operator ritual
```

## Pin

Current submodule: **v6.3.1** (`862415d`) — matches NuGet 6.3.1.120 baseline in guiders-wpf TextEngine peel.

## Build

```bash
dotnet build FederationTextSurface.slnx -c Release
```
