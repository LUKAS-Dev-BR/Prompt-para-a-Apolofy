Você é um engenheiro de software sênior, arquiteto de APIs, especialista em TypeScript/Node.js, bancos de dados, sistemas de scraping/crawling, agregação de providers, sistemas de metadata e arquiteturas de APIs multimídia.

Sua tarefa é criar a Apolofy.

==================================================
1. OBJETIVO PRINCIPAL
==================================================

Crie uma API chamada:

Apolofy

A apolofy será um fork/derivative project baseado no repositório oficial do Anify:

Eltik/Anify

O repositório oficial do Anify deve ser utilizado como arquitetura principal/base do projeto.

IMPORTANTE:

NÃO recrie do zero aquilo que já existe no Anify.

Primeiro clone/fork o repositório oficial do Anify e analise profundamente:

- estrutura de diretórios
- backend
- frontend, se necessário
- providers
- mappings
- crawlers
- scrapers
- database
- cache
- rotas
- models
- services
- configurações
- sistema de episódios
- sistema de anime
- sistema de mangá
- sistema de light novels
- sistema de sources
- sistema de metadata

Depois faça uma extensão arquitetural do projeto para transformá-lo na apolofy.

A regra principal é:

ANIFY CORE
+
APOLOFY EXTENSIONS
=
apolofy

==================================================
2. PRESERVAR FUNCIONALIDADES DO ANIFY
==================================================

NÃO remova as funcionalidades existentes do Anify.

A Apolofy deve continuar suportando:

- Anime
- Mangá
- Light Novels
- Anime metadata
- Mangá metadata
- Light Novel metadata
- Anime mappings
- Mangá mappings
- Light Novel mappings
- Providers
- Crawlers
- Scrapers
- Database
- Cache
- Search
- Recent
- Schedule
- Info
- Sources
- Sistema de episódios
- Sistema de capítulos
- Sistemas internos de mapping

Preserve a compatibilidade existente sempre que tecnicamente possível.

Se alguma alteração for necessária, crie uma camada de compatibilidade em vez de simplesmente quebrar os endpoints existentes.

==================================================
3. NOVOS TIPOS DE CONTEÚDO
==================================================

A grande expansão da Apolofy será adicionar suporte completo para:

1. Movies
2. TV Series
3. Seasons
4. Episodes
5. Movie Collections
6. Franchises
7. Movie/TV metadata
8. Movie/TV mappings
9. Movie/TV providers
10. Movie/TV sources
11. Movie/TV search

A Apolofy deverá funcionar como um catálogo multimídia unificado.

==================================================
4. ARQUITETURA
==================================================

Utilize uma arquitetura modular.

Estrutura conceitual:

apolofy/
│
├── core/
│   ├── anime/
│   ├── manga/
│   ├── light-novel/
│   ├── mappings/
│   ├── providers/
│   ├── crawlers/
│   ├── scrapers/
│   ├── metadata/
│   ├── database/
│   └── cache/
│
├── movies/
│   ├── controllers/
│   ├── services/
│   ├── models/
│   ├── providers/
│   ├── mappings/
│   ├── metadata/
│   └── sources/
│
├── tv/
│   ├── controllers/
│   ├── services/
│   ├── models/
│   ├── seasons/
│   ├── episodes/
│   ├── providers/
│   ├── mappings/
│   ├── metadata/
│   └── sources/
│
├── search/
├── sources/
├── providers/
├── mappings/
├── metadata/
├── database/
├── cache/
├── api/
├── config/
├── tests/
└── docs/

ADAPTE essa estrutura à arquitetura real existente no Anify.

Não destrua a organização original sem necessidade.

==================================================
5. CATÁLOGO DE ANIME
==================================================

Preserve o sistema de anime existente.

A Apolofy deve continuar podendo:

- pesquisar anime
- obter informações de anime
- obter temporadas
- obter episódios
- obter metadata
- obter mappings
- localizar providers
- localizar sources autorizadas
- consultar episódios
- consultar informações de lançamento

A estrutura deve permitir:

Anime
 ├── Season 1
 │   ├── Episode 1
 │   ├── Episode 2
 │   └── ...
 ├── Season 2
 └── ...

