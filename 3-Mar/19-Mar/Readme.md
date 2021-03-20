# Next.js Tutorial from Traversy Media

## Styling
- Styles Folder
  - e.g. home.module.css => this is the naming convention when declaring styling for your page
 
## Pages 
- Components inside the pages folder are the ones that will be rendered 
  - _api.js 
  - index.js
  - _document.js => I have to pay close attention to this file

# ```import Head from 'next/head'```
- assists in SEO
- <Head> wraps the met data of the site for SEO
- If you do a view source page, you will see the meta tag
 ```
 const Meta = ({title, keywords, description}) => {
    return (
        <Head>
        <meta name='viewport' content='width=device-width, initial-scale=1' />
        <meta name='keywords' content={keywords} />
        <meta name='description' content={description} />
        <meta charSet='utf-8' />
        <link rel='icon' href='/favicon.ico' />
        <title>{title}</title>
      </Head>
    )
}

Meta.defaultProps = {
    title: 'WebDev Newz',
    keywords: 'web development, programming',
    description: 'Get the latest news in web dev',
  }
 ```
 
 # wrapping _app.js
 - _app.js looks like the parent component
 - Layout.js wrapped all pages/components 
 - The page will have a Nav bar even though moving between routes/pages
 ```
 // _api.js
 function MyApp({ Component, pageProps }) {
  return (
    <Layout>
        <Component {...pageProps} />
    </Layout>
  )
}

// Layout.js
    const Layout = ({ children }) => {
        console.log(children)
        return (
            <>
            <Meta />
            <Nav/>
            <div className={styles.container}>
                <main className={styles.main}>
                    <Header />
                        {children}
                </main>
            </div>
            </>
        )
    }
 ```
# Creating the Nav
- utilize ```import Link from 'next/link'`` for navigation
- After renaming About.js, it looks like ```Link``` looks for the file in the page directory
```
import Link from 'next/link'

import navStyles from '../styles/Nav.module.css'


const Nav = () => {
    return (
        <nav className={navStyles.nav}>
            <ul>
                <li>
                    <Link href="/">Home</Link>
                </li>
                <li>
                    <Link href="/about">About</Link>
                </li>
            </ul>
        </nav>
    )
}

export default Nav
```

 
