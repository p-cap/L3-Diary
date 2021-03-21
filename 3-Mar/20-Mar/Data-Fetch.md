# API calling with Nextjs
1. Create a smaple data in root of the project
```
FILE: data.js

export const articles = [
    {
        id: '1',
        title: 'GitHub introduces dark mode and auto-merge pull request',
        excerpt:
          'GitHub today announced a bunch of new features at its virtual GitHub...',
        body:
          'GitHub today announced a bunch of new features at its virtual GitHub Universe conference including dark mode, auto-merge pull requests, and Enterprise Server 3.0. In the past couple of years, almost all major apps have rolled out a dark theme for its users, so why not GitHub?',
      },
      {
        id: '2',
        title: 'What’s multi-cloud? And why should developers care?',
        excerpt: 'Most developers don’t care about multi-cloud. But they should...',
        body:
          'Most developers don’t care about multi-cloud. But they should. Whether developers know it or not, their companies likely already have a multi-cloud environment.    Multi-cloud is a strategy where a business selects different services from different cloud providers',
      },
      {
        id: '3',
        title: 'Here is how to make your website more accessible',
        excerpt:
          'An accessible website is one that’s optimized for all people, including those with disabilities...',
        body:
          'There are many things to consider when setting up a website, and accessibility is one factor that can sometimes be overlooked. An accessible website is one that’s optimized for all people, including those with impaired vision or hearing, motor difficulties, or learning disabilities',
      },
      {
        id: '4',
        title: 'Why open ecosystems are the future of app development',
        excerpt:
          'When app stores entered the mainstream tech culture, they exposed developers to an audience of millions...',
        body:
          'We can’t get enough of our mobile apps. There were 204 billion apps downloads last year, and that number is rising in 2020.  When app stores entered the mainstream tech culture, they exposed developers to an audience of millions who were keen to adopt the innovative capabilities',
      },
]
```
2. Creata API path and file
```
FILE: /api/articles/index.js

import { articles } from '../../../data'

export default function handler(req, res) {
    res.status(200).json(articles)
}
```
#### imported articles from data.js
## NOTE: If you rename index.js to another filename, IT WILL NOT WORK
## http://localhost:port/api/articles => you do not need the index.js file in the path when calling the api

# Display the fetched data via API call
1. Utilize the ```getStaticProps``` to fetch data
2. return from ```getStaticProps``` will be the props for the function within the same file
3. map through the fetched data
4. Implement unqiue keys to avoid the warning "Each child in a list should have a unique "key" prop"

```
FILE: index.js (/pages/index.js)

2. => export default function Home({articles}) {
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
                         3. =>  {articles.map((article) => (
                         4. =>    <h3 key={article.id}>{article.title}</h3>
                                  ))}
                   </main>
         </div>
        )
      }

1 => export const getStaticProps = async () => {
      const res = await fetch(`http://localhost:3000/api/articles`) => Needs to be ABSOLUTE PATH
      const articles = await res.json()
      return {
        props: {
          articles
        }
      }
   }

```
