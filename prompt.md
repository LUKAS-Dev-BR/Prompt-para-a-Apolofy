Você é uma IA/LLM especializada em engenharia de software, arquitetura de APIs, TypeScript, Node.js/Bun, scraping/crawling, sistemas de metadata, media catalogs, providers, mappings, bancos de dados, players de vídeo web e integração de APIs com sites de terceiros.

Sua missão é transformar o projeto Anify que JÁ ESTÁ CLONADO NO DIRETÓRIO ATUAL em uma nova API chamada:

APOLOFY API

============================================================
1. REGRA ABSOLUTA: USE O DIRETÓRIO ATUAL
============================================================

NÃO clone o Anify novamente.

NÃO crie outro projeto em uma pasta diferente.

O repositório oficial do Anify já está configurado/clonado no diretório atual.

Primeiro execute comandos equivalentes a:

pwd
ls -la
find . -maxdepth 2 -type f
git status
git remote -v

Identifique exatamente onde está o repositório Anify.

Depois trabalhe diretamente nesse projeto.

Antes de modificar qualquer código:

1. examine a estrutura;
2. examine o git status;
3. examine package.json;
4. examine os README.md;
5. examine anify-backend;
6. examine anify-backend/src;
7. examine os providers;
8. examine os mappings;
9. examine os crawlers;
10. examine os scrapers;
11. examine as rotas;
12. examine o sistema de episódios;
13. examine o sistema de sources;
14. examine o sistema de metadata;
15. examine o banco de dados;
16. examine o Redis/cache;
17. examine os scripts Bun;
18. execute o projeto quando possível;
19. execute os testes/lint/build existentes.

NÃO faça alterações grandes antes de entender a arquitetura existente.

============================================================
2. OBJETIVO DA APOLOFY
============================================================

Transforme:

ANIFY
+
EXTENSÕES APOLOFY
=
APOLOFY API

A Apolofy deve preservar as funcionalidades existentes do Anify e adicionar suporte para:

- Anime
- Mangá
- Light Novel
- Filmes
- Séries de TV
- Temporadas
- Episódios
- Filmes relacionados
- Coleções
- Franquias
- Metadata
- Capas
- Banners
- Classificações etárias
- Mappings
- Providers
- Sources autorizadas
- Search
- Schedule
- Recent
- Player de vídeo
- Player de vídeo incorporável
- API para integração com sites externos

============================================================
3. NÃO REMOVER O SISTEMA DE ANIME
============================================================

IMPORTANTE:

NÃO remova a coleta existente de anime do Anify.

NÃO substitua os providers existentes sem necessidade.

NÃO remova o sistema de episódios existente.

NÃO remova mappings existentes.

NÃO remova metadata existente.

NÃO remova o sistema de sources existente.

A Apolofy deve preservar e expandir a funcionalidade existente.

============================================================
4. ESTUDAR O ANIFY ANTES DE IMPLEMENTAR SOURCES
============================================================

Antes de implementar o sistema de fontes da Apolofy, faça uma auditoria específica do código real do Anify.

Estude:

- providers;
- base providers;
- mapping providers;
- episode providers;
- source resolvers;
- rotas relacionadas a mídia;
- rotas relacionadas a episódios;
- metadata providers;
- crawlers;
- filas;
- cache;
- banco de dados;
- processamento de URLs;
- subtitles;
- formatos de vídeo;
- HLS;
- DASH, quando existente;
- tratamento de erros;
- fallback entre providers.

O Anify explica oficialmente que o backend utiliza mappings próprios, obtém informações dos providers e armazena os mappings no banco de dados. Também possui crawling e criação de mappings durante buscas e carregamento sazonal.

Use essa arquitetura como referência.

NÃO copie mecanismos destinados a:

- contornar DRM;
- quebrar paywalls;
- roubar credenciais;
- contornar autenticação;
- burlar controles de acesso;
- evadir proteções de provedores.

Para a Apolofy, implemente resolução de sources apenas para fontes que possam ser acessadas legalmente/autorizadamente.

============================================================
5. SISTEMA DE PROVIDERS
============================================================

