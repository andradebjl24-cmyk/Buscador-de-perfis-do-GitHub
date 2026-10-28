# 🔎 Buscador de Perfis do GitHub

Aplicação web desenvolvida com **Vue 3** e **Vite** que permite pesquisar perfis do GitHub pelo nome de usuário e visualizar suas principais informações de forma simples e intuitiva.

## ✨ Funcionalidades

- 🔍 Busca de usuários pelo nome de usuário do GitHub.
- 👤 Exibição da foto de perfil e do nome do usuário.
- 📝 Visualização da biografia, quando disponível.
- 👥 Exibição da quantidade de seguidores.
- 📂 Exibição da quantidade de repositórios públicos.
- ⚠️ Tratamento de erros para usuários não encontrados.
- ⏳ Indicador de carregamento durante a busca.
- 📱 Interface adaptável a diferentes tamanhos de tela.

## 🛠️ Tecnologias utilizadas

- **Vue 3** — construção da interface com componentes reativos.
- **JavaScript** — lógica e funcionalidades da aplicação.
- **HTML5** — estrutura da página.
- **CSS3** — estilização e layout responsivo.
- **Vite** — ferramenta de desenvolvimento e build.
- **GitHub REST API** — consulta dos dados públicos dos usuários.

## 🚀 Como executar o projeto

### Pré-requisitos

- [Node.js](https://nodejs.org/)
- [Git](https://git-scm.com/)
- Um editor de código, como o [Visual Studio Code](https://code.visualstudio.com/)

### 1. Clone o repositório

```bash
git clone https://github.com/andradebjl24-cmyk/Buscador-de-perfis-do-GitHub.git
```

### 2. Acesse a pasta do projeto

```bash
cd Buscador-de-perfis-do-GitHub
```

### 3. Instale as dependências

```bash
npm install
```

### 4. Inicie o servidor de desenvolvimento

```bash
npm run dev
```

Depois, acesse o endereço local exibido no terminal para utilizar a aplicação.

### 5. Gere a versão de produção

```bash
npm run build
```

## 📡 API utilizada

O projeto utiliza a API pública do GitHub para consultar informações dos perfis.

Exemplo de consulta:

```text
https://api.github.com/users/USERNAME
```

Substitua `USERNAME` pelo nome de usuário que deseja pesquisar.

## 🎯 Objetivo do projeto

Este projeto foi desenvolvido para praticar conceitos de desenvolvimento front-end, incluindo reatividade com Vue 3, manipulação de dados, consumo de API, tratamento de erros e criação de interfaces com CSS.

## 👩‍💻 Desenvolvido por

**Letícia Andrade**

[GitHub](https://github.com/andradebjl24-cmyk)

---

Feito com Vue 3 💜
