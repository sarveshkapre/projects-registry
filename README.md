# Projects Registry

Single source of truth for `projects.md` across local repos.

## Local setup
This repo stores the canonical `projects.md`. On this machine, a symlink keeps the
legacy path working:

```
/Users/sarvesh/code/projects.md -> /Users/sarvesh/code/projects-registry/projects.md
```

This preserves tools that expect `projects.md` at the root of `/Users/sarvesh/code`.
If you prefer a different layout, update the symlink and point tools accordingly.