Crie uma arquitetura unificada:

ProviderManager

    ├── Anime Providers
    ├── Manga Providers
    ├── Light Novel Providers
    ├── Movie Providers
    └── TV Providers

Cada provider deve possuir uma interface consistente.

Conceitualmente:

Provider
    ├── search()
    ├── getInfo()
    ├── getMetadata()
    ├── getSeasons()
    ├── getEpisodes()
    ├── getSources()
    └── getArtwork()

Adapte isso à arquitetura REAL do Anify.

NÃO invente uma arquitetura paralela se o Anify já possuir abstrações equivalentes.

============================================================
6. FILMES
============================================================

Adicionar suporte completo para filmes.

Endpoints:

GET /movie/:id

GET /movie/:id/metadata

GET /movie/:id/mappings

GET /movie/:id/providers

GET /movie/:id/sources

GET /movie/:id/recommendations

GET /movie/:id/similar

GET /movie/:id/collection

GET /movie/:id/artwork

Os dados devem incluir, quando disponíveis:

- ID;
- título;
- título original;
- títulos alternativos;
- sinopse;
- gêneros;
- tags;
- ano;
- data de lançamento;
- duração;
- idioma;
- países;
- classificação etária;
- elenco;
- diretores;
- roteiristas;
- produtores;
- estúdios;
- avaliações;
- popularidade;
- poster/capa;
- backdrop/banner;
- imagens adicionais;
- trailers;
- IDs externos;
- collection;
- franchise;
- providers;
- sources autorizadas.

============================================================
7. SÉRIES DE TV
============================================================

Adicionar suporte completo para séries.

Endpoints:

GET /tv/:id

GET /tv/:id/metadata

GET /tv/:id/mappings

GET /tv/:id/providers

GET /tv/:id/seasons

GET /tv/:id/artwork

GET /tv/:id/age-rating

A estrutura deve ser:

TV Series
    ├── Season 1
    │   ├── Episode 1
    │   ├── Episode 2
    │   ├── Episode 3
    │   └── ...
    ├── Season 2
    │   ├── Episode 1
    │   └── ...
    └── Season N

============================================================
8. TODAS AS TEMPORADAS
============================================================

A Apolofy deve possuir uma arquitetura capaz de catalogar todas as temporadas disponíveis de cada série.

Endpoint:

GET /tv/:id/seasons

Cada temporada deve possuir:

- ID;
- número;
- nome;
- descrição;
- poster;
- banner/backdrop;
- data de início;
- data final;
- quantidade de episódios;
- metadata;
- IDs externos.

============================================================
9. TODOS OS EPISÓDIOS
============================================================

Para cada temporada, catalogue os episódios disponíveis.

Endpoint:

GET /tv/:id/season/:season

ou:

GET /tv/:id/season/:season/episodes

Endpoint individual:

GET /tv/:id/season/:season/episode/:episode

Cada episódio deve possuir:

- ID;
- número;
- título;
- título original;
- descrição;
- duração;
- data de lançamento;
- thumbnail;
- imagens;
- classificação etária, quando disponível;
- temporada;
- série;
- IDs externos;
- providers;
- sources autorizadas.

============================================================
10. ANIME — TEMPORADAS E EPISÓDIOS
============================================================

NÃO remova o sistema existente do Anify.

Expanda-o para que a Apolofy consiga catalogar:

Anime
    ├── Season 1
    │   ├── Episode 1
    │   ├── Episode 2
    │   └── ...
    ├── Season 2
    └── ...

Quando os dados estiverem disponíveis, catalogue:

- todas as temporadas;
- todos os episódios;
- episódios especiais;
- OVAs;
- ONAs;
- filmes relacionados;
- metadata;
- classificação etária;
- capas;
- banners;
- providers;
- sources autorizadas.

Utilize o sistema de mappings do Anify para relacionar IDs entre providers.

============================================================
11. COLEÇÃO DE LINKS/SOURCES
============================================================

A Apolofy deve possuir um sistema:

SourceResolver

com suporte conceitual para:

    Anime
    Movie
    TV

Exemplos:

