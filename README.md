<div align="center">

<img src="https://raw.githubusercontent.com/mainuan/.github/main/profile/assets/mainuan-logo.svg" width="96" alt="Logotipo do Mainuan">

# Mainuan Icon Themes

Seis variações de cor do tema de ícones Kora para o **Mainuan Linux**, empacotadas como `mainuan-icon-themes`.

[![CI](https://github.com/mainuan/icons/actions/workflows/ci.yml/badge.svg)](https://github.com/mainuan/icons/actions/workflows/ci.yml)
[![Release](https://img.shields.io/github/v/release/mainuan/icons)](https://github.com/mainuan/icons/releases)
[![Licença](https://img.shields.io/github/license/mainuan/icons)](LICENSE)
![Base](https://img.shields.io/badge/base-Kubuntu%2026.04%20LTS-0079c1)
![Plasma](https://img.shields.io/badge/KDE%20Plasma-6.6-1d99f3)

[English](README.en.md)

</div>

---

| <img src="docs/previews/folder-kora-cyan.svg" width="72" alt="Pasta do Kora Ciano"> | <img src="docs/previews/folder-kora-grey.svg" width="72" alt="Pasta do Kora Cinza"> | <img src="docs/previews/folder-kora-magenta.svg" width="72" alt="Pasta do Kora Magenta"> | <img src="docs/previews/folder-kora-violet.svg" width="72" alt="Pasta do Kora Violet"> | <img src="docs/previews/folder-kora-brown.svg" width="72" alt="Pasta do Kora Marrom"> | <img src="docs/previews/folder-kora-lima.svg" width="72" alt="Pasta do Kora Lima"> |
|:-:|:-:|:-:|:-:|:-:|:-:|
| `kora-cyan` | `kora-grey` | `kora-magenta` | `kora-violet` | `kora-brown` | `kora-lima` |

O ícone de pasta (`places/scalable/folder.svg`) de cada tema, copiado sem
alterações para `docs/previews/`.

## O que é

O Mainuan tem seis cores de destaque, e cada uma tem um tema de ícones Kora
próprio. O pacote Debian `mainuan-icon-themes` instala os seis em
`/usr/share/icons`, e o Plasma os lista em **Configurações do sistema >
Cores e temas > Ícones**.

O pacote vem instalado na ISO do Mainuan. O tema padrão das novas contas
(`kora-cyan`) é definido pelo
[`mainuan-desktop-defaults`](https://github.com/mainuan/dot-files).

## O que o pacote contém

| Pasta em `/usr/share/icons` | Nome no Plasma | Arquivo no repositório |
|---|---|---|
| `kora-brown` | Kora Marrom | `kora-brown.tar.gz` |
| `kora-cyan` | Kora Ciano | `kora-cyan.tar.gz` |
| `kora-grey` | Kora Cinza | `kora-grey.tar.gz` |
| `kora-lima` | Kora Lima | `kora-lima.tar.gz` |
| `kora-magenta` | Kora Magenta | `kora-magenta.tar.gz` |
| `kora-violet` | Kora Violet | `kora-violet.tar.gz` |

Os ícones que um tema não define vêm do Breeze e do hicolor
(`Inherits=breeze,hicolor`); o pacote recomenda `breeze-icon-theme` e
`hicolor-icon-theme`.

## Instalação

O pacote já vem na ISO do Mainuan. Para instalar ou atualizar à mão, baixe o
`.deb` e o `SHA256SUMS` da
[última release](https://github.com/mainuan/icons/releases/latest):

```bash
sha256sum --check --ignore-missing SHA256SUMS
sudo apt install ./mainuan-icon-themes_*_all.deb
```

O GitHub Releases não é um repositório APT: as atualizações chegam por novas
versões do pacote ou pela ISO.

## Como o pacote é montado

Os temas ficam no repositório como `kora-*.tar.gz`. Durante a compilação, o
script `debian/unpack-icon-themes`:

- recusa arquivos com membros fora da pasta do tema ou com `..`;
- remove o `icon-theme.cache` pré-gerado, scripts de manutenção (`*.sh`) e
  arquivos ocultos soltos;
- troca links simbólicos absolutos (que apontavam para a pasta pessoal de quem
  criou o tema) pelo ícone de mesmo nome na mesma pasta.

O cache de ícones é gerado na instalação, pelo `dh_icons`. Os temas usam
pastas próprias (`kora-*`) e não substituem nenhum arquivo de outro pacote.

## Adicionar ou atualizar um tema

1. Gere o arquivo `kora-<cor>.tar.gz` com uma única pasta `kora-<cor>/` na
   raiz, contendo o `index.theme`.
2. Para um tema novo, acrescente o nome à lista do teste de fumaça em
   `.github/workflows/ci.yml`.
3. Registre a mudança em `debian/changelog` (`dch -v <nova versão>`) e abra um
   pull request. A release é publicada quando a tag `v<versão>`, igual à de
   `debian/changelog`, é enviada.

## Informações técnicas

| Item | Valor |
|---|---|
| Pacote | `mainuan-icon-themes` (`Architecture: all`) |
| Destino | `/usr/share/icons/kora-*` |
| Base | Kubuntu 26.04 LTS, KDE Plasma 6.6 |
| Empacotamento | debhelper 13, formato `3.0 (native)` |
| Recomenda | `breeze-icon-theme`, `hicolor-icon-theme` |

## Compilação e testes

```bash
dpkg-buildpackage -us -uc -b
```

O [CI](.github/workflows/ci.yml) usa o pipeline compartilhado
[`mainuan/.github`](https://github.com/mainuan/.github) num contêiner
Ubuntu 26.04 e:

1. confere a sintaxe de `debian/unpack-icon-themes` e que o pacote-fonte não
   leva `.git` nem sobras de build;
2. compila com `dpkg-buildpackage` e passa o `lintian` (falha em erro);
3. instala o pacote num Ubuntu 26.04 limpo e, para cada tema, confere o cache
   gerado, ícones de referência, o `index.theme` (nome, herança e ao menos
   30 pastas declaradas) e a ausência de links quebrados ou absolutos;
4. reinstala, remove e expurga o pacote, sem sobras.

Uma tag `v<versão>` publica o `.deb` e o `SHA256SUMS` na release.

## Contribuição

Relate problemas em [Issues](https://github.com/mainuan/icons/issues) e envie
mudanças por pull request. O CI roda em cada pull request, em
[Actions](https://github.com/mainuan/icons/actions).

## Créditos

- **bikass**: autor do tema de ícones [Kora](https://github.com/bikass/kora),
  do qual as seis variações derivam.
- **Daigo** ([daigoasuka](https://github.com/daigoasuka)): variações de cor do
  Mainuan.
- **Rafael Ruscher** ([ruscher](https://github.com/ruscher)): empacotamento
  Debian e CI.

## Licença

Os temas de ícones Kora, de [bikass](https://github.com/bikass/kora), e as
variações de cor feitas pelo Mainuan são distribuídos sob a **GNU GPL
versão 3** (texto em [`LICENSE`](LICENSE)). Por serem derivados de uma obra
GPL-3, não podem ser relicenciados.

O trabalho próprio do Mainuan neste repositório (empacotamento em `debian/`
e documentação) é distribuído sob a **GNU GPL versão 2** (GPL-2.0), como
registra o [`debian/copyright`](debian/copyright).