Também suporte:

- especiais
- OVAs
- ONAs
- filmes relacionados
- episódios especiais

==================================================
6. CATÁLOGO DE MANGÁ
==================================================

Preserve completamente o sistema de mangá existente.

Suporte:

- pesquisa
- metadata
- capítulos
- mappings
- providers
- fontes permitidas
- autores
- artistas
- gêneros
- tags
- status
- datas
- volumes

==================================================
7. LIGHT NOVELS
==================================================

Preserve o sistema existente de Light Novels.

Suporte:

- pesquisa
- metadata
- mappings
- volumes
- capítulos quando disponíveis
- autores
- ilustradores
- gêneros
- tags
- status

==================================================
8. MOVIES
==================================================

Adicione suporte completo para filmes.

Endpoints conceituais:

GET /movie/:id

GET /movie/:id/sources

GET /movie/:id/providers

GET /movie/:id/recommendations

GET /movie/:id/similar

GET /movie/:id/collection

GET /movie/:id/metadata

GET /movie/:id/mappings

A informação de um filme deve poder incluir:

- id
- título
- título original
- títulos alternativos
- sinopse
- gêneros
- tags
- ano
- data de lançamento
- duração
- classificação
- idioma
- países
- elenco
- diretores
- roteiristas
- produtores
- estúdios
- pôster
- backdrop
- imagens
- trailers
- vídeos promocionais
- avaliações
- popularidade
- IDs externos
- providers
- sources autorizadas
- coleção
- franquia
- filmes relacionados

==================================================
9. TV SERIES
==================================================

Adicione suporte completo para séries de televisão.

Endpoints:

GET /tv/:id

GET /tv/:id/seasons

GET /tv/:id/season/:season

GET /tv/:id/season/:season/episodes

GET /tv/:id/episode/:episode

GET /tv/:id/episode/:episode/sources

GET /tv/:id/providers

GET /tv/:id/metadata

GET /tv/:id/mappings

Uma série deverá possuir:

- metadata
- temporadas
- episódios
- especiais
- providers
- mappings
- sources autorizadas

==================================================
10. TEMPORADAS
==================================================

A Apolofy deve coletar/catalogar todas as temporadas disponíveis para uma série ou anime.

Exemplo:

TV Series
 ├── Season 1
 ├── Season 2
 ├── Season 3
 ├── Season 4
 └── ...

Anime
 ├── Season 1
 ├── Season 2
 ├── Season 3
 └── ...

Cada temporada deve possuir:

- id
- número
- nome
- descrição
- data de estreia
- data de encerramento
- poster
- backdrop
- número de episódios
- episódios
- metadata
- IDs externos

==================================================
11. EPISÓDIOS
==================================================

A Apolofy deve catalogar todos os episódios disponíveis de cada temporada.

Exemplo:

Season 1
 ├── Episode 1
 ├── Episode 2
 ├── Episode 3
 ├── Episode 4
 └── ...

Cada episódio poderá possuir:

- id
- número
- título
- título original
- descrição
- duração
- data de lançamento
- imagem
- thumbnail
- temporada
- série
- anime
- IDs externos
- providers
- sources autorizadas

Endpoint:

GET /tv/:id/season/:season/episode/:episode

e equivalente para anime:

GET /anime/:id/season/:season/episode/:episode

==================================================
12. FILMES E FRANQUIAS
==================================================

Filmes não devem ser tratados como temporadas.

Utilize:

Movie
 └── Collection
      ├── Movie 1
      ├── Movie 2
      ├── Movie 3
      └── Movie 4

Endpoints:

GET /movie/:id/collection

GET /collection/:id

GET /collection/:id/movies

Suporte também a:

- franquias
- sequências
- prequels
- spin-offs
- filmes relacionados

==================================================
13. SEARCH
==================================================

Crie um sistema de pesquisa unificado.

Endpoints:

GET /search

GET /search/advanced

GET /search/anime

GET /search/manga

GET /search/light-novel

GET /search/movie

GET /search/tv

Pesquisa básica:

GET /search?query=...

Parâmetros:

- query
- page
- perPage
- type
- year
- genre
- genres
- tags
- language
- country
- sort
- order