GET /anime/:id/episode/:episode/sources

GET /movie/:id/sources

GET /tv/:id/season/:season/episode/:episode/sources

A arquitetura deve seguir o padrão encontrado no Anify:

1. identificar a obra;
2. identificar o provider;
3. localizar a obra/episódio;
4. resolver a fonte disponível;
5. normalizar a resposta;
6. retornar as fontes ao cliente;
7. utilizar cache apropriado;
8. aplicar timeout/retry;
9. fazer fallback para outro provider autorizado quando necessário.

NÃO implemente bypass de DRM ou mecanismos para violar controles de acesso.

============================================================
12. FORMATO UNIFICADO DE SOURCES
============================================================

Normalize as fontes em um formato comum:

{
  "sources": [
    {
      "id": "source-id",
      "provider": "provider-name",
      "type": "hls",
      "url": "https://...",
      "quality": "1080p",
      "language": "pt-BR",
      "audio": "original",
      "subtitles": [],
      "headers": {},
      "expiresAt": null
    }
  ]
}

Suporte, quando legitimamente fornecido:

- HLS;
- DASH;
- MP4;
- outros formatos suportados pelo player.

============================================================
13. CAPAS DE TODOS OS CONTEÚDOS
============================================================

A Apolofy deve coletar/normalizar artwork de:

- filmes;
- séries;
- anime.

Incluindo:

- poster;
- cover;
- thumbnail;
- backdrop;
- banner;
- logos;
- imagens promocionais, quando disponíveis.

Crie:

ArtworkService

Exemplo:

GET /movie/:id/artwork

GET /tv/:id/artwork

GET /anime/:id/artwork

O serviço deve normalizar diferentes formatos de providers.

Não duplique imagens desnecessariamente.

Utilize cache.

============================================================
14. BANNERS
============================================================

A Apolofy deve coletar banners/backdrops de:

- filmes;
- séries;
- anime.

Exemplo:

{
  "poster": "...",
  "backdrop": "...",
  "banner": "...",
  "logo": "..."
}

Quando determinado provider não possuir banner, tente outro provider de metadata autorizado.

Não invente URLs.

============================================================
15. CLASSIFICAÇÃO ETÁRIA
============================================================

A Apolofy deve coletar classificações etárias de:

- filmes;
- séries;
- anime.

Exemplos conceituais:

- Livre;
- 10;
- 12;
- 14;
- 16;
- 18;
- TV-Y;
- TV-PG;
- TV-14;
- TV-MA;
- ou equivalentes conforme o país.

Não converta classificações de forma incorreta.

Armazene:

{
  "rating": "16",
  "system": "BR",
  "country": "BR"
}

Quando houver múltiplos países:

{
  "ratings": [
    {
      "country": "BR",
      "system": "...",
      "rating": "16"
    },
    {
      "country": "US",
      "system": "...",
      "rating": "TV-14"
    }
  ]
}

============================================================
16. METADATA ENGINE
============================================================

Crie um Metadata Engine unificado.

Suporte:

AnimeMetadata
MangaMetadata
LightNovelMetadata
MovieMetadata
TVMetadata
SeasonMetadata
EpisodeMetadata

O Metadata Engine deve normalizar:

- títulos;
- sinopse;
- gêneros;
- tags;
- elenco;
- equipe;
- datas;
- duração;
- ratings;
- artwork;
- relações;
- IDs externos.

============================================================
17. MAPPING ENGINE
============================================================

Preserve o Mapping Engine do Anify.

Expanda-o para:

Anime
Movie
TV
Manga
Light Novel

Utilize IDs externos quando disponíveis.

Exemplo:

{
  "apolofyId": "movie-123",
  "externalIds": {
    "tmdb": "123",
    "imdb": "tt1234567",
    "tvdb": "12345"
  }
}

O sistema deve impedir duplicação de títulos.

============================================================
18. SEARCH
============================================================

Criar busca global:

GET /search

GET /search/advanced

GET /search/anime

GET /search/manga

GET /search/light-novel

GET /search/movie

GET /search/tv

Parâmetros:

query
page
perPage
type
year
genre
genres
tags
sort
order
language
country

A pesquisa global deve poder retornar:

Anime
Movie
TV
Manga
Light Novel

============================================================
19. PLAYER DE VÍDEO APOLOFY
============================================================

ESTA É UMA FUNCIONALIDADE PRINCIPAL.

A Apolofy deve possuir seu próprio PLAYER DE VÍDEO.

O player deve ser inspirado VISUALMENTE NA IMAGEM DE REFERÊNCIA FORNECIDA PELO USUÁRIO.

A imagem mostra um player:

- dark;
- moderno;
- minimalista;
- cinematográfico;
- responsivo;
- com painel superior;
- área de vídeo grande;
- controles inferiores;
- aparência premium.

NÃO faça apenas um elemento HTML:

<video>

Crie um componente de player completo.

============================================================
20. DESIGN DO PLAYER
============================================================

O player deve possuir visual equivalente ao layout da imagem fornecida.

Na parte superior:

[←] Nome do Filme / Série / Anime

Temporada 1 • Episódio 1

No lado direito:

[Cast]
[Settings]
[More]

Área central:

Imagem/poster/backdrop do conteúdo

Botão:

▶

No rodapé da área de vídeo:

tempo atual / duração

barra de progresso

Na barra inferior:

Pause/Play

Retroceder 10 segundos

Avançar 10 segundos

Volume

No lado direito:

HD

Seletor de qualidade:

1080p
720p
480p
360p

Botão de legendas

Fullscreen

============================================================
21. PLAYER RESPONSIVO
============================================================

O player deve funcionar em:

- Desktop;
- Notebook;
- Tablet;
- Smartphone;
- Smart TV quando possível.

No celular:

- controles devem se adaptar;
- botões devem continuar acessíveis;
- fullscreen deve funcionar;
- orientação landscape deve ser suportada;
- interface não pode ficar cortada.

============================================================
22. FUNCIONALIDADES DO PLAYER
============================================================

Implementar:

- play/pause;
- seek;
- barra de progresso;
- volume;
- mute;
- fullscreen;
- picture-in-picture quando suportado;
- seleção de qualidade;
- seleção de áudio quando disponível;
- seleção de legenda;
- sincronização de legenda;
- avanço de 10 segundos;
- retrocesso de 10 segundos;
- indicador de carregamento;
- tratamento de erro;
- retry;
- troca de source;
- troca automática de source quando configurado;
- resume playback;
- remember position;
- keyboard shortcuts no desktop;
- touch gestures no mobile quando apropriado;
- Cast quando suportado pelo navegador/dispositivo.

============================================================
23. PLAYER COMO COMPONENTE REUTILIZÁVEL
============================================================

O player NÃO deve existir somente dentro da própria Apolofy.

Ele deve ser construído como componente reutilizável.

Crie uma arquitetura:

ApolofyPlayer

e permita integração em sites externos.

O objetivo é:

Um usuário possui seu próprio site.

Ele configura a Apolofy API no site.

A Apolofy fornece os dados de filmes/séries/animes.

Quando o visitante clicar em assistir:

O site do usuário abre o ApolofyPlayer.

============================================================
24. FORMAS DE INTEGRAÇÃO
============================================================

A Apolofy deve fornecer pelo menos duas formas de integração.

FORMA 1 — IFRAME

Exemplo conceitual:

<iframe
  src="https://api.exemplo.com/player/..."
  width="100%"
  height="600"
  allow="fullscreen; picture-in-picture; autoplay"
  allowfullscreen>
</iframe>

A URL deve receber um identificador seguro da mídia/episódio e, quando necessário, uma referência de source.

FORMA 2 — COMPONENTE JAVASCRIPT/REACT

Criar um pacote:

@apolofy/player

Uso conceitual:

<ApolofyPlayer
    source="..."
    title="Nome do Filme"
    poster="..."
    season={1}
    episode={1}
/>

Adapte a implementação ao stack real do projeto.

============================================================
25. API DO PLAYER
============================================================

Crie endpoints próprios para integração.

Exemplo:

GET /player/:id

GET /player/:type/:id

