# Sistema Academia PRO 2.0

Aplicação desktop em Python (PySide6) para gestão de academia: membros, instrutores, treinos, planos, pagamentos e portal do aluno.

## Executar

```bash
python main.py
```

No Windows, se o venv não ativar por política do PowerShell:

```powershell
.\.venv\Scripts\python.exe main.py
```

## Login

| Usuário     | Senha | Permissões |
|-------------|-------|------------|
| admin       | 123   | Tudo (planos, remover catálogo, backup) |
| funcionario | 123   | Membros, instrutores, treinos, pagamentos |
| aluno       | CPF + data de nascimento | Portal do aluno |

## Estrutura do projeto

```
main.py                 # Ponto de entrada
models/                 # Entidades (Pessoa, Aluno, Plano, Pagamento, Usuario...)
core/                   # Regras de negócio, validação, decoradores
  repositorio/            # Persistência SQLite por entidade
  pagamentos/             # Geração, inadimplência e operações financeiras
  servico_*.py            # Fachadas de serviço
ui/                     # Interface PySide6
  app.py                # Tela de login
  dashboard.py          # Menu e navegação
  portal.py             # Área do aluno
  pages/                # Telas: início, membros, instrutores, treinos, planos, pagamentos
  widgets.py, dialogs.py, theme.py
database/
  academia.db           # Banco SQLite
  academia.json         # Dados iniciais (migração única se DB vazio)
  operacoes.log         # Log de operações
tests/                  # Testes automatizados (unittest)
```

## Funcionalidades

- **Dashboard:** indicadores, financeiro, alertas clicáveis, backup (admin/funcionário)
- **Membros:** CRUD, plano, instrutor, mensalidades, exportar CSV/PDF de treinos
- **Instrutores:** CRUD e vínculo com membros
- **Treinos:** catálogo, vincular/editar/remover
- **Planos (admin):** CRUD; remoção limpa vínculos e boletos
- **Pagamentos:** pastas por membro, marcar pago, gerar mensalidades, registrar cobrança
- **Portal aluno:** dados, treinos e financeiro

## Testes

```bash
python -m unittest discover -s tests -v
```

27 testes cobrem validação, serviços, pagamentos, treinos, planos e dashboard.

## Dependências

```bash
pip install -r requirements.txt
```
