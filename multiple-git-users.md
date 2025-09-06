# 📌 Guia de Configuração de Perfis Git (Pessoal e Trabalho)

#### Este guia ensina a configurar dois perfis Git no mesmo usuário do Linux:

- **Pessoal** (GitHub pessoal)
- **Trabalho** (GitHub da empresa)

A configuração separa os repositórios em pastas diferentes e usa chaves SSH independentes para cada perfil.

---

---

---

## 📂 1. Estrutura de Diretórios

#### Crie a pasta `development` e duas subpastas:

```bash
mkdir -p ~/development/personal
mkdir -p ~/development/work
```

~/development/personal → Repositórios pessoais.

~/development/work → Repositórios de trabalho.

---

---

---

## ⚙️ 2. Arquivos de Configuração Git

#### Perfil Pessoal (~/.gitconfig-personal)

```bash
[user]
name = Seu Nome Pessoal
email = email.personal@gmail.com
```

#### Perfil Trabalho (~/.gitconfig-work)

```bash
[user]
name = Seu Nome Trabalho
email = email.work@company.com
```

---

---

---

## 🛠️ 3. Configuração Global do Git (~/.gitconfig)

```bash
[includeIf "gitdir:/home/$USER/development/personal/**"]
path = /home/$USER/.gitconfig-personal

[includeIf "gitdir:/home/$USER/development/work/**"]
path = /home/$USER/.gitconfig-work
```

---

---

---

## 🔑 4. Criar Chaves SSH Separadas

#### Pessoal

```bash
ssh-keygen -t ed25519 -C "email.personal@gmail.com" -f ~/.ssh/id_ed25519_personal
```

#### Trabalho

```bash
ssh-keygen -t ed25519 -C "email.work@company.com" -f ~/.ssh/id_ed25519_work
```

---

---

---

## 🗂️ 5. Configuração do SSH (~/.ssh/config)

# Conta Pessoal

```bash
Host github.com-personal
HostName github.com
User git
IdentityFile ~/.ssh/id_ed25519_personal
```

# Conta Trabalho

```bash
Host github.com-work
HostName github.com
User git
IdentityFile ~/.ssh/id_ed25519_work
```

---

---

---

## 🚀 6. Adicionar as Chaves ao SSH-Agent

```bash
eval "$(ssh-agent -s)"
ssh-add ~/.ssh/id_ed25519_personal
ssh-add ~/.ssh/id_ed25519_work
```

---

---

---

## 🌐 7. Registrar Chaves no GitHub

#### Pessoal:

```bash
cat ~/.ssh/id_ed25519_personal.pub
```

Adicione em GitHub → Settings → SSH and GPG keys → New SSH key.

#### Trabalho:

```bash
cat ~/.ssh/id_ed25519_work.pub
```

Adicione no GitHub da empresa em Settings → SSH and GPG keys → New SSH key.

---

---

---

## 📦 8. Criar e Inicializar Repositórios

#### Pessoal:

```bash
cd ~/development/personal
mkdir my-project
cd my-project
git init
```

#### Trabalho:

```bash
cd ~/development/work
mkdir project-company
cd project-company
git init
```

---

---

---

## 🔗 9. Configurar Remotes

#### Pessoal:

```bash
git remote add origin git@github.com-personal:user/personal-repo.git
```

#### Trabalho:

```bash
git remote add origin git@github.com-work:company/repo.git
```

---

---

---

## ✅ 10. Testes Finais

#### Verificar usuário configurado:

```bash
git config user.name
git config user.email
```

#### Testar conexão SSH:

```bash
ssh -T git@github.com-personal
ssh -T git@github.com-work
```

Você deverá receber mensagens de boas-vindas do GitHub para cada conta.