GET /player/anime/:id/episode/:episode

GET /player/tv/:id/season/:season/episode/:episode

GET /player/movie/:id

Também pode existir:

GET /player/config/:id

para retornar a configuração necessária ao player.

============================================================
26. PLAYER + SOURCES
============================================================

Fluxo:

SITE DO USUÁRIO
        ↓
APOLOFY API
        ↓
IDENTIFICA MÍDIA
        ↓
IDENTIFICA EPISÓDIO
        ↓
MAPPING
        ↓
PROVIDER
        ↓
SOURCE RESOLVER
        ↓
SOURCE AUTORIZADA
        ↓
APOLOFY PLAYER
        ↓
REPRODUÇÃO

O player nunca deve precisar conhecer a lógica interna dos providers.

O player recebe uma resposta normalizada.

============================================================
27. RESPOSTA PARA O PLAYER
============================================================

Exemplo:

{
  "media": {
    "id": "123",
    "type": "tv",
    "title": "Example Series",
    "season": 1,
    "episode": 1
  },

  "artwork": {
    "poster": "...",
    "backdrop": "...",
    "banner": "..."
  },

  "rating": {
    "country": "BR",
    "rating": "14"
  },

  "sources": [
    {
      "provider": "authorized-provider",
      "type": "hls",
      "url": "...",
      "quality": "1080p",
      "language": "pt-BR"
    }
  ],

  "subtitles": [
    {
      "language": "pt-BR",
      "url": "..."
    }
  ]
}

============================================================
28. EPISÓDIO AUTOMÁTICO
============================================================

Quando estiver assistindo uma série/anime:

O player deve saber:

- série/anime;
- temporada;
- episódio atual;
- próximo episódio;
- episódio anterior.

Quando o episódio terminar, o player poderá oferecer:

"Próximo episódio"

E:

"Próximo episódio em 5... 4... 3..."

O comportamento deve ser configurável.

============================================================
29. PLAYER SEM DADOS FIXOS
============================================================

NÃO coloque:

- títulos fixos;
- posters fixos;
- URLs fixas;
- episódios fixos.

Tudo deve vir da API.

O mesmo player deve conseguir reproduzir:

Filme A

Série B
Season 3
Episode 7

Anime C
Season 2
Episode 12

sem modificar o código do player.

============================================================
30. TECNOLOGIA DO PLAYER
============================================================

Escolha uma tecnologia moderna compatível com:

- React;
- TypeScript;
- HLS;
- DASH quando necessário;
- HTML5 Video.

Pode utilizar uma biblioteca madura de player caso seja compatível com a arquitetura do projeto.

Porém:

A aparência final deve ser CUSTOMIZADA para ficar visualmente equivalente à imagem de referência.

Não entregue simplesmente o player padrão da biblioteca.

============================================================
31. BANCO DE DADOS
============================================================

Preserve o banco existente do Anify.

Expanda com entidades equivalentes a:

movies
movie_collections

tv_series
tv_seasons
tv_episodes

anime
anime_seasons
anime_episodes

manga
manga_chapters

light_novels
light_novel_volumes

mappings
providers
sources
metadata
artwork
age_ratings
cache

Adapte aos models reais existentes.

Não crie duplicações desnecessárias.

============================================================
32. CACHE
============================================================

Utilize Redis/cache para:

- metadata;
- search;
- mappings;
- seasons;
- episodes;
- artwork;
- ratings;
- provider responses;
- source responses.

Sources com URLs temporárias devem possuir TTL apropriado.

NÃO mantenha URLs temporárias indefinidamente.

============================================================
33. SEGURANÇA DO PLAYER
============================================================

O player incorporável deve possuir:

- CORS configurável;
- CSP;
- validação de origin;
- tokens quando necessário;
- expiração de tokens;
- rate limiting;
- proteção contra abuso;
- validação de IDs;
- proteção contra SSRF;
- allowlist de hosts quando necessário.

NÃO permita que qualquer usuário use a API como proxy arbitrário para qualquer URL.

============================================================
34. EMBED PARA SITES DE TERCEIROS
============================================================

