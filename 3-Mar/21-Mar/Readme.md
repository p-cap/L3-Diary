# Rendering and Styling fetched data (Nextjs)

1. Create styling for your fetched data. In this case, we copied the styling from the Nextjs boilerplate. Keep in mind, the naming convention is COMPONENT-NAME.module.css.
```
FILE: /styles/Article.module.css

.grid {
    display: flex;
    align-items: center;
    justify-content: center;
    flex-wrap: wrap;
    max-width: 800px;
    margin-top: 3rem;
  }
  
  .card {
    margin: 1rem;
    flex-basis: 45%;
    padding: 1.5rem;
    text-align: left;
    color: inherit;
    text-decoration: none;
    border: 1px solid #eaeaea;
    border-radius: 10px;
    transition: color 0.15s ease, border-color 0.15s ease;
  }
  
  .card:hover,
  .card:focus,
  .card:active {
    color: #0070f3;
    border-color: #0070f3;
  }
  
  .card h3 {
    margin: 0 0 1rem 0;
    font-size: 1.5rem;
  }
  
  .card p {
    margin: 0;
    font-size: 1.25rem;
    line-height: 1.5;
  }
  
  .logo {
    height: 1em;
  }
  
  @media (max-width: 600px) {
    .grid {
      width: 100%;
      flex-direction: column;
    }
  }
```

2. Personally, I would create the item first so I can determine what json data I want to display
```
FILE: /components/ArticleItem.js

// imported the styling for the data
import articleStyles from '../styles/Article.module.css'

const ArticleItem = ({ article }) => {
    return (
        // utilizedd the .card class for styling the data
        <div className={articleStyles.card}>
            <h3>{article.title}</h3>
            <p>{article.excerpt}</p>
        </div>
    )
}

export default ArticleItem
```
3. Thenn, I created the ArticleList that is responsible of mapping through the data
```
FILE: /components/ArticleList.js

// imported the newly created item component
import ArticleItem from '../components/ArticleItem'

// and the styling of course
import articleStyles from '../styles/Article.module.css'

const ArticleList = ({articles}) => {
    return (
        // utilizing the .grid class for styling
        <div className={articleStyles.grid}>
            {articles.map((article) => (
                <ArticleItem article={article} />
            ))}
        </div>
)}

export default ArticleList
```
4. Finally, declaring the ```<ArticleList />``` in ```/pages/index.js```
```
import Head from 'next/head'
import styles from '../styles/Home.module.css'

import TronAFLogo from '../components/TronAFLogo'
import Navigation from '../components/Navigation'

// imported the ArticleList component
import ArticleList from '../components/ArticleList'

export default function Home({articles}) {
  return (
    <div className={styles.container}>
      <Head>
        <title>Pcap's First Nextjs App</title>
        <link rel="icon" href="/favicon.ico" />
      </Head>
      <TronAFLogo />
      <Navigation />
      <main className={styles.main}>
       <h1> Welcome to Pcap's First Nextjs App</h1>
      // here is the ArticleList component
       <ArticleList articles={articles} />
     
      </main>
   </div>
  )
}

export const getStaticProps = async () => {
  const res = await fetch(`http://localhost:3000/api/articles`)

  const articles = await res.json()

  return {
    props: {
      articles
    }
  }
}
```
# STUCKED: MAP SYNTAX
### My data was not rendering because of the code snippet below:
```
{articles.map(article => {
        <h4>{article.title}</h4>
      })}
```
### The correct syntax was 
```
 {articles.map((article) => (
        <h4>{article.title}</h4>
      ))}
```
1. The article argument should be enclosed in a parenthesis independently ```(article)```
2. The expression inside the map should also be in parenthesis 
```
=> (
.....
)
```
