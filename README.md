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

### Salvando as alterações no repositório local

#### Para ver o status atual dos arquivos

```shell
git status
```

#### Adicionar os arquivos ao versionamento do Git

##### Todos os arquivos não ocultos

```shell
git add *
```

##### Todos os arquivos inclusive os ocultos

```shell
git add .
```

##### Um ou mais aquivos específicos

```shell
git add exemplo01.txt exemplo02.txt
```

Obs.: O Git não reconhece pastas sem arquivos. A convenção para pastas vazias é criar um arquivo oculto .gitkeep na pasta

```shell
echo pasta_vazia/.gitkeep
```

### Inserir os arquivos na nova versão

```shell
git commit -m "commit inicial"
```

#### Exibe o histórico de commits

```shell
git log
```

#### Exibe o histórico somente as mensagens dos commits

```shell
git reflog
```

### Ignorar pastas e arquivos

para ignorar pastas e arquivos, cria-se na raiz do projeto um arquivo oculto .gitignore contendo os caminhos.

#### Exemplo de arquivo .gitignore:

```txt
pasta/
arquivo.txt
*.c
```

### Desfazendo Alteracões no Repositório Local

#### Retorna ao último estado do arquivo:

```shell
git restore <arquivo>
```

Atenção! Este comando irá descartar todas as alterações feitas no arquivo ou nos arquivos

#### Altera a última mensagem de commit ou adiciona novos arquivos ao último commit:

```shell
git commit --amend -m "Esta será a mensagem do último commit"
```

```shell
git commit --amend -m
```

#### Desfazer o commit:

```shell
git log
```

Copiar o hash do commit a ser desfeito.

1. Retorna ao estado do hash informado e os arquivos posteriores para staging area:

```shell
git reset --soft <hash>
```

2. Retorna ao estado do hash informado e os arquivos para untraked files(comportamento padrão):

```shell
git reset --mixed <hash>
```

3. Retorna ao estado do hash informado, apagando os arquivos posteriores:

Cuidado!!!

```shell
git reset --hard <hash>
```

#### Descrição Detalhada dos Commits

```shell
git reflog
```

#### Retirar arquivos da área de preparação:

```shell
git reset <arquivo>
```

Outra opção:

```shell
git restore staged <arquivo>
```

### Enviando e Baixando Alterações com o Repositório Remoto

#### Enviar para um repositório existente no GitHub

```shell
git remote add origin <repositório>
```

#### Renomeia a branch caso você esteja trabalhando com a branch master:

```shell
git git branch -M main <repositório>
```

#### Envia as alterações do repositório Local para o Remoto:

```shell
git push -u origin main
```

### Editor remoto

Para abrir o editor remoto pressione a tecla (. ponto) no GitHub.

Ao editar remotamente o arquivo, as alterações não aparecerão no repositório local.

Será preciso fazer o pull do repositório.

```shell
git pull
```

### Trabalhando com Branches - Criando, Mesclando, Deletando e Tratando Conflitos

Para ver as branches

```shell
git log
```

#### Direciona para a branch indicada, se não existir, cria a nova branch:

```shell
git checkout -b <nome>
```

#### Lista o último commit de cada branch:

```shell
git branch -v
```

#### Mesclar a branch desejada com o a branch em uso:

```shell
git merge <nome-da-branch-a-ser-mesclada>
```

#### Excluir a branch desejada da branch em uso:

```shell
git merge git branch -d <nome-da-branch-a-ser-excluída>
```

### Resolvendo Conflitos de versões

#### Baixar as alterações feitas remotamente:

```shell
git pull
```

Decidir qual das alterações deve ser mantida e indicar para o Git.

Deletar as linhas que não serão aprovadas.

Adicionar o arquivo ao stage.

```shell
git add .
```

Fazer novo commit

```shell
git commit
```

Enviar para o repositório

```shell
git push origin main
```