Criar documentação clara para desenvolvedores.

Exemplo:

<script>
  const player = new ApolofyPlayer({
      container: "#player",
      type: "tv",
      id: "123",
      season: 1,
      episode: 1
  });
</script>

Ou:

<iframe
    src="https://api.apolofy.example/player/tv/123/season/1/episode/1"
    allowfullscreen>
</iframe>

A API deve gerar configurações seguras para o player.

============================================================
35. DOCUMENTAÇÃO DO PLAYER
============================================================

Criar:

PLAYER.md

EMBED.md

PLAYER-API.md

PLAYER-REACT.md

PLAYER-IFRAME.md

Explicar:

- instalação;
- configuração;
- iframe;
- React;
- JavaScript;
- eventos;
- callbacks;
- troca de episódio;
- qualidade;
- legendas;
- fullscreen;
- Picture-in-Picture;
- Cast;
- autenticação;
- segurança;
- CORS.

============================================================
36. EVENTOS DO PLAYER
============================================================

Criar eventos como:

onPlay

onPause

onEnded

onTimeUpdate

onProgress

onVolumeChange

onQualityChange

onSubtitleChange

onEpisodeChange

onError

onFullscreen

onSourceChange

Isso permitirá que o site do usuário controle o player.

============================================================
37. API DO PLAYER PARA O SITE DO USUÁRIO
============================================================

Permitir:

player.play()

player.pause()

player.seek(120)

player.setVolume(0.5)

player.setQuality("1080p")

player.setSubtitle("pt-BR")

player.nextEpisode()

player.previousEpisode()

player.fullscreen()

Os métodos devem funcionar de forma segura e documentada.

============================================================
38. API V1 E V2
============================================================

Preserve endpoints existentes do Anify sempre que possível.

Crie uma API moderna:

/api/v1/...

/api/v2/...

A v2 deve possuir a arquitetura unificada da Apolofy.

============================================================
39. HEALTH
============================================================

Preserve/crie:

GET /health

GET /health/providers

GET /health/database

GET /health/cache

GET /health/player

============================================================
40. SEARCH
============================================================

Implementar:

GET /search

GET /search/advanced

GET /search/anime

GET /search/manga

GET /search/light-novel

GET /search/movie

GET /search/tv

A busca deve poder retornar resultados unificados.

============================================================
41. RECENT
============================================================

Preserve:

GET /recent

Permita:

GET /recent?type=anime

GET /recent?type=tv

GET /recent?type=movie

============================================================
42. SCHEDULE
============================================================

Preserve:

GET /schedule

Expanda para incluir quando disponível:

- anime;
- séries;
- episódios;
- datas;
- temporada;
- horário de lançamento.

============================================================
43. ARTWORK
============================================================

Crie um Artwork Manager.

Prioridade:

1. provider principal;
2. provider secundário;
3. fallback;
4. cache.

Não inventar artwork.

Guardar:

poster
cover
banner
backdrop
logo
thumbnail

============================================================
44. CLASSIFICAÇÃO ETÁRIA
============================================================

Crie AgeRatingService.

Deve suportar:

Anime
Movies
TV
Episodes quando disponível.

Endpoint:

GET /anime/:id/ratings

GET /movie/:id/ratings

GET /tv/:id/ratings

GET /tv/:id/season/:season/episode/:episode/ratings

============================================================
45. CRAWLER
============================================================

Preserve o crawler existente.

Crie novos crawlers somente quando necessário.

O crawler deve poder atualizar:

- filmes;
- séries;
- temporadas;
- episódios;
- anime;
- artwork;
- ratings;
- mappings.

Não faça crawling ilimitado sem controle.

Implementar:

- queue;
- concurrency;
- retry;
- backoff;
- rate limiting;
- cache;
- logs;
- deduplicação.

============================================================
46. LEGALIDADE E SOURCES
============================================================

A Apolofy deve trabalhar com:

- APIs públicas;
- providers autorizados;
- fontes licenciadas;
- conteúdo fornecido pelo próprio usuário;
- fontes cuja utilização seja permitida.

Não implemente:

- bypass de DRM;
- quebra de autenticação;
- invasão de contas;
- contorno de paywalls;
- evasão de mecanismos de proteção;
- coleta de conteúdo sem autorização.

O objetivo do SourceResolver é normalizar e entregar fontes que o sistema está autorizado a utilizar.

============================================================
47. TESTES
============================================================

Crie testes para:

- Anime;
- Manga;
- Light Novel;
- Movies;
- TV;
- Seasons;
- Episodes;
- Search;
- Metadata;
- Artwork;
- Age Ratings;
- Mappings;
- Providers;
- Sources;
- Player;
- iframe;
- React component;
- API;
- Database;
- Cache.

Teste também:

- source indisponível;
- provider indisponível;
- episódio inexistente;
- temporada inexistente;
- artwork inexistente;
- rating inexistente;
- timeout;
- erro de rede.

============================================================
48. DOCKER
============================================================

Criar/atualizar:

Dockerfile

docker-compose.yml

Serviços:

Apolofy API
PostgreSQL
Redis

Comando esperado:

docker compose up -d

============================================================
49. DOCUMENTAÇÃO
============================================================

Criar/atualizar:

README.md
ARCHITECTURE.md
API.md
MOVIES.md
TV.md
ANIME.md
MAPPINGS.md
PROVIDERS.md
SOURCES.md
METADATA.md
ARTWORK.md
AGE-RATINGS.md
PLAYER.md
EMBED.md
PLAYER-API.md
DATABASE.md
CACHE.md
DOCKER.md
DEVELOPMENT.md
CONTRIBUTING.md
LICENSE.md

Utilizar OpenAPI/Swagger.

============================================================
50. LICENÇA E CRÉDITOS
============================================================

O projeto é derivado do Anify.

Não remova os créditos e avisos exigidos pela licença.

O Anify deve continuar sendo reconhecido como projeto-base.

O novo projeto deve se chamar:

APOLOFY API

============================================================
51. ESTRUTURA FINAL
============================================================

A arquitetura final deverá possuir conceitualmente:

apolofy-api/
│
├── anify-backend/
│
├── core/
│   ├── anime/
│   ├── manga/
│   ├── light-novel/
│   ├── mappings/
│   ├── metadata/
│   ├── providers/
│   ├── crawlers/
│   └── database/
│
├── movies/
│
├── tv/
│   ├── series/
│   ├── seasons/
│   └── episodes/
│
├── artwork/
│
├── age-ratings/
│
├── sources/
│
├── player/
│   ├── core/
│   ├── ui/
│   ├── controls/
│   ├── hls/
│   ├── subtitles/
│   ├── quality/
│   ├── fullscreen/
│   ├── cast/
│   ├── iframe/
│   └── react/
│
├── search/
├── cache/
├── database/
├── api/
├── tests/
├── docs/
└── docker/

IMPORTANTE:

Essa é uma estrutura conceitual.

Adapte-a à estrutura REAL do Anify.

Não duplique diretórios se o Anify já possui módulos equivalentes.

============================================================
52. ORDEM OBRIGATÓRIA DE EXECUÇÃO
============================================================

FASE 1
Identificar o diretório atual.

FASE 2
Identificar o Anify já clonado.

FASE 3
Executar git status.

FASE 4
Auditar completamente o projeto.

FASE 5
Executar o backend original.

FASE 6
Executar lint/build/testes.

FASE 7
Estudar especificamente o sistema de providers, mappings, episódios e sources.

FASE 8
Documentar internamente como o Anify funciona.

FASE 9
Criar a base da Apolofy.

FASE 10
Adicionar Movies.

FASE 11
Adicionar TV Series.

FASE 12
Adicionar Seasons.

FASE 13
Adicionar Episodes.

FASE 14
Expandir Anime Seasons/Episodes.

FASE 15
Adicionar Movie Collections/Franchises.

FASE 16
Expandir Metadata.

FASE 17
Adicionar Artwork.

FASE 18
Adicionar Age Ratings.

FASE 19
Expandir Mapping Engine.

FASE 20
Expandir Provider Manager.