O sistema deverá permitir busca:

- global
- por tipo
- avançada
- filtrada
- paginada

==================================================
14. SISTEMA DE MAPPINGS
==================================================

Crie/expanda o Mapping Engine.

Ele deve relacionar uma obra da Apolofy com IDs externos e IDs dos providers.

Exemplo:

{
  "apolofyId": "movie-123",
  "externalIds": {
    "tmdb": "123",
    "imdb": "tt1234567",
    "tvdb": "12345"
  }
}

Para anime, preserve os mappings existentes.

Para filmes e séries, adicione mappings compatíveis com fontes/metadados que possam ser usados legalmente.

O sistema deve evitar duplicação de obras.

==================================================
15. PROVIDER SYSTEM
==================================================

Crie uma arquitetura modular de providers.

Exemplo:

ProviderManager
│
├── Anime Providers
├── Manga Providers
├── Light Novel Providers
├── Movie Providers
└── TV Providers

Cada provider deve implementar uma interface comum.

Exemplo conceitual:

interface Provider {
    search()
    getInfo()
    getMetadata()
    getEpisodes()
    getSources()
}

Adapte a interface à implementação real do Anify.

Providers devem ser plugáveis.

Um provider com erro não deve derrubar toda a API.

Implemente:

- timeout
- retry
- circuit breaker quando apropriado
- health status
- logging
- rate limiting
- cache

==================================================
16. SOURCE SYSTEM
==================================================

Crie um SourceResolver unificado.

Arquitetura:

SourceResolver
│
├── Anime
├── Movie
└── TV

O sistema deve poder retornar fontes de reprodução SOMENTE quando forem legalmente acessíveis/autorizadas.

Exemplo:

GET /anime/{id}/episode/{episode}/sources

GET /movie/{id}/sources

GET /tv/{id}/season/{season}/episode/{episode}/sources

Formato conceitual:

{
  "sources": [
    {
      "provider": "provider-a",
      "type": "hls",
      "url": "...",
      "quality": "1080p",
      "language": "pt-BR",
      "subtitles": [],
      "isAuthorized": true
    }
  ]
}

NÃO implemente:

- bypass de DRM
- quebra de paywall
- contorno de autenticação
- evasão de controles de acesso
- obtenção ilícita de conteúdo protegido

==================================================
17. METADATA ENGINE
==================================================

Crie um Metadata Engine unificado.

Tipos:

- AnimeMetadata
- MangaMetadata
- LightNovelMetadata
- MovieMetadata
- TVMetadata
- SeasonMetadata
- EpisodeMetadata

O sistema deve normalizar dados vindos de diferentes providers.

Evite que cada provider tenha um formato incompatível.

Crie modelos internos normalizados.

==================================================
18. DATABASE
==================================================

Crie/expanda o banco mantendo compatibilidade com o projeto original.

Estrutura lógica mínima:

anime
anime_episodes

manga
manga_chapters

light_novels
light_novel_volumes

movies
movie_collections

tv_series
tv_seasons
tv_episodes

mappings
providers
sources
metadata
cache

Adicione:

- índices
- foreign keys
- constraints
- unique constraints
- migrations
- timestamps
- soft delete quando apropriado

Evite duplicação de dados.

==================================================
19. CACHE
==================================================

Implemente cache para:

- search
- metadata
- mappings
- provider responses
- schedules
- recent releases
- episode information

Utilize o sistema de cache existente do Anify quando apropriado.

Não duplique sistemas desnecessariamente.

==================================================
20. SCHEDULE
==================================================

Preserve:

GET /schedule

Expanda para suportar, quando os dados estiverem disponíveis:

- anime
- TV series
- episódios
- datas de lançamento

==================================================
21. RECENT
==================================================

Preserve:

GET /recent

Permita categorias:

- anime
- tv
- movies
- manga
- light-novel

Exemplo:

GET /recent?type=anime

GET /recent?type=tv

GET /recent?type=movie

==================================================
22. API VERSIONING
==================================================

Não quebre os endpoints existentes sem necessidade.

Utilize versionamento.

Exemplo:

/api/v1/...

/api/v2/...

A versão v1 deve priorizar compatibilidade.

