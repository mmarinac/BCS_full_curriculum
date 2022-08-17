# Routing and query data

## Link

We have already seen how we can change pages using next built-in routing system, which works very similarly to react router as it still uses a Link component to redirect to a page.
One major difference is that in next as we don't define manually the path, so we can't declare in advance the params that we need to receive.
We can overcome this issue by usign query strings instead.
If you are familiar with query strings this won't look new, if you are not then here is the synthax:
```javascript
    import Link from 'next/link';
    // We import the Link from 'next/link
    <Link href = {`/product?_id=${1234}`}>
    // Here we redirect to an hypothetical product page passing a query string with the key of _id and the value of 1234.
```

So after the ? we add our key and after the = we add our value.
If we have multiple query strings we can separate them using the & sign.
for example:

```javascript
<Link href = {`/product?_id=${1234}&product_name=${name}`}>
```

Now the query string we passed will be available in the props in the component that we render when we go to /product, which name is product.js

So in our product.js we can fetch the product by id server side using getInitialprops as shown below
```javascript
Product.getInitialProps = async(props) => {
    return axios
        .get(`http://YOUR_SERVER_ROUTE:YOUR_PORT/${props.query._id}`)
        .then(res => {
            return {product: res.data}
        })
}
```

## Router.push

We can also use Router.push to navigate between pages like in React Router the difference is that you don't have the state object to pass data,
you can use the queries instead and get them in the new page in the getInitialProps method.
```javascript
import Layout from '../components/layout';
//we import the router
import Router from 'next/router'

const Product = () => 
  <Layout>
    <div>
      <button onClick={()=>Router.push({
      	                          pathname:'/',
      	                          query   : {_id:'7sydtf879wf97'}
      	                   })}>Product details</button>
    </div>
  </Layout>

export default Product
```

```javascript
Product.getInitialProps = async(props) => {
    return axios
        .get(`http://YOUR_SERVER_ROUTE:YOUR_PORT/${props.query._id}`)
        .then(res => {
            return {product: res.data}
        })
}
```