FASE 21
Criar SourceResolver para fontes autorizadas.

FASE 22
Criar Apolofy Video Player.

FASE 23
Reproduzir o design visual da imagem fornecida.

FASE 24
Criar iframe embed.

FASE 25
Criar React component.

FASE 26
Criar JavaScript SDK do player quando apropriado.

FASE 27
Criar API de integração do player.

FASE 28
Criar documentação de integração.

FASE 29
Criar testes.

FASE 30
Criar Docker.

FASE 31
Executar build.

FASE 32
Executar testes.

FASE 33
Corrigir erros.

FASE 34
Testar player.

FASE 35
Testar integração iframe.

FASE 36
Testar integração React.

FASE 37
Validar API.

FASE 38
Gerar relatório final.

============================================================
53. RESULTADO FINAL ESPERADO
============================================================

O resultado final deve ser:

APOLOFY API

Uma API baseada na arquitetura do Anify, mas expandida para:

✓ Anime
✓ Mangá
✓ Light Novel
✓ Filmes
✓ Séries
✓ Temporadas
✓ Episódios
✓ Coleções
✓ Franquias
✓ Metadata
✓ Mappings
✓ Providers
✓ Sources autorizadas
✓ Capas
✓ Banners
✓ Backdrops
✓ Classificações etárias
✓ Search
✓ Recent
✓ Schedule
✓ Cache
✓ Database
✓ Player de vídeo
✓ Iframe embed
✓ React Player
✓ JavaScript Player API

============================================================
54. EXPERIÊNCIA FINAL DO USUÁRIO DO SITE
============================================================

O objetivo final é permitir que um desenvolvedor faça:

1. Configure a Apolofy API no próprio site.

2. O site pesquisa:

"Nome do Filme"

ou:

"Nome da Série"

ou:

"Nome do Anime"

3. O site recebe os dados da Apolofy.

4. O site recebe:

- poster;
- banner;
- metadata;
- classificação;
- temporadas;
- episódios;
- sources autorizadas.

5. O visitante seleciona:

ASSISTIR

6. O site abre:

APOLOFY PLAYER

7. O player mostra a interface visual equivalente à imagem fornecida.

8. O player recebe a source através da API.

9. O visitante consegue:

- assistir;
- pausar;
- avançar;
- voltar;
- alterar volume;
- alterar qualidade;
- escolher legenda;
- fullscreen;
- Picture-in-Picture;
- Cast quando suportado;
- trocar episódio;
- ir para próximo episódio.

10. Ao terminar um episódio:

PRÓXIMO EPISÓDIO

11. O player consulta a Apolofy novamente e carrega o próximo episódio.

============================================================
55. NÃO ENTREGAR UM MOCK
============================================================

NÃO crie somente:

- telas falsas;
- JSON falso;
- endpoints que retornam dados estáticos;
- providers simulados;
- player que não reproduz uma source real autorizada;
- seasons fictícias;
- episódios inventados.

Implemente código funcional.

Se determinada integração não puder ser implementada porque não existe uma fonte/API autorizada disponível, crie a interface real do provider e documente claramente:

"Provider não configurado/disponível."

NÃO invente dados.

============================================================
56. REGRA FINAL
============================================================

COMECE AGORA.

Você já possui o repositório Anify no diretório atual.

NÃO clone novamente.

NÃO comece criando outro projeto do zero.

Primeiro descubra exatamente o estado atual do diretório.

Depois estude o Anify.

Depois implemente a Apolofy incrementalmente.

Depois valide.

Depois teste.

Depois corrija.

Depois documente.

Somente no final apresente o relatório completo da implementação.

A prioridade máxima é:

1. preservar o Anify funcional;
2. adicionar Movies;
3. adicionar TV Series;
4. adicionar Seasons;
5. adicionar Episodes;
6. expandir Anime;
7. adicionar Metadata;
8. adicionar Artwork;
9. adicionar Age Ratings;
10. adicionar Sources autorizadas;
11. criar o Apolofy Player;
12. tornar o Player incorporável em sites externos;
13. testar tudo.

COMECE PELO DIRETÓRIO ATUAL.