A v2 pode oferecer a arquitetura unificada da Apolofy.

==================================================
23. DOCUMENTAÇÃO
==================================================

Crie documentação completa.

Inclua:

README.md

ARCHITECTURE.md

API.md

PROVIDERS.md

MAPPINGS.md

METADATA.md

DATABASE.md

SOURCES.md

DEVELOPMENT.md

CONTRIBUTING.md

LICENSE.md

Documente:

- instalação
- configuração
- variáveis de ambiente
- banco
- Redis/cache
- providers
- endpoints
- autenticação, se houver
- desenvolvimento
- testes
- deploy
- Docker
- produção

Utilize OpenAPI/Swagger para documentar os endpoints.

==================================================
24. TESTES
==================================================

Crie testes:

- unitários
- integração
- API
- database
- mappings
- metadata
- providers
- search
- seasons
- episodes
- movies
- TV

Crie testes de regressão para garantir que as funcionalidades herdadas do Anify continuem funcionando.

==================================================
25. SEGURANÇA
==================================================

Implemente:

- validação de entrada
- sanitização
- rate limiting
- CORS configurável
- headers de segurança
- proteção contra abuso
- timeout
- limites de payload
- tratamento seguro de erros
- secrets via environment variables
- logs sem informações sensíveis

Nunca coloque API keys diretamente no código.

==================================================
26. OBSERVABILIDADE
==================================================

Implemente:

- logs estruturados
- request ID
- métricas
- health endpoint
- provider health
- database health
- cache health

Endpoints:

GET /health

GET /health/providers

GET /health/database

==================================================
27. PERFORMANCE
==================================================

A API deve ser preparada para grande quantidade de requisições.

Utilize:

- cache
- índices
- paginação
- connection pooling
- processamento assíncrono
- filas quando necessário
- concorrência controlada
- deduplicação de requests
- retries inteligentes

Não faça scraping de dezenas de providers simultaneamente sem limites.

==================================================
28. CRAWLING/SCRAPING
==================================================

Preserve o sistema de crawling/scraping do Anify onde apropriado.

Para novas integrações, crie adapters/providers independentes.

Todo crawler deve possuir:

- timeout
- retry
- rate limit
- identificação clara do provider
- logs
- tratamento de erros
- cache
- respeito às políticas aplicáveis
- respeito a robots.txt quando aplicável
- respeito aos termos de uso e direitos autorais

Não implemente mecanismos destinados a contornar proteções de acesso.

==================================================
29. CONFIGURAÇÃO
==================================================

Crie:

.env.example

Exemplo conceitual:

DATABASE_URL=
REDIS_URL=
API_PORT=
API_HOST=
NODE_ENV=
LOG_LEVEL=

Não coloque secrets reais.

==================================================
30. DOCKER
==================================================

Crie suporte para Docker.

Inclua:

Dockerfile

docker-compose.yml

Serviços quando necessários:

- apolofy
- PostgreSQL
- Redis

O ambiente deve permitir:

docker compose up -d

==================================================
31. CLI
==================================================

Se o projeto original possuir CLI, preserve-o.

Adicione comandos úteis quando apropriado:

apolofy dev

apolofy start

apolofy migrate

apolofy seed

apolofy provider:list

apolofy provider:health

apolofy cache:clear

==================================================
32. REGRAS DE IMPLEMENTAÇÃO
==================================================

NÃO entregue apenas exemplos ou pseudocódigo.

Você deve trabalhar no código real do projeto.

Primeiro:

1. clone/fork o Anify;
2. examine sua arquitetura;
3. identifique os módulos existentes;
4. execute o projeto;
5. execute os testes existentes;
6. documente o estado inicial;
7. somente depois comece as alterações.

Não substitua módulos funcionais por mocks.

Não crie endpoints falsos que retornem dados inventados.

Se determinada funcionalidade não puder ser implementada por falta de um provider legítimo ou de uma fonte de dados, implemente a interface/arquitetura necessária e documente claramente o que falta.

==================================================
33. COMPATIBILIDADE
==================================================

Preserve o máximo possível:

- endpoints
- schemas
- providers
- mappings
- database
- configurações
- testes

Ao adicionar funcionalidades, prefira extensão sobre substituição.

