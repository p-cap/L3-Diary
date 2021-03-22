#Dynamic Routing NextJs

1. Create the api calls ```getStaticPath``` and ```getStaticProps```
- /api/articles => this route will be used by ```getStaticPaths``` which allows it to build the dynamic paths at build time
```
FILE: index.js

import {articles} from '../../../data'

// pulling the data from the data.js file
// http://localhost:3000/api/artciles

export default function handler(req, res) {
    res.status(200).json(articles)
}
```

- /api/articles/[id].js => this dynamic route will help pull specific information based on the id. The code below is using filter function
```
FILE: [id].js

import {articles} from '../../../data'

export default function handler({query: {id}}, res) {

    const filtered = articles.filter(article => article.id === id)

    if (filtered.length > 0) {
        res.status(200).json(filtered[0])
    } else {
        res.status(404).json({message: `Article with the id of ${id} is not found`})
    }

}
```
2. create the dynamic route based on file structure
- /pages/article/[id]
  - getStaticPaths => build static paths at run time
```
FILE: [id].js

 export const getStaticPaths = async () => {
 
    // res returns all articles based on the api call
    const res = await fetch(`${server}/api/articles/`)

    const articles = await res.json()

    const ids = articles.map(article => article.id)

    const paths = ids.map(id => ({params: {id: id.toString()}}))

    return {    
        paths,
        fallback: false,
    }
}
```
#### NOTE: params must match the parameters used in the page name 
      - page name: /pages/article/[id]
      - params: { params: { id: '1' } }

  - getStaticProps => will return the data based on the api call. The api call filters the response based on the id 
```
  export const getStaticProps = async (context) => {
    const res = await fetch(`${server}/api/articles/${context.params.id}`)
    const article = await res.json()
    return {
        props: {
            article
        }
    }
}
```
3. Create the Link that the component will route to 
```
FILE: /components/ArticleItem.js

import Link from 'next/link'
import articleStyles from '../styles/Article.module.css'


const ArticleItem = ({article}) => {
    return (
       <Link href="/article/[id]" as={`/article/${article.id}`}>
           <a className={articleStyles.card}>
            <h3>{article.title} &rarr;</h3>
            <p>{article.excerpt}</p>
           </a>
     </Link>
    )
}

export default ArticleItem
```
