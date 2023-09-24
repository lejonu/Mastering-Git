# Mastering Git

### Resumo do curso DIO Versionamento de Código com Git e GitHub - com Elidiana Andrade

## Instalação no Ubuntu

```shell
add-apt-repository ppa:git-core/ppa
apt update
apt install git
git --version
```

```txt
git version 2.42.0
```

## Configurções do Git

#### Configurações Locais

```shell
git config <opções>
```

#### Configurações Globais

```shell
git config --global <opções>
```

### Exemplos

#### Configuração Local de Usuário

```shell
git config user.name "userName"

git config user.email "email@servidor"

git config user.nickname "nickName"
```

#### Configuração Global de Usuário (Caso não haja outros usuários no sistema operacional em uso)

```shell
$ git config --global user.name "userName"

$ git config --global user.email "email@servidor"

$ git config --global user.nickname "nickName"
```

### Verificar as configurações do Git

```shell
# Retorna todas as configurações
git config  --list

# Retorna somente as configurações globais
git config --global --list
```

### Alterando o Branch padrão

#### Local:

git config init.defaultBranch main

#### Global:

git config --global init.defaultBranch main

### Autenticação

### Autenticando via token

- No GitHub vá na foto do usuário e selecione settings
- Na barra de menus selecione Developer settings
- Clique em Personal access token -> tokens(classic)
- Cliquen Generate new tokeon -> Generate new token(classic)
- Dê um nome para o token. Ex: Curso Git
- Selecione o prazo de expiração
- Selecione o escopo de acesso e clique em Generate token
- Copie o token

  Importante!!! : ao sair da página o token não será mais visto.

Ao conectar com um repositório usar o token gerado como password.

#### Salvar token na máquina

```shell
# máquina compartilhada com outros usuários
git config credential.helper cache
```

```shell
# máquina com único usuário
git config --global credential.helper store
```

### Autenticação via SSH

Começar verificando se existe a chave em nossa máquina.

```shell
ls -al ~/.ssh
```

\* Caso já exista a chave, você deverá decidir se usará a existe ou se irá deletá-la e criar uma nova.

#### Gerar nova chave ssh

```shell
# Usar o mesmo email do GitHub
ssh-keygen -t ed25519 -C "email@servidor"
```

#### Adicionar sua chave SSH ao ssh-agent

Iniciar o SSH agent

```shell
eval "$(ssh-agent -s)"
```

Adicionar a chave privada ao ssh agent

```shell
ssh-add ~/.ssh/id_ed25519
```

#### Adicionar a chave criada ou pré-existente ao GitHub

Abra o arquivo que contém a chave

```shell
cat ~/.ssh/id_ed25519.pub
```

copie a chave que começa com ssh e cole no campo indicado pelo GitHub.

### Criando um repositório local

Na pasta do projeto que se deseja versionar:

```shell
git init
```

Este comando criará a pasta oculta .git com os arquivos iniciais de configuração do Git.

### Clonar um repositório existente no GitHub

```shell
git clone <nome-do-repositório>
```

#### Clonar um repositório existente no GitHub alterando o nome

```shell
git clone git@github.com:lejonu/Mastering-Git.git Mastering-Git-Clonado
```

#### Mostra os repositórios que estão vinculados.

```shell
git remote -v
```

#### Vincula o repositório local ao remoto

```shell
git remote add origin url-do-repositório
```
