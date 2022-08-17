# Notes about _app.js

In case we need to share data between components in different pages, we can use a top level component, which is at even higher level than the page component, not unlike we would do with React-Router.

This allow us to fetch data server-side and pass it along making it available to all the pages.

We can create a file called _app.js in our pages folder:
/pages/_app.js
```
import App, {Container} from 'next/app'
import React from 'react'
import axios from 'axios';
const isServer = typeof window === 'undefined'
const clientStore = isServer ? null : {}

// Here we can do an initial fetch of data and pass it along to the pages
async function initialFetch() {
    const res =  await axios.get('your_url')
	return {data:res.data}
}
// We extend the original App component.
export default class MyApp extends App {
	static async getInitialProps ({ Component, router, ctx }) {
		let pageProps = {}
		let appData = clientStore ? clientStore.appData : await initialFetch()

		if (Component.getInitialProps) {
			pageProps = await Component.getInitialProps(ctx)
		}

		return {appData, pageProps}
	}

	constructor(props) {
		super(props)

		if(clientStore && !clientStore.appData) {
			clientStore.appData = props.appData
		}
	}

	render () {
		const {Component, pageProps, appData} = this.props
		return <Container>
			<Component 
                {...pageProps} 
                {...appData}
            />
		</Container>
	}
}
```
