# FastAPI
### Quem é o FastAPi?
Framework FastAPI, alta performance, fácil de aprender, fácil de codar, pronto para produção.
FastAPI é um moderno e rápido (alta performance) framework web para construção de APIs com Python 3.6 ou superior, baseado nos type hints padrões do Python.

### Async
Código assíncrono apenas significa que a linguagem tem um jeito de dizer para o computador / programa que em certo ponto, ele terá que esperar por algo para finalizar em outro lugar

# Projeto
## WorkoutAPI

Esta é uma API de competição de crossfit chamada WorkoutAPI (isso mesmo rs, eu acabei unificando duas coisas que gosto: codar e treinar). É uma API pequena, devido a ser um projeto mais hands-on e simplificado nós desenvolveremos uma API de poucas tabelas, mas com o necessário para você aprender como utilizar o FastAPI.

## Modelagem de entidade e relacionamento - MER
![MER](/mer.jpg "Modelagem de entidade e relacionamento")

## Stack da API

A API foi desenvolvida utilizando o `fastapi` (async), junto das seguintes libs: `alembic`, `SQLAlchemy`, `pydantic`. Para salvar os dados está sendo utilizando o `postgres`, por meio do `docker`.

## Execução da API

Para executar o projeto, utilizei a [pyenv](https://github.com/pyenv/pyenv), com a versão 3.11.4 do `python` para o ambiente virtual.

Caso opte por usar pyenv, após instalar, execute:

```bash
pyenv virtualenv 3.11.4 workoutapi
pyenv activate workoutapi
pip install -r requirements.txt
```
Para subir o banco de dados, caso não tenha o [docker-compose](https://docs.docker.com/compose/install/linux/) instalado, faça a instalação e logo em seguida, execute:

```bash
make run-docker
```
Para criar uma migration nova, execute:

```bash
make create-migrations d="nome_da_migration"
```

Para criar o banco de dados, execute:

```bash
make run-migrations
```

## API

Para subir a API, execute:
```bash
make run
```
e acesse: http://127.0.0.1:8000/docs

# Desafio Final
    - adicionar query parameters nos endpoints
        - atleta
            - nome
            - cpf
    - customizar response de retorno de endpoints
        - get all
            - atleta
                - nome
                - centro_treinamento
                - categoria
    - Manipular exceção de integridade dos dados em cada módulo/tabela
        - sqlalchemy.exc.IntegrityError e devolver a seguinte mensagem: “Já existe um atleta cadastrado com o cpf: x”
        - status_code: 303
    - Adicionar paginação utilizando a lib: fastapi-pagination
        - limit e offset

# Futuras implementações

1. Ranking de Atletas

    Funcionalidade: Gerar um ranking dos atletas baseado em performances registradas (pontuação, tempo, etc).
    Como implementar: Adicionar uma tabela/modelo para “Resultados” ou “Performances” e criar endpoints para consulta de rankings por categoria, centro de treinamento, ou geral.

2. Gestão de Competição/Eventos

    Funcionalidade: Permitir o cadastro de eventos/competições (WODs, campeonatos, etc), vinculando atletas e resultados.
    Como implementar: Criar modelos para “Evento” e “Resultado”, relacionando com atletas e categorias. Permitir cadastro, edição, e consulta desses eventos.

3. Autenticação e Autorização

    Funcionalidade: Adicionar login/logout para usuários (admin, coach, atleta), com permissões diferenciadas.
    Como implementar: Integrar OAuth2/JWT ao FastAPI, criar rotas protegidas e papéis de usuário.

4. Histórico e Evolução do Atleta

    Funcionalidade: Registrar histórico de treinos, resultados e evolução dos atletas.
    Como implementar: Criar endpoints que permitam consultar, adicionar e atualizar registros históricos, apresentando gráficos ou relatórios.

5. Upload de Fotos/Documentos

    Funcionalidade: Permitir que atletas ou centros de treinamento adicionem fotos de perfil, comprovantes, etc.
    Como implementar: Usar FastAPI para upload de arquivos, armazenando em disco ou em cloud storage (S3, etc).

6. Notificações por Email ou Push

    Funcionalidade: Enviar notificações sobre novos eventos, resultados, ou mudanças de status do atleta.
    Como implementar: Integrar um sistema de envio de emails (SMTP) ou push notifications para dispositivos.

7. Filtros Avançados e Relatórios

    Funcionalidade: Permitir consultas avançadas com múltiplos filtros (idade, sexo, categoria, centro, data de evento, etc), e exportação de relatórios em PDF ou CSV.

8. Dashboard Estatístico

    Funcionalidade: Criar endpoints que retornem estatísticas para visualização em dashboards (quantidade de atletas por categoria, evolução de resultados, etc).

9. Integração com APIs externas (ex: WODs do Crossfit.com)

    Funcionalidade: Buscar e sugerir treinos (WODs) de bases externas, integrando dados via API.

10. Sistema de Feedback/Avaliação

    Funcionalidade: Permitir que atletas avaliem eventos, centros de treinamento, ou até outros atletas.

# Referências

FastAPI: https://fastapi.tiangolo.com/

Pydantic: https://docs.pydantic.dev/latest/

SQLAlchemy: https://docs.sqlalchemy.org/en/20/

Alembic: https://alembic.sqlalchemy.org/en/latest/

Fastapi-pagination: https://uriyyo-fastapi-pagination.netlify.app/
