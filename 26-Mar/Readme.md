# My very first Next.js Web application

### I tried to mock the https://tronaf.dev

#### Reference: https://nextjs.org

# _document.js
- According to Nextxjs site, "A custom Document is commonly used to augment your application's <html> and <body> tags. This is necessary because Next.js pages skip the definition of the surrounding document's markup."
```
import Document, { Html, Head, Main, NextScript } from 'next/document'

class MyDocument extends Document {
  render() {
    return (
      <Html lang='en'>
        <Head>
        <meta name="pcap" content="pcap" />

        </Head>
        <body>
          <Main />
          <NextScript />
        </body>
      </Html>
    )
  }
}

export default MyDocument  
```

# _app.js
- Next.js uses the App component to initialize pages. You can override it and control the page initialization.
```
import 'tailwindcss/tailwind.css'
import Layout from '../components/Layout'

function MyApp({ Component, pageProps }) {

  return (
    <Layout >
      <Component {...pageProps} />
    </Layout>
  )
}

export default MyApp
```

# Layout.js with _app.js
- This component wraps the ```<Component {...pageProps} />``` in the _app.js file
```
import Navigation from './Navigation'
import SearchIcon from './SearchIcon'
import LinkedInIcon from './LinkedInIcon'
import InstagramIcon from './InstagramIcon'
import TronAFLogo from './TronAFLogo'

const Layout = ({ children }) => {
    return (  
        <>  
        <div class="flex items-center justify-between p-2 bg-black">
                    <TronAFLogo />
                    <div class="flex flex-row items-center">
                            <Navigation />
                    <div class="grid grid-cols-3 gap-1 pl-3">
                            <SearchIcon />
                            <LinkedInIcon />  
                            <InstagramIcon />
                    </div>
                    </div>
        </div>
        <div class="min-h-screen flex flex-col justify-start items-center bg-black">
             {children}
        </div>
        </>
        
     
    )
}

export default Layout
```



# Deleted ```postcss.config.js```.....opppsss
- I lost the tailwindcss utiliities applied to my elements when I deleted the file above
```
module.exports = {
    plugins: {
      tailwindcss: {},
      autoprefixer: {},
    },
  }
```
# tailwind.config.js
- By default, Tailwind will look for an optional tailwind.config.js file at the root of your project where you can define any customizations.
```
module.exports = {
  purge: ['./pages/**/*.{js,ts,jsx,tsx}', './components/**/*.{js,ts,jsx,tsx}'],  
  darkMode: false, // or 'media' or 'class'
  theme: {
    extend: {},
  },
  variants: {
    extend: {},
  },
  plugins: [
    require('@tailwindcss/aspect-ratio'),
  ],
}
```
# Title component
- I created a component that creates a consistent look for all pages
```
export default function Title(props) {
    return <h1 class="text-7xl text-green-400 pt-96">{props.title}</h1>
}
```

# Image components
- I wasn't too happy using images as components. I could have used the Image component from next (next/Image)
```
FILE: InstagramIcon.js

import Image from 'next/image'

export default function InstagramIcon() {
    return <Image src="/instagram.svg" width="50" height="50"/>
}
```

# Navigation.js
- I like utilizing the ```as``` prop of link to mask the real url of a specific path.
```
import Link from 'next/link'

export default function Navigation() {
    return(
        <div className="grid grid-cols-6 gap-3 text-white">
            <Link href="/">
                <a>Home</a>
            </Link>
            <Link href="/navigation/mission" as="/mission">
                <a>Mission</a>
            </Link> 
            <Link href="/navigation/players" as="/players">
                <a>Players</a>
            </Link> 
            <Link href="/navigation/projects" as="/projects">
                <a>Projects</a>
            </Link>
            <Link href="/navigation/partners" as="/partners">
                <a>Partners</a>
            </Link> 
            <Link href="/navigation/contact" as="/contact">
                <a>Contact</a>
            </Link>
        </div>
    )
}
```

# What do I need to work on? 
- Parent and child relationship especially when it comes to flex box. Make sure I can take into account 
