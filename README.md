# rox-pack

Distribuição do pacote **R O X** para o [UltraNX](https://github.com/mathst/ultranx).

Este repositório não tem código: cada **release** (`vX.Y.Z`) carrega as partes
`.zip` do pacote e o `manifest.json`. O app no Switch e o app de PC leem sempre

```
https://github.com/mathst/rox-pack/releases/latest/download/manifest.json
```

então publicar uma release nova marcada como *latest* é o que faz todos os
consoles enxergarem a atualização. O endereço é fixo no binário do app.

## Arquivos

| Arquivo | Para quê |
| --- | --- |
| `cleanup.json` | O que o app apaga antes de extrair (`delete`), as pastas limpas item a item (`delete_children`) e o que preserva além do padrão (`preserve`). Vai para o bloco `cleanup` do manifest. |

Saves, `emummc`, `Nintendo`, `*.keys` e `JKSV` são protegidos pelo próprio app
e nenhum manifest consegue apagá-los.

## Publicar uma versão

Gerado por `tools/make_release.py` do repositório `ultranx` (fatia o pacote em
partes ≤ 1,9 GB, calcula SHA-256 e escreve o manifest):

```bash
python tools/make_release.py pacote/ --version 1.5.0 --cleanup ../rox-pack/cleanup.json \
  --base-url https://github.com/mathst/rox-pack/releases/download/v1.5.0/ --out dist/v1.5.0
gh release create v1.5.0 dist/v1.5.0/* --repo mathst/rox-pack --latest
```

Rollback: marcar a release anterior como *latest*.

> Repositório **público** de propósito: o console baixa sem token. Quem pode
> publicar release aqui controla o que é instalado em todos os consoles — mantenha
> 2FA ativo na conta.
