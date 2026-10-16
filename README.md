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

Depois de instalar o script, configure o atalho pela interface gráfica do ambiente de desktop:

1. Abra **Configurações** e procure por **Teclado** ou **Atalhos de teclado**.
2. Escolha **Atalhos personalizados** (ou opção equivalente) e adicione um atalho.
3. Defina um nome, como **Traduzir seleção**, e informe `notitrans` como comando. Se não instalou o script em `/usr/local/bin`, informe o caminho completo para o arquivo, por exemplo `/caminho/para/translate-linux/notitrans`.
4. Use a opção para definir a combinação de teclas e pressione as teclas que deseja associar.
5. Salve o atalho. Selecione um texto em outro aplicativo e pressione a combinação escolhida; a janela exibirá o texto original e a tradução.

Os nomes e a localização dessas opções variam conforme o ambiente. No GNOME, procure **Configurações → Teclado → Atalhos de teclado → Ver e personalizar atalhos → Atalhos personalizados**. No KDE Plasma, procure **Configurações do sistema → Teclado → Atalhos**; no Xfce, **Configurações → Teclado → Atalhos de aplicativos**. Em cada caso, escolha a opção para adicionar um atalho personalizado.

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
