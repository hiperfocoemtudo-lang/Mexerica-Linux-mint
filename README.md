# Mexerica-Linux-mint
Versão do tangerine para linux mint
# 🍊 Mexerica para Linux Mint Cinnamon

Converta arquivos com um gesto: **arraste, segure Shift e escolha um gomo**.

Esta adaptação do [Mexerica original](https://github.com/rogersocruz/mexerica), de Roger Augusto Souza da Cruz, integra conversões e ferramentas ao Linux Mint Cinnamon, com menus em português, animação de encaixe, fundo branco e destaque individual dos gomos.

## Recursos

- Conversões de imagens, vídeos, áudios, PDFs e documentos.
- Compactação de pastas e arquivos em ZIP, 7Z e TAR.GZ.
- Ferramentas para recortar, redimensionar, comprimir e remover fundo.
- Operações para juntar, separar e reorganizar PDFs.
- Ações para copiar caminho, copiar ou mover arquivos e abrir o terminal.
- Integração com o menu de contexto do Nemo.
- 18 composições de menu com 98 imagens de gomos individuais.

## Compatibilidade

Requer **Linux Mint 22 ou superior, Cinnamon e sessão X11**, com GTK 4.10 ou superior.

O gesto global não funciona em Cinnamon Wayland. Não é necessário instalar uma extensão do GNOME Shell.

## Instalação

1. Clique em **Code → Download ZIP**.
2. Extraia o arquivo.
3. Abra a pasta extraída no terminal.

Para instalar a Mexerica e os conversores:

```bash
bash install.sh
```

Para incluir a remoção de fundo por IA:

```bash
bash install.sh --with-background-removal
```

Execute como usuário normal. O script solicitará a senha para instalar dependências pelo APT. O aplicativo é instalado em `~/.local` e iniciado quando o instalador é executado na sessão gráfica.

Para adicionar a IA posteriormente:

```bash
bash install-background-removal.sh
```

## Como usar

Durante o arraste de um arquivo ou pasta:

| Atalho | Menu |
| --- | --- |
| **Shift** | Conversões |
| **Shift + Alt** | Ferramentas |
| **Shift + Ctrl** | Ações |

Passe sobre o gomo desejado e solte o botão do mouse para executar. Você pode trocar de menu durante o mesmo arraste.

Para cancelar, solte Shift ou solte o arquivo fora dos gomos.

As opções também estão disponíveis pelo botão direito do Nemo.

## Dependências

### Interface e sistema

- **Python 3** — o Mint 22 fornece Python 3.12.
- **PyGObject:** `python3-gi`.
- **Pycairo e integração com GTK:** `python3-cairo` e `python3-gi-cairo`.
- **GTK 4/Gdk 4:** `gir1.2-gtk-4.0`.
- **GTK 3/Gdk 3:** `gir1.2-gtk-3.0`, usado pelo leitor de arraste.
- **GLib, GObject, Gio, Pango e PangoCairo**, instalados como dependências do GTK.
- **Cinnamon, X11, libX11, sessão D-Bus e Nemo**.
- **Adwaita Icon Theme:** `adwaita-icon-theme`.
- **Registro de atalhos:** `desktop-file-utils`.
- **Bash, APT, sudo, util-linux e coreutils**, fornecidos pelo sistema.

### Conversores instalados automaticamente

| Pacote | Utilização |
| --- | --- |
| `ffmpeg` | Vídeo e áudio; inclui `ffprobe` e `ffplay` |
| `imagemagick` | Conversões e ferramentas de imagem; inclui `montage` |
| `poppler-utils` | `pdftoppm`, `pdftotext`, `pdfimages` e `pdfinfo` |
| `qpdf` | Organização, junção e divisão de PDFs |
| `ghostscript` | Processamento e compressão de PDFs |
| `libimage-exiftool-perl` | Leitura e remoção de metadados |
| `zbar-tools` | Leitura de QR codes |
| `libarchive-tools` | `bsdtar`, usado em arquivos compactados |
| `pandoc` | Conversões de texto, Markdown, EPUB e documentos |
| `libreoffice` | Documentos, planilhas e apresentações |

O APT resolve automaticamente as bibliotecas e codecs exigidos por esses programas.

### Remoção de fundo por IA — opcional

Requer **pipx**, **python3-venv** e **`rembg[cpu,cli]`**.

Suas dependências diretas são:

- Núcleo: `jsonschema`, `numpy`, `Pillow`, `pooch`, `pymatting`, `scikit-image`, `scipy` e `tqdm`.
- Processamento por CPU: `onnxruntime`.
- Linha de comando: `aiohttp`, `asyncer`, `click`, `fastapi`, `filetype`, `gradio`, `python-multipart`, `sniffio`, `uvicorn` e `watchdog`.

O pipx instala também as dependências transitivas. A [lista completa do ambiente de referência](docs/rembg-dependencias-referencia.txt) contém as 83 distribuições Python e suas versões. Essa lista documenta o ambiente testado; versões futuras do rembg podem exigir outras versões.

A IA executa localmente e pode baixar o modelo na primeira utilização. **CUDA e placa NVIDIA não são necessárias** para o modo CPU.

### Complementos opcionais

- `librsvg2-bin` / `rsvg-convert`: conversão dedicada de SVG.
- `typst`: geração de PDF em determinadas rotas do Pandoc.
- `xournalpp`: recursos de cadernos XOPP.
- Um emulador de terminal e aplicativos associados aos arquivos.

Esses complementos não são instalados automaticamente.

### Desenvolvimento

Para executar os testes:

```bash
sudo apt-get install python3-pytest make
make test
```

## Atualizar

Execute o instalador da versão nova. Se as dependências já estiverem instaladas:

```bash
bash install.sh --no-deps
```

## Diagnóstico

Verifique os conversores encontrados:

```bash
~/.local/bin/mexerica doctor
```

Os registros ficam em:

```text
~/.cache/mexerica/mexerica.log
```

## Desinstalar

```bash
bash uninstall.sh
```

O desinstalador preserva o cache, os conversores e o complemento de IA.

## Limitações

Os formatos disponíveis dependem das versões, codecs e políticas dos conversores. Algumas instalações do ImageMagick bloqueiam a escrita de PDF; o instalador não altera essa política.

As artes prontas cobrem os menus principais. Combinações adicionais de arquivos ou operações podem usar o desenho de apoio.

## Licença

Código sob licença **MIT**, com os créditos e o aviso de direitos autorais do projeto original preservados.
