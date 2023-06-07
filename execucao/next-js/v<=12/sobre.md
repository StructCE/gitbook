# O que é?

Next js é um _framework full stack_ construído em cima do React, da mesma maneira que React é construído em cima do JS. Por isso é muito simples nos adaptarmos e até usarmos a documentação do react normal para boa parte dos problemas enfrentados.

## Por que usar?

SG (_Static Generation_) e SSR (_Server Side Rendering_) ajudam muito na performance e no SEO (_Search Engine Optimization_) do web app.

Além disso, o diferencial do Next é o ISR (_Incremental Static Regeneration_), ou seja, o Next pode gerar páginas estáticas novas caso necessário. Ou seja, a página é renderizada no servidor uma vez quando surgir a primeira request para ela, e então é guardada em cachê como um _asset_ estático. Essa rota pode ser revalidada para gerar um novo _asset_ estático a ser guardado, caso necessário.

## Diferença principal do nosso React "padrão"

A diferença principal entre o Next e o Create React App (que normalmente usamos em projetos React):

SG (_Static Generation_) e SSR (_Server Side Rendering_) do diretório '/pages'

Geração de rotas a partir da organização de arquivos do diretório '/pages'

Capacidade de dar uma resposta de api (ou seja, com um json), desde que seja feito dentro do diretório 'pages/api/'

## Usando api específica do Next

Next disponibiliza api's construídas em cima do React e que devem ser usadas, como:
- [Link](https://nextjs.org/docs/api-reference/next/link);
- [Router](https://nextjs.org/docs/api-reference/next/router);
- [Head](https://nextjs.org/docs/api-reference/next/head);
- [Image](https://nextjs.org/docs/api-reference/next/image);
- etc.

Exemplo de uso:


```jsx
// src/pages/index.js

import Link from 'next/link'
import Router from 'next/router'
import Head from 'next/head'
import Image from 'next/image'

export default function Home() {
    return (
        <div>
        {/**
            Head é usado para adicionar tags html no head do documento.
            É possível adicionar tags como title, meta, link, etc.
            É essa tag que torna o Next ótimo para SEO.
        **/}
        <Head>
            <title>Home</title>
            <meta name="viewport" content="initial-scale=1.0, width=device-width" />
            <meta name="google" content="unavailable_after: 01 Jan 2021 00:00:00 GMT" />
            {/**]
                Quaisquer outras tags podem ser adicionadas aqui.
                Elas podem depender de uma resposta de api também, por exemplo.
            **/}
        </Head>
        <h1>Home</h1>

        {/**
            Link melhora a performance do app, por usar prefetch em certos casos
        **/}
        <Link href="/sobre">
            <a>Acessar página Sobre</a>
        </Link>
        <br />

        {/**
            Router, em geral, é melhor usado em lógicas mais complexas, como
            redirecionamento condicional,
            acessar proriedades da rota atual, etc.
        **/}
        <button onClick={() => Router.push('/sobre')}>Acessar página Sobre</button>
        <br />

        {/**
            Image é usado para carregar imagens de forma otimizada.
            Como src, deve receber uma imagem importada.
            Também pode receber uma url externa ou um caminho relativo, desde que configurado.
            Caso seja passado um asset não estático para a tag Image, precisa possuir tamanho definido, ou então preencher o pai.
            https://nextjs.org/docs/api-reference/next/image#src
        **/}
        <Image src="/images/nextjs.png" width={200} height={200} />
        </div>
    )
}


```