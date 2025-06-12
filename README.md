---
![download](https://github.com/user-attachments/assets/50720f5f-61f0-42db-9b7f-d2198c0df903)
---
#  Plataforma de Treinamento de Dev

---

## Visão Geral

Plataforma de treinamento para desenvolvedores com backend em Flask + PostgreSQL, dashboard administrativo e interface do usuário em Streamlit. Sistema de recompensas implementado via blockchain local simulada (Ganache) usando token ERC20 para premiar usuários pela conclusão de conteúdos.

---

## Tecnologias Usadas

* Python 3.9+
* Flask (API backend)
* PostgreSQL (Banco de dados)
* SQLAlchemy (ORM)
* Streamlit (Dashboard e interface do aluno)
* Web3.py (Interação com blockchain)
* Ganache (Blockchain local Ethereum simulada)
* Solidity (Contrato ERC20 token)

---

## Setup Backend Flask + PostgreSQL

### Instalar dependências

```bash
pip install flask flask_sqlalchemy flask_cors psycopg2-binary web3
```

### Configurar banco

* Instalar e configurar PostgreSQL local
* Criar database `dev_training`
* Ajustar URI no app Flask (`postgresql://usuario:senha@localhost/dev_training`)

### Modelos e rotas principais

* Modelos: `Usuario`, `Conteudo`, `Recompensa`, `Progresso`
* Rotas:

  * `/conteudos` \[GET, POST] — listar e adicionar conteúdos programáticos
  * `/usuario` \[GET] — buscar dados do usuário por email
  * `/saldo` \[GET] — consultar saldo de token da carteira blockchain
  * `/historico` \[GET] — histórico de recompensas do usuário
  * `/concluir` \[POST] — marcar conteúdo como concluído e emitir recompensa

---

## Setup Blockchain Local com Ganache

1. Baixar e instalar [Ganache](https://trufflesuite.com/ganache/)
2. Rodar Ganache para criar blockchain local Ethereum simulada
3. Compilar e implantar contrato ERC20 token (exemplo padrão OpenZeppelin)
4. Anotar endereço do contrato e ABI
5. Configurar Web3.py no Flask para se conectar a Ganache (`http://127.0.0.1:8545`)
6. Usar conta Ganache como carteira admin para emitir tokens

---

## Contrato Inteligente ERC20

```solidity
// SPDX-License-Identifier: MIT
pragma solidity ^0.8.0;

import "@openzeppelin/contracts/token/ERC20/ERC20.sol";

contract DevRewardToken is ERC20 {
    constructor() ERC20("DevRewardToken", "DVR") {
        _mint(msg.sender, 1000000 * 10 ** decimals());
    }
}
```

Compile e implante no Ganache.

---

## Dashboard Administrativo (Streamlit)

Arquivo: `dashboard.py`

* Interface para adicionar novos conteúdos programáticos
* Listagem dos conteúdos já cadastrados

---

## Interface do Usuário (Streamlit)

Arquivo: `usuario.py`

* Exibe lista de conteúdos com descrição
* Campo para o usuário informar o e-mail
* Botão para marcar conteúdo como concluído
* Consulta do saldo e histórico de recompensas
* Integração com backend Flask para envio de recompensas

---

## Como Rodar Localmente

1. Inicie Ganache (blockchain local)
2. Configure e rode o backend Flask:

   ```bash
   export FLASK_APP=app.py
   flask run
   ```
3. Inicie o dashboard administrativo:

   ```bash
   streamlit run dashboard.py
   ```
4. Inicie a interface do aluno:

   ```bash
   streamlit run usuario.py
   ```
5. Use a interface para cadastrar conteúdos, alunos para concluir e receber recompensas.

---

## Notas Finais

* A assinatura das transações blockchain para transferir tokens está simulada e deve ser implementada com segurança para uso real (ex: usando chaves privadas seguras).
* IDs de conteúdo assumidos sequenciais para simplicidade; podem ser adaptados.
* É possível expandir para autenticação real, front-end mais elaborado e blockchain pública.

---

Se quiser, posso gerar todos esses arquivos `.md` para o seu repositório GitHub de uma vez só. Quer que eu faça isso?
