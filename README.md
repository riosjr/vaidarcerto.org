# VaiDarCerto.org

O projeto foi construído utilizando uma stack baseada em Javascript, com Gatsby + ReactJS e armazenando os dados no Firebase Firestore. A hospedagem dos assets estáticos e cloud-functions também ficaram no Firebase Hosting + Functions.

Algumas seções do site são geradas estaticamente, como a seção Aprender (e futuramente a de empresas). Por isso, as atualizações entram no ar a cada período de tempo pois exigem um novo build do site.

## Configuração inicial

Para rodar o projeto localmente, é necessário criar alguns arquivos de configuração para a ligação com o Firebase, bem como criar algumas estrutuas iniciais no Firestore. Recomendamos criar um novo projeto no Firebase para testes.

## Configurações Públicas do Firebase:

Para gerar este json de configuração, entre no painel do projeto de testes criado no Firebase e crie um novo aplicativo web. Dentro das informações do projeto há uma seção `Firebase SDK Snippet`, selecione `Configuração`. Copie somente o objeto e salve como `firebase-public.json` na raiz do projeto. Este arquivo é público, mas ele deve apontar para o mesmo projeto de testes para evitar incosistências.

Exemplo:

```
{
  "apiKey": "<API_KEY>",
  "authDomain": "<AUTH_DOMAIN>",
  "databaseURL": "<DATABASE_URL>",
  "projectId": "<PROJECT_ID>",
  "storageBucket": "<STORAGE_BUCKET>",
  "messagingSenderId": "<MSG_SENDER_ID>",
  "appId": "<APP_ID>",
  "measurementId": "<MEASURE_ID>"
}
```

## Configurações Privadas do Firebase:

Configuramos a fonte de dados para o gatsby (por meio do plugin `gatsby-source-firestore`) com chaves de serviço. Estas chaves dão acesso irrestrito ao Firestore. E por este motivo elas não são publicáveis no repositório.

Para gerá-las, nas configurações de projeto, selecione a aba `Contas de Serviço`. Você terá que gerar uma nova chave. Um JSON será gerado e baixado. Salve-o na raíz do projeto com o nome `firebase-private.json`.

# Executando o projeto

Para iniciar o desenvolvimento do projeto, basta executar:

```
gatsby develop
```

Caso você não tenha o gatsby-cli instalado, instale-o por meio da instrução:

```
npm install -g gatsby-cli
```

# Estrutura de Dados no Firestore

## Collection: `learningpaths`

Armazena as trilhas de aprendizado da seção Aprender.

### Caminho no Firestore: 
```
/learningpaths/{id-learning-path}/
```

### Estrutura:

```
slug: url-identificador da trilha de aprendizado.
title: nome da trilha de aprendizado
```

## Collection: `lessons`

Armazena as lições de cada trilha de aprendizado da seção Aprender.

### Caminho no Firestore: 

```
/lessons/{id-lesson}/
```

### Estrutura:

```
title: título da lição
position (number): posição da lição dentro da trilha de aprendizado
video_url: url de embed do youtube (ex: https://www.youtube.com/embed/2P62JuxA4cA)
description: descrição da lição.
learningpath: slug do learningpath que esta lição pertence.
```