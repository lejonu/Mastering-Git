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