==================================================
34. NOME E IDENTIDADE
==================================================

O nome do novo projeto é:

apolofy

Não chame o projeto de Anify depois da transformação, exceto quando estiver se referindo ao projeto original/base.

No README, deixe claro:

"Apolofy is a fork/derivative project based on Anify."

Mantenha as atribuições e obrigações da licença do projeto original.

Não remova créditos obrigatórios.

==================================================
35. ESTRUTURA FINAL ESPERADA
==================================================

A arquitetura final deverá conceitualmente possuir:

Apolofy
│
├── Anime
│   ├── Seasons
│   ├── Episodes
│   ├── Metadata
│   ├── Providers
│   ├── Mappings
│   └── Sources
│
├── Manga
│   ├── Chapters
│   ├── Metadata
│   ├── Providers
│   └── Mappings
│
├── Light Novels
│   ├── Volumes
│   ├── Metadata
│   ├── Providers
│   └── Mappings
│
├── Movies
│   ├── Metadata
│   ├── Collections
│   ├── Franchises
│   ├── Providers
│   ├── Mappings
│   └── Sources
│
├── TV Series
│   ├── Seasons
│   ├── Episodes
│   ├── Metadata
│   ├── Providers
│   ├── Mappings
│   └── Sources
│
├── Search
├── Metadata Engine
├── Mapping Engine
├── Provider Manager
├── Source Resolver
├── Crawler Engine
├── Scraper Engine
├── Database
├── Cache
├── API
├── CLI
├── Docker
└── Documentation

==================================================
36. RESULTADO FINAL
==================================================

O resultado final deve ser uma API funcional chamada:

Apolofy

Ela deve combinar:

ANIFY
+
MOVIES
+
TV SERIES
+
SEASONS
+
EPISODES
+
METADATA
+
MAPPINGS
+
PROVIDERS
+
SEARCH
+
SOURCES AUTORIZADAS
+
DATABASE
+
CACHE

O sistema deve ser modular, escalável, testável, documentado e preparado para produção.

==================================================
37. ORDEM DE EXECUÇÃO
==================================================

Execute o trabalho nesta ordem:

FASE 1
Clonar/forkar o Anify.

FASE 2
Auditar a arquitetura existente.

FASE 3
Executar e validar o projeto original.

FASE 4
Criar branch:

feature/apolofy

FASE 5
Criar arquitetura de Movies.

FASE 6
Criar arquitetura de TV Series.

FASE 7
Criar Seasons.

FASE 8
Criar Episodes.

FASE 9
Criar Movie Collections/Franchises.

FASE 10
Expandir Metadata Engine.

FASE 11
Expandir Mapping Engine.

FASE 12
Expandir Provider Manager.

FASE 13
Expandir SourceResolver com fontes autorizadas.

FASE 14
Expandir Search.

FASE 15
Expandir Database.

FASE 16
Implementar Cache.

FASE 17
Implementar testes.

FASE 18
Implementar Docker.

FASE 19
Implementar documentação.

FASE 20
Executar todos os testes.

FASE 21
Corrigir todos os erros.

FASE 22
Executar build de produção.

FASE 23
Validar todos os endpoints.

FASE 24
Gerar relatório final.

==================================================
38. RELATÓRIO FINAL OBRIGATÓRIO
==================================================

Ao terminar, informe:

1. O que foi herdado do Anify.
2. O que foi adicionado pela Apolofy.
3. Estrutura final do projeto.
4. Todos os endpoints.
5. Banco de dados.
6. Providers implementados.
7. Providers que ainda precisam ser implementados.
8. Sistema de mappings.
9. Sistema de metadata.
10. Sistema de seasons.
11. Sistema de episodes.
12. Sistema de movies.
13. Sistema de TV.
14. Sistema de sources.
15. Sistema de cache.
16. Testes executados.
17. Resultado do build.
18. Como executar localmente.
19. Como executar com Docker.
20. Variáveis de ambiente.
21. Limitações conhecidas.
22. Próximos passos.

NÃO pare depois de criar apenas a estrutura.

Implemente o máximo possível no código real, valide tudo e só então apresente o relatório final.

COMECE AGORA.