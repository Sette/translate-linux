# notitrans

Traduza rapidamente para português do Brasil um texto selecionado no desktop Linux. O `notitrans` lê a seleção ativa, solicita a tradução e abre o resultado em uma janela do Zenity. Você pode associar o comando a um atalho de teclado para traduzir sem abrir um terminal.

## Como funciona

Ao executar, o script:

1. Lê o texto selecionado com `xsel`.
2. Envia o texto pela internet ao endpoint público de tradução do Google, com detecção automática do idioma de origem e destino `pt-br`.
3. Mostra o texto original e a tradução em uma janela do `zenity`.

É necessário estar conectado à internet. O texto selecionado é enviado ao serviço de tradução; evite usar o programa com conteúdo confidencial. O projeto é um script pequeno que usa um endpoint público, sem garantia de disponibilidade ou compatibilidade contínua.

## Requisitos

Em distribuições baseadas em Debian ou Ubuntu, instale as dependências com:

```sh
sudo apt-get update
sudo apt-get install libnotify-bin wget xsel zenity
```

O script usa `xsel` para acessar a seleção do X11 e `zenity` para exibir o resultado. Portanto, precisa ser executado em uma sessão gráfica compatível com essas ferramentas.

## Instalação

Clone ou baixe este repositório e, no diretório do projeto, torne o script executável:

```sh
chmod +x notitrans
```

Para instalá-lo para todos os usuários:

```sh
sudo install -m 755 notitrans /usr/local/bin/notitrans
```

Ou execute diretamente do diretório do projeto:

```sh
./notitrans
```

## Uso

Selecione um texto em um aplicativo e execute `notitrans`. Uma janela mostrará o conteúdo original e a tradução. Também é possível configurar `notitrans` como atalho de teclado nas configurações do seu ambiente de desktop. Por exemplo, crie um atalho personalizado cujo comando seja:

```text
notitrans
```

O caminho para configurar atalhos varia entre GNOME, KDE Plasma, Xfce e outros ambientes. Depois de criar o atalho, selecione o texto que deseja traduzir e pressione a combinação escolhida.

## Limitações

- O idioma de destino está definido no script como português do Brasil (`pt-br`); o idioma de origem é detectado automaticamente.
- A leitura da seleção depende do `xsel` e do mecanismo de seleção do X11. Em sessões Wayland, o acesso à seleção pode não funcionar conforme esperado.
- O script depende de um endpoint público de tradução e de conexão com a internet.
- Se não houver texto selecionado, ou se a tradução falhar, a janela pode aparecer sem uma tradução útil.

## Solução de problemas

- **O comando não é encontrado:** confirme que `/usr/local/bin` está no `PATH`, ou execute `./notitrans` no diretório do projeto.
- **A janela não aparece:** verifique se `zenity` está instalado e se o comando foi iniciado dentro da sessão gráfica.
- **O texto não é lido:** confirme que há uma seleção ativa e que `xsel` está instalado. Em Wayland, pode ser necessário usar uma sessão X11.
- **A tradução não retorna:** confira a conexão com a internet e tente novamente mais tarde; o serviço remoto pode estar indisponível.
